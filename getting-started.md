---

copyright:

  years: 2015, 2019

lastupdated: "2019-09-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:note: .note}

# Getting started with Cloud Foundry Public
{: #getting-started}

<!-- Revamp the getting started to guide the user from the CF overview page in the console, starting with selecting Public. One of the prereqs should be setting up the IBM Cloud environment and point to the Determining your organization architecture topic. -->

{:shortdesc}

## Signing up
{: #ee_start}

Go to the [{{site.data.keyword.Bluemix_notm}} console](https://{DomainName}) and create a Lite account. It's free and never expires. Use the [Liberty for Java](/catalog/starters/cloud-foundry?runtime=liberty-for-java) runtime to build a Cloud Foundry App with upto 256 MB memory. 


## Developing your app
{: #develop}

There are three ways to develop your app:

* With the Continuous Delivery service
* In the dashboard of the IBM Cloud user interface
* At the Cloud Foundry command line

## Developing and deploying your apps by using toolchains and the {{site.data.keyword.contdelivery_short}} service
{: #ee_cd}

[Add a toolchain](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains_getting_started#creating_a_toolchain_from_an_app) that includes the {{site.data.keyword.contdelivery_full}} service to your app. Then, [use the toolchain](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains-using#toolchains-using) to develop and deploy your app.

Try the [Using toolchains with a simple Cloud Foundry app](https://www.ibm.com/cloud/garage/tutorials/introduce-develop-cloud-foundry-app-toolchain) tutorial to learn about using toolchains to modify and continuously deliver a simple "Hello World" sample Cloud Foundry app. 
{:tip}

## Creating your web app with the {{site.data.keyword.Bluemix_notm}} user interface
{: #ee_appui}

After signing up, start to build your first app by using {{site.data.keyword.Bluemix_notm}} catalog and dashboard.

In {{site.data.keyword.Bluemix_notm}}, apps are associated with organizations and spaces. An organization is owned and used by multiple collaborators. Initially, you get a default organization that is named after your user name and you are the only collaborator. You also get a space within this organization. The space is an environment to run your apps; for example, you can have a dev space as a development environment, a test space as a test environment, and a production space as a production environment. Each of the environments belong to a region. With {{site.data.keyword.Bluemix_notm}}, you can deploy your applications to a specific geographical region for lower network latency, data privacy, and better availability.

For this scenario, you want to develop a web app using Node.js. Assume that you are in the US and most of your app users are also in the US. You decide to build and run your app close to your user base, so that you can benefit from lower network latency. After logging in to {{site.data.keyword.Bluemix_notm}}, click the user account preferences link, then select the **US South** region. Then, you can take the following steps to create an app:

  1. Click to **Catalog** in the {{site.data.keyword.Bluemix_notm}} toolbar.
  2. Click **Cloud Foundry Apps** and choose the **Cloud Foundry** tile. 
  3. Click **Public Applications** to select Region and Runtime. 
  4. Type a unique name for your app, and click **Create**. The app name must be unique in the whole {{site.data.keyword.Bluemix_notm}} environment.

Once created, you will see a **Getting started** page in the left navigation pane. Follow the instructions in that page to download the starter code of your app, modify, and deploy it.

The app is created with 1 instance and 512 MB memory quota by default. You can increase the memory, or add more instances to get high availability of your app, for example, 3 instances with 1 GB memory per instance. Click **Overview** to specify your app instances and memory quota. For example, type 3 for instances and 1 GB for memory quota, and click **Save**. You can also see the files, logs, and environment variables to troubleshoot your problems.

### Binding a service by using {{site.data.keyword.Bluemix_notm}} user interface
{: #ee_bindui}

After creating your app, connect to a database with your app. You can store and observe the app data by using database query language. In this scenario, you decide to use the {{site.data.keyword.cloudant}} service that is provided by {{site.data.keyword.Bluemix_notm}}.

To use services within the application, create a service instance and bind your application to the service instance by taking the following steps:

  1. In the {{site.data.keyword.Bluemix_notm}} catalog, select the {{site.data.keyword.cloudant}} service. Add a unique name for your Cloudant service and click **Create**. In the Cloudant Manage panel, launch the service by clicking **Launch**.
  2. Click **Connections**. Then, click **Create connection**.
  3. Click **Connect** next to your app.
  4. The Restage App window is displayed. Click **Restage**.

Now your app is bound to the {{site.data.keyword.cloudant}} service. You can find all the required data for the application to communicate with the service instance in the VCAP_SERVICES environment variable. For example, because {{site.data.keyword.Bluemix_notm}} hosts several applications on the same virtual machine, applications cannot use the same HTTP port number to receive incoming requests. To avoid conflicts, each application is given a unique port number. This port number is available under the VCAP_APP_PORT variable.

You can see the whole list of VCAP_SERVICES associated with your app in the dashboard. To see that list, click the Menu in the IBM Cloud toolbar, then click **Dashboard**. Click your app. Then click **Runtimes** and select the **Environment Variables** tab.

**Note:** This environment variable is the serialization of a JSON object with one entry for each service instance that the app is bound to. The amount and type of data that each service instance provides are service-specific. When your app does not use any service, VCAP_SERVICES is an empty JSON object. This environment variable is used only when you add a service to your app.

## Building your app by using cf cli
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} provides several tools for you to start coding with your app, for example cf command line interface and Eclipse tools. You can choose the cf command line interface to start coding with your app.

  1. First, download and develop the code of your app.

    1. Click Getting started in your app dashboard. Click the **Download the sample code** link to download your app code.
    2. Extract the downloaded file to a directory.
    3. Develop the code with your local integrated development environment.

  2. Install the **cf** command line interface (CLI).

    1. Download the cf command line tool installation program for your operating system.
    2. Follow the tool wizard to complete the installation.
    3. Use the `cf -v` command to verify the version of the cf command line interface.

    **Requirement:** Make sure that you always use the latest version of the cf command line tool.

  3. After you install the **cf** command line interface, you must specify which {{site.data.keyword.Bluemix_notm}} region you want to work with by using the **cf api** command. The API endpoint for the US South region is `api.us-south.cf.cloud.ibm.com`. Additonal API endpoints for other regions can be found [here](/docs/cloud-foundry-public?topic=cloud-foundry-public-endpoints). Enter the following command to connect to {{site.data.keyword.Bluemix_notm}}:

  ```
  cf api api.us-south.cf.cloud.ibm.com
  ```

  To find other API endpoints, see [Regions and Endpoints](/docs/cloud-foundry-public?topic=cloud-foundry-public-endpoints). After you specify the {{site.data.keyword.Bluemix_notm}} region, the location information that you specified is saved.

  4. Next, log in to {{site.data.keyword.Bluemix_notm}} by using the `cf login` command.

  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```

  If your organization uses single sign on, use `cf login -sso`.

  5. After you are logged in to {{site.data.keyword.Bluemix_notm}}, you are ready to deploy your app back to {{site.data.keyword.Bluemix_notm}}. From your app directory , enter the following command:

  ```
  cf push [your_appname]
  ```

  For more information, see [`**cf push**`](/docs/cli/reference/ibmcloud?topic=cf-cli-plugin-cf-cli-plugin#cf_push).

  6. Now, you can access the app by entering the following app URL in a browser:
  ```
  http://your_app.us-south.cf.appdomain.cloud
  ```

You can also choose other tools to build your app, such as Eclipse tools. For more information, see the Getting started page of your app in the {{site.data.keyword.Bluemix_notm}} dashboard.

### Binding a service by using cf cli
{: #ee_cfbind}

You can also bind a service by using the **cf** command line interface. Assume that you want to add the {{site.data.keyword.cloudant}} service to your app with the cf command line interface.

To use the {{site.data.keyword.cloudant}} service within your app, create a Cloudant service instance, bind your app to the service instance, and then use the service instance. The same procedure applies to all the other services.

  1. Create a Cloudant NoSQL DB service instance.

  Use the cf create-service command to create a new instance of a service. In this example, *Lite* is the name of the plan. For example:

  ```
  cf create-service cloudantNoSQLDB Lite [your_name_for_your_cloudant_service]
  ```

  You can also use the cf services command to see the list of service instances that you created.

  ```
  cf services
  ```

  After a service instance is created, it is available for any of your applications to bind and use.

  2. Bind the service instance to your app.

  To use a service instance, you must bind it to your application. Use the cf bind-service command to bind a service instance to an application by specifying the application name and the service instance that you created.

  ```
  cf bind-service [your_app_name] [your_name_for_your_cloudant_service]
  ```

  Binding a service instance to an application enables {{site.data.keyword.Bluemix_notm}} to communicate to the service, and to specify that a new application will communicate with that service instance. For different services, {{site.data.keyword.Bluemix_notm}} might process the application and the service instance differently during the binding. For example, some services might create a new tenant for each application that communicates to the service instance. The service responds back to {{site.data.keyword.Bluemix_notm}} with information, such as credentials, that must be passed to the application for communication between the application and the service.

  **Note:** If the application is running when it is bound to a service instance, the VCAP_SERVICES environment variable is not updated until the application is restarted. To restart your application, use the cf restart command.

  3. Use the service instance.

  In this scenario, the VCAP_SERVICES environment variable includes information, such as the following items, that an application can use to connect to this instance of {{site.data.keyword.cloudant}}:

  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>secret</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dl>

  For example, your Node.js app might access this information as follows:
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```

  **Note:** As the sample code shows, to connect to a {{site.data.keyword.cloudant}} service instance, you can check whether the VCAP_SERVICES environment variable exists first. If it exists, the application can use the cloudant variable's properties to access the database. However, if the VCAP_SERVICES environment variable is not present, the local {{site.data.keyword.cloudant}} service instance is used with the default values that are provided.

  4. Interact with the service instance.

  You can interact with the service instance by using the credential information. The actions that you can take include read, write, and update. The following example demonstrates how to insert a JSON object into the {{site.data.keyword.cloudant}} service instance:

  ```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```

  5. **Optional:** Unbind or delete a service instance.

  You might want to unbind or delete a service instance when it is no longer used or when you want to free up some spaces. To unbind a service instance from your app, use the **cf unbind-service command**; to delete a service instance, use the **cf delete-service** command.

  For more information about services, see Services. For more information about the **cf** options that you can use to manage your applications in the {{site.data.keyword.Bluemix_notm}} environment, issue **cf --help** in the **cf** command line interface.

  **Note:** Ensure that you no longer require a service instance before you delete it. Deleting a service instance erases all data that is associated with that instance of the service. Any application that is bound to a deleted service cannot have its VCAP_SERVICES environment variable updated until the application is restarted.

## Calculating your app cost
{: #ee_billing}

Your 30-day free trial has expired, but you want to continue to use {{site.data.keyword.Bluemix_notm}}. You must add your credit card information for a Pay As You Go account or a Subscription account to continue using {{site.data.keyword.Bluemix_notm}}. However, {{site.data.keyword.Bluemix_notm}} still provides free allowances for most of the runtime frameworks and services even if you convert to a pay account. You are not charged by {{site.data.keyword.Bluemix_notm}} unless the usage is beyond the free allowances.

{{site.data.keyword.Bluemix_notm}} provides an estimator and calculator for you to see your app cost. You can see the cost of your app in the following ways:

  * In your dashboard, click your app. Then, in the Overview page, click **estimate the cost of this app** to see the price of **SDK for Node.js** runtime and Support, and the total monthly price of your app.

  * Or, in the Pricing Sheet page, type the monthly usage of the runtime and services of your app. For example, 3 instances of **SDK for Node.js** with 1 GB memory for each instance. The monthly price is calculated and displayed.

You can also calculate your app cost manually by adding up the prices of your runtimes and services and deducting the free allowance. For more information, see Calculating your costs manually.

## Removing apps
{: #ee_removing}

As you build more apps, the quota might approach the limit. However, some apps that you might no longer use still occupy the quota. It’s easy to delete apps to free up some spaces in {{site.data.keyword.Bluemix_notm}} at any time.

In {{site.data.keyword.Bluemix_notm}} user interface, go to the app **Overview** page, click the **Menu** icon, and delete the app that you no longer use. You can also use the **cf delete** command to delete apps.
