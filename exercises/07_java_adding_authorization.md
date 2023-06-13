# Authorization and Authentication

Authorization means restricting access to data by adding respective declarations to CDS models, which are then enforced in service implementations. Individual privileges are given by adding such declarations. While, authorization verifies the user's identity and the presented claims such as granted roles and tenant membership.

## Prepare User Authentication and Authorization (XSUAA) Setup

### Roles and scopes
A scope represents a single authorization to perform an action. For example, there could be a scope “Read” and a scope “Write”. The scope allows a user to read or write a certain business object. Scopes can’t be assigned to users directly. They’re packaged into roles. For example, there could a role “Editor” consisting of the “Read” and “Write” scopes, while the role “Viewer” consists only of the “Read” scope.

<br/> <br/>
For this example, we can add access restriction to our `CustomersService`.

Edit the `srv/incidents-service.cds` file as follows:

```sh
service IncidentsService @(requires: 'admin') {
    ...
}
```

This will make the incidents service accesible to only the `admin` roles.
Once the server is reloaded, a pop-up will come on IncidentsService, we can check our implementation here.

`@sap/cds` has some users as default configuration. You can use `alice` as username to check for the `admin` right and `bob` as username to check for when the `admin` right are not there. When you use `alice`, you will be able to access the application whereas when you use `bob`, it will throw an error.

We can define the roles in our `srv/src/main/resources/application.yaml` by adding the following snippet in there *under the cds node*:

```yaml
  security.mock.users:
  - name: admin1
    password: abcd
    roles:
    - admin
```

The complete `srv/src/main/resources/application.yaml` file needs to look like this:

```yaml
---
spring:
  config.activate.on-profile: default
cds:
  datasource:
    auto-config.enabled: false
  security.mock.users:
    - name: admin1
      password: abcd
      roles:
      - admin
```

Addtionally, you need to add the Spring Boot Security starter module to the `<dependencies>` section in the `pom.xml` fil` in the `srv` folder of your application:

```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
```

You can check the access to the application by using the new credentials (username: admin1 and password: abcd) now.
<br/>

To learn more about Authorization and Authentication methods, you can refer [here](https://cap.cloud.sap/docs/guides/authorization#prerequisite-authentication)

***

Proceed with the next step: [(Optional) Add multitenancy](08_java_optional_add_multitenancy.md)