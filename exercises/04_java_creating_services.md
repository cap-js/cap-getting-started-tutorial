# Creating Services

After defining the model, the running application is still not exposing any service endpoints.

It's a good practice in CAP to create one service per use case. Hence, we will add two service definitions for the different use cases:

- A `CustomersService` for customers to create and browse their own incidents.
- An `IncidentsService` for support engineers to process incidents created by customers.

## Steps:

1. Create a new file `customers-service.cds` in the `srv` folder of your project.

2. Copy the following content in the file:

```cds
using { sap.capire.incidents as my } from '../db/schema';

/**
 * Used by Customers to create and browse their Incidents.
 */
service CustomersService {
  entity Incidents as projection on my.Incidents { *
  } excluding { modifiedBy } where customer.ID = $user;
}
```

3. Create a new file `incidents-service.cds` in the `srv` folder of your project.

4. Copy the following content in the file:

```cds
using { sap.capire.incidents as my } from '../db/schema';

service IncidentsService { 
  @odata.draft.enabled
  entity Incidents as projection on my.Incidents;
  entity Customers as projection on my.Customers;
  entity Conversations as projection on my.Conversations;
  entity Urgency as projection on my.Urgency;
  entity Status as projection on my.Status;
}
```

The application is reloaded, open the url mentioned in the terminal in your browser and you can see the generic index.html page. If you don't find the link in the terminal output, you can also use the "Ports Preview" (press `F1 and type `Ports`) and select port `8080`.
<br/>

![Endpoints](assets/services_java.png)
<br/>

## Adding Custom Logic

You can add custom code to deal with the specific domain logic of your application.

- Create a new folder `handlers` in the `srv/src/main/java/customer/incidents` folder.
- Create a new file `IncidentUrgencyHandler.java` in that folder and add the following content:

```java
package customer.incidents.handlers;


import java.util.List;
import java.util.Locale;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

import com.sap.cds.services.cds.CqnService;
import com.sap.cds.services.handler.EventHandler;
import com.sap.cds.services.handler.annotations.After;
import com.sap.cds.services.handler.annotations.ServiceName;

import cds.gen.incidentsservice.Incidents;
import cds.gen.incidentsservice.IncidentsService_;

@Component
@ServiceName(IncidentsService_.CDS_NAME)  
public class IncidentUrgencyHandler implements EventHandler {

    private static final Logger logger = LoggerFactory.getLogger(IncidentUrgencyHandler.class);
    @After(event = CqnService.EVENT_READ)  
    public void ensureHighUrgencyForIncidentsWithUrgentInTitle(List<Incidents> incidents) {  

        for (Incidents incident : incidents) {
            if (incident.getTitle() != null &&
				incident.getTitle().toLowerCase(Locale.ENGLISH).contains("urgent") &&  
                incident.getUrgencyCode() == null || !"H".equals(incident.getUrgencyCode())) {  

                incident.setUrgencyCode("H");  
                logger.info("Adjusted Urgency for incident '{}' to 'HIGH'.", incident.getTitle());  
            }  
        }  
    }  
}
```

**Note:** this is the first (and last;)) time in this tutorial where you create Java code. It might happen that the Java support in BAS fails to correctly pick up the code generated from CDS files and gives some error markers in the inserted Java code. In that case you can try one of the following techniques:

 * Press ctrl+shift+p (the command pallette) and type "Java: Clean Java Lanaguage Server Workspace"
 * Press ctrl+shift+p (the command pallette) and type "Java: Force Java Compilation"

Afterwards the error markers should be gone. If not it's still not a road blocker since the `mvn cds:watch` command does not care about IDE errors. ;)

In case you still run into issues with this handler (you'll see that in the stack trace of the application log) you can just comment the `@After` annotation in line 24. Then this handler will not be called at runtime.

You can read more about [Providing Services](https://cap.cloud.sap/docs/guides/providing-services) 

***

Proceed with the next step: [Adding data](05_java_adding_data.md)
