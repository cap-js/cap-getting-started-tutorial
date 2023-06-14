# Setting up Dev Environment

1. Open the [Business Application Studio](https://bas-dlm-eu12.eu12cf.int.applicationstudio.cloud.sap/index.html)
2. Click on `Create Dev Space`
<br/>

![Create Dev Space](./assets/create_dev_space.png)
<br/>

3. You will be redirected to choose what kind of application you want to create and to choose the name of the dev space.
<br/>

Here, you can name the dev space as `incidents_mgmt` and choose `Full Stack Cloud Application`
<br/>

![Full Stack Cloud Application](./assets/full_stack_application.png)
<br/>

4. Click on `Create Dev Space`
<br/>

![Create Dev Space](./assets/create_space.png)
<br/>

5. Wait for the dev space to start, once it has started running, you can open it.
<br/>

![Open Space](./assets/spaces.png)
<br/>

6. Once your space is opened you need to perform a small adjustment to the settings in order to have a smooth developer experience while developing your CAP Java application. Click the cog-wheel in the bottom left corner and then click "settings". Perform the following 2 steps.
<br/>

7. At first you need to *enable* "autobuild" for Java artifacts. This is needed to have quick turnarounds with Spring Boot DevTools while using `mvn cds:watch`.
<br/>

![enable Java autobuild](./assets/java_auto_build.png)

<br/>

8. Then, you need to *disable* "auto save". This prevents that an automatic, yet incremental, build is triggered after each key-stroke. ;-)

![disable auto save](./assets/java_auto_save.png)

7. Your space is ready for use. You can open the terminal by clicking on the top left button and then `Terminal -> New Terminal`
<br/>

![Open Terminal](./assets/Terminal.png)

***

Proceed with the next step: [Introduction to the Incident Management application](02_java_introduction_to_incident_management_application.md)