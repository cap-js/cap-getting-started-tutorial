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

We can define the roles in our `package.json` by adding the following snippet as node *below the top level object*:

```sh
"cds":{
    "requires":{
        "auth":{
            "kind": "basic",
            "users": {
                "admin1": {
                    "password": "abcd",
                    "roles": [
                        "admin"
                    ]
                }
            }
        }
    }
}
```

You can check the access to the application by using these credentials now.
<br/>

To learn more about Authorization and Authentication methods, you can refer [here](https://cap.cloud.sap/docs/guides/authorization#prerequisite-authentication)

***

Congratulations! You finished the CAP Getting Started tutorial.
