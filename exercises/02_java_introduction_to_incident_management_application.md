# Incident Management Application

In this exercise we assume we are a developer given the task to implement an application to create and manage incidents, that is customer support messages.
The application will allow customers to create incidents, processed by support team members. Both add comments to a conversation. Eventually, a repair appointment is created with a service worker assigned.

## Create a new project

To create a new CAP project, you can use the `cds init` command. This command creates the needed project configuration for you to start developing your application. Since this exercise is about creating a simple incident management application, the project name will be `incidents`.

Use the following command in the terminal:
```sh
cds init incidents --add java
```

## Load the project in the editor

Now, it's time to load our IDE and access the newly created directory.
You can open the project folder `incidents` in your choice of IDE

In BAS:

1. Go to `Explorer -> Open Folder`
<br/>

![Open Folder](./assets/open_folder.png)
<br/>

2. Choose `incidents` from the file explorer.
<br/>

![Open Application](./assets/incidents_mgmt_java.png)
<br/>

Basic CAP structure containing folder `db` and `srv` has been created. 

For now, the CAP Java application cannot serve any purpose as it has neither defined a domain model nor a service interface. This will be done in the following steps.


***

Proceed with the next step: [Domain modeling](03_java_domain_modeling.md)
