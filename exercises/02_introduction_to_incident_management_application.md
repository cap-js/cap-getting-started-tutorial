# Incident Management Application

In this exercise we assume we are a developer given the task to implement an application to create and manage incidents, that is customer support messages.
The application will allow customers to create incidents, processed by support team members. Both add comments to a conversation. Eventually, a repair appointment is created with a service worker assigned.

## Create a new project

To create a new CAP project, you can use the `cds init` command. This command creates the needed project configuration for you to start developing your application. Since this exercise is about creating a simple incident management application, the project name will be `incidents-mgmt`.

Use the following command in the terminal:
```sh
cds init incidents-mgmt
```

## Load the project in the editor

Now, it's time to load our IDE and access the newly created directory.
You can open the project folder `incidents-mgmt` in your choice of IDE

In BAS:

1. Go to `Explorer -> Open Folder`
<br/>

![Open Folder](./assets/open_folder.png)
<br/>

2. Choose `incidents-mgmt` from the file explorer.
<br/>

![Open Application](./assets/incidents_mgmt.png)
<br/>

Basic CAP structure containing folder `app`, `db` and `srv` has been created. 

Open the terminal and use the command: 
```sh
npm install
``` 
to install the dependencies.

Start the CAP server by using `cds watch` in the Integrated Terminal.

```sh
cds watch
```
The CAP server serves all the CAP sources from your project. It also "watches" all the files in your projects and conveniently restarts whenever you save a file. Changes you have made will immediately be served without you having to do anything.
<br/>

Currently, it will show 

`No service definitions found in loaded models...`
<br/>

It tells you that there is no model and no service definitions yet that it can serve.
<br/>

We will be adding the service definitions in the upcoming modules.