# Adding Data to your database

## Using In-Memory Database
`cds watch` automatically bootstraps a database by default - unless told otherwise. It drastically speeds up turn-around times in local development and furthermore allows self-contained testing.
<br/>

Since we already have an SQLite in-memory database that was automatically created, let's now fill it with some test data.

### Adding Initial Data in `.csv` Files

First, make sure that you're in the root directory of the `incidents` application. If you're in the `srv` folder go one up with this command:

```sh
cd ..
```

You can fill your database with initial data by adding a few plain CSV files. For each entity that you want to populate with mock-data, you can add the mockdata files using the naming convention `{enityNamespace}-{entityName}.csv` files in the `db/data` folder or use the following command:

```sh
cds add data
```

It will generate `.csv` templates which can be filled with the following content. Please make sure that you replace the full content of the file including the header columns.

`sap.capire.incidents-Conversations.csv`
```csv
ID, Incidents_ID, timestamp,author,message
2b23bb4b-4ac7-4a24-ac02-aa10cabd842c,3b23bb4b-4ac7-4a24-ac02-aa10cabd842c, 1995-12-17T03:24:00Z,Harry Potter,My broom doesn't work
2b23bb4b-4ac7-4a24-ac02-aa10cabd843c,3a4ede72-244a-4f5f-8efa-b17e032d01ee,1995-12-18T04:24:00Z,Gladys Boothby,What exactly is wrong?
9583f982-d7df-4aad-ab26-301d4a157cd7,3583f982-d7df-4aad-ab26-301d4a157cd7,2022-09-04T12:00:00Z,Sunny Sunshine,"Solar panel is broken, please check"
9583f982-d7df-4aad-ab26-301d4a158cd7,3ccf474c-3881-44b7-99fb-59a2a4668418,2022-09-04T13:00:00Z,Bradley Flowers,What exactly is wrong?
```

`sap.capire.incidents-Customers.csv`
```csv
ID,firstName,lastName,email,phone,streetAddress,city,postcode
8fc8231b-f6d7-43d1-a7e1-725c8e988d18,Harry,Potter,harry.potter@demo.com,+44-555-123,4 Privet Drive Little Whinging, Surrey, 1234"
feb04eac-f84f-4232-bd4f-80a178f24a17,Sherlock,Holmes,sherlock.holmes@demo.com,,221B Baker Street,London,NW1 6XE
2b87f6ca-28a2-41d6-8c69-ccf16aa6389d,Sunny,Sunshine,sunny.sunshine@demo.com,+01-555-789,11111 W Sunset Blv,Los Angeles,90049
```

`sap.capire.incidents-Incidents.csv`
```csv
ID,customer_ID,title,urgency_code,status_code
3b23bb4b-4ac7-4a24-ac02-aa10cabd842c,8fc8231b-f6d7-43d1-a7e1-725c8e988d18,Broomstick doesn't fly,H,C
3a4ede72-244a-4f5f-8efa-b17e032d01ee,feb04eac-f84f-4232-bd4f-80a178f24a17,Ran out of tea,H,N
3ccf474c-3881-44b7-99fb-59a2a4668418,feb04eac-f84f-4232-bd4f-80a178f24a17,Violin broken,M,N
3583f982-d7df-4aad-ab26-301d4a157cd7,2b87f6ca-28a2-41d6-8c69-ccf16aa6389d,Solar panel broken,H,I
```

`sap.capire.incidents-Status.csv`
```csv
code;descr
N;new
A;assigned 
I;in_process 
H;on_hold
R;resolved 
C;closed
```

`sap.capire.incidents-Urgency.csv`
```csv
code;descr
H;high
M;medium
L;low
```

Once added, the running `mvn cds:watch` will automatically refresh the data.
You can open the application by using `Command Palette` (F1 or Command+Shift+P) -> `Ports: Preview` and selecting the port 8080. In your browser, you will now be able to see the data in the corresponding endpoints.

In contrast to other tutorials that you run on your local machine you can't use localhost because you don't develop on your local host. ;)

***

Proceed with the next step: [Adding Fiori Elements](06_java_adding_fiori_elements.md)