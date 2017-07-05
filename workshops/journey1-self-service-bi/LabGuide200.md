# Demo Introduction

## Keywords:

```
Oracle Integration Cloud Service, Oracle Storage Cloud Service
```
## Goal of Demo:

To demonstrate how easily to leverage Oracle Integration Cloud Service to build integration
to pull Twitter feeds which the user cares about and store the data into Data Lake in Oracle
Storage Cloud.

## Pre-requisites:

User has registered both Oracle Integration Cloud Service and Oracle Storage Cloud Service.
The storage containers for the demo have been configured properly.

User already has a Twitter account.

# Demo Steps

## Step 1: Create an Application in Twitter

This step will create an application in Twitter. However it is actually not an application
running in Twitter. Instead it is for allocating OAuth 1.0 credentials for an remote application
which can request Twitter services, for example retrieving feeds, creating Twitter message etc.

To create an application in Twitter, open a browser and access Twitter Application
Management System with the URL: https://apps.twitter.com/. After a successful login with your
Twitter account, you will see following Application Management page:

![](images/200/Twitter.png)


Click **Create New App** button to load the page below to create a new application.

![](images/200/createapplication.png)


**Name** of the application must be unique among all users in Twitter. You’d better adding a
user-specific prefix to the name. **Website** of the application must start with a protocol, either
http or https in the demo. **Callback URL** is only necessary if the application need to request
Twitter services as some other accounts. In the Oracle Integration Cloud Service, it only allows to
use same account, so can leave the field empty.

After reading and accepting Twitter Developer Agreement, click **Create your Twitter
application** button at bottom.

When the application is created, following application page will appear. You can review
general information of the application. But the most critical information we need in the Oracle
Integration Cloud Service is OAuth 1.0 credentials.
![](images/200/ICSBigdata.png)

Select **Keys and Access Tokens** tab in the page. By default, only Consumer Key & Secret are
generated. In this demo, we also need to allocate Access Token to access Twitter service from
application.

![](images/200/appsetting.png)

Select **Keys and Access Tokens** tab in the page. By default, only Consumer Key & Secret are
generated. In this demo, we also need to allocate Access Token to access Twitter service from
application. Click **Create my access token** button in Token Actions section to generate required
credentials.

Keep Consumer Key/Secret and Access Token/Secret pairs confidentially for configuring
connections to Twitter with Oracle Cloud Integration Service.

![](images/200/twitter5.png)

## Step 2 : Configure Connections in Oracle Integration Cloud Service

Oracle Integration Cloud Service can leverage built-in adapters to connect various kinds of
external services. In this step, we will configure connections to Twitter and Oracle Storage Cloud
Services.

You need to first login to Oracle Cloud to configure Oracle Integration Cloud Service. Open a
browser, and then enter the URL of Oracle Cloud. Click **Sign In** link on the top to access following
page:

![](images/200/Twitter6.png)


Oracle Cloud will leverage data center infrastructure in different spots across the world.
After registering to Oracle Cloud, customers can request services from the data center near their
location to get better performance.

When login to Oracle Cloud, customers need to first select the data center where their
services have been deployed.

![](images/200/Twitter7.png)


Identity Domain is the container where accounts and Cloud Services are provisioned.
Customers must select the correct Identity Domain to login and access their services. In this
demo, user should select the Identity Domain where Oracle Integration Service is provisioned.

![](images/200/Twitter8.png)


Then, credential information need to input to login to Oracle Cloud platform. After login to
Oracle Cloud, user can view and access cloud services from following page.

![](images/200/Twitter9.png)


Select **Integration** catalog in this page to jump to following Oracle Integration Service page.
From the **Overview** page, user can view current instances of Oracle Integration Cloud Service.
Integrations are configured and deployed in separate service instances.

![](images/200/Twitter10.png)


Click **Open Service Console** link of the service instance where connections and integrations
will be configured. Integration Service Console will display as below:

![](images/200/Twitter11.png)

**2 .1 Configure connection to Twitter**


Click Create Connections in the Console to load the Connection Designer page:

![](images/200/Twitter12.png)


Click **New Connection** action in the page, following Wizard will appear to let you first select
from pre-built adapters.

![](images/200/Twitter13.png)

Scroll down to the bottom of the list you can find **Twitter** adapter, click **Select** button to
confirm your selection. A Twitter connection configuration page will appear, first following dialog
will pop up to input general information of the connection.

![](images/200/Twitter14.png)

Specify a name of the connection, and select the **Role** to **Invoke** to allow request services to
Twitter. Click **Create** button to create the connection.

After the connection is successfully created, you can see a light-green banner on top of the
page. Next you need to configure parameters of the connection.

![](images/200/Twitter15.png)


Click **Configure Security** button in the page, following dialog will appear to let you input
credential information to establish the Twitter connection.

![](images/200/Twitter16.png)


All credential information used in this dialog is from previous step. You can copy those
parameters from Twitter Application Management page directly. After fill all required fields, click
**OK** button.

Now all required parameters have been configured for the Twitter connection. However it is
not sure that the connection will work. Click **Test** action on top of the page to trigger a test. If the
test passed, a message will display in the light-green banner. Also the progress icon on the right
will indicate that the connection is 100 percent correct.

After test is done, you can save the connection by clicking **Save** action. Then click **Exit
Connection** action to go back to Connection Designer page.

![](images/200/Twitter17.png)


**2.2 Configure connection to Oracle Storage Cloud Service**

In the Connection Designer page, click **New Connection** action to launch the Adapter
Selection dialog. Oracle Integration Service does not provide built-in adapter for Oracle Storage
Cloud Service, however user can leverage generic REST adapter to access REST API endpoint of
the Oracle Storage Cloud.

In the search box of the dialog, input “REST” then click the search icon, the REST adapter will
be the only available adapter in the list.

![](images/200/Twitter18.png)

Click **Select** action in the REST adapter, the connection design page will show again to let you
configure the connection to Oracle Storage Cloud Service.

First, following dialog will appear to collect general information of the connection.

![](images/200/Twitter19.png)

Specify the name of the connection and select **Role** to **Trigger and Invoke** which means that
the connection can both receive notification from Oracle Storage Cloud when Object Store is
changed and make requests to the Oracle Storage Service. Click **Create** button to create the
connection.

Next, we need to input the connection parameters to REST API endpoint of the Oracle
Storage Cloud. Click **Configure Connectivity** button in the page to launch following dialog.

![](images/200/Twitter20.png)


Set **Connection Type** to “REST API Base URL”, select **TLS Version** to “TLS V1.1” and copy the
base url (without URI part) of the REST API endpoint of the Storage Cloud to the **Connection URL**
field. Click **OK** to close the dialog.

The last parameters need to configure is the security information to login to REST API
endpoint of the Storage Cloud. Click **Configure Security** button in the page to launch following
dialog.

All the information in this dialog can be known from the Oracle Storage Cloud configuration.
Format of the **Username** filed is “Storage-\<Identity Domain\>:\<login name\>”.

![](images/200/Twitter21.png)


After specifying all required information, click **OK** to close the dialog.
Now all required parameters have been configured for the Oracle Storage Cloud connection.
A test is also required to ensure the configuration is correct. After test is done, click **Save** action
to save the connection, and then click **Exit Connection** action to return to Connection Design
page.

## Step 3 : Design the Integration

In this step, we will demonstrate how to design integrations with Oracle Integration Cloud
Service to load Twitter feeds that the user is interested in and pull the data into Data Lake in
Oracle Storage Cloud.

Oracle Integration Cloud Service provides an interactive tool for designing integrations with
zero coding. The tool is available from the Designer Portal in Oracle Integration Cloud Service


page. To go to Designer Portal, select **Designer** link on top of the Oracle Integration Cloud Service
page.

![](images/200/Twitter22.png)


From Designer Portal user can go directly to various designer tools, for example Integration
Designer, Connection Designer etc., in Oracle Integration Cloud Service. Click **Integrations** icon to
launch following Integration Designer.

![](images/200/Twitter23.png)

User can manage and monitor integrations in the designer page. To create a new integration,
click **New Integration** button on the top. Oracle Integration Cloud Service has pre-defined styles
or patterns to design the integration.

![](images/200/Twitter24.png)


In this demo, the integration is complex. It needs to handle connections to both Twitter and
Oracle Storage Cloud carefully. User also needs to control data ingestion, transform and output at
fine-grained level.

Select the **Orchestration** pattern for the integration, following dialog will pop up to allow
user provide general information of the integration.

Name, version and an optional package are used to uniquely identify the integration. An
integration could be triggered either by an event from a service connection or a schedule defined
by Oracle Integration platform.

![](images/200/Twitter25.png)

Select Schedule as trigger for the integration, and specify name, version and package for the

integration, then click **Create** button.

Following Designer page will appear to give user an interactive interface to design logic of
the integration. On the left of the page are popup toolboxes. User can select to **Invoke** an
available services, add an **Action** and handle **Error** in the integration. In the middle of the page
are panel to view and edit the integration interactively. If the integration logic is very complex,
user can also zoom and go to different part of the view with UI controls in the page.

![](images/200/Twitter26.png)

At initial, only a start and end node in the integration design page. User needs to add more
logic to the integration.

In the demo, we will first invoke Twitter to retrieve any new feeds. Move the mouse to
INVOKES tab on the left, it will pop up a toolbox to let user select available services. Select
Twitter catalog, all Twitter service connections will show just below the catalog.

![](images/200/Twitter27.png)

Drag the connection in between start and end node of the flow in the design panel.

![](images/200/Twitter28.png)

Following wizard will appear to let use customize the service invocation. The **Basic Info** tab
let user assign a name of the invocation. The name will show as display name of the invocation
node in the design panel.

![](images/200/Twitter29.png)

After filling the required information, click **Next** button to move to following page. In this
page user can select which service function need to invoke from the integration.

![](images/200/Twitter30.png)

Select “Search tweets” from the function list, then click **Next** button to move to following
page. This page will show overview information of the invocation. User has the opportunity to
check the configuration, if anything is wrong, they can go back to previous page to make
modification.

![](images/200/Twitter31.png)


Click **Done** to accept the configuration. A new invocation node will appear in the design
panel. However it is not done yet, user also needs to customize parameters of the invocation.
Click the invocation node, a pop up toolbox will appear.

![](images/200/Twitter32.png)

Click button in the toolbox to launch following dialog to map invocation parameters.
Available parameters of the service call are listed on the right. User can design mapping for each
individual parameter. A mapping is the way to assign runtime value of the target of existing
sources. The source could be a static value, data from an available data source etc. Click a
parameter in the list can modify the mapping.

![](images/200/Twitter33.png)

The first parameter needs to customize in the demo is **q**. Click the parameter will launch
another dialog to design the mapping. User can select an entity from a source on the left, and
drag it to link with the target. Also user can assign a fixed value to the target.

![](images/200/Twitter34.png)

In this demo, the parameter will use a fixed value which indicates search tweets by a specific
tag.

Click the target directly, a text box will appear to let you input the value. Input name of the
interested tag in the tweets. You should encode the string according to XML standard.

Click **Save** button on the top to apply the change, then click **Close** button to return to
previous dialog.

![](images/200/Twitter35.png)

Another parameter needs to be customized is **result_type**. Use a fixed value “recent” for
this parameter to only retrieve new tweets from user’s Twitter account.

After both parameters are customized, use can view the configuration in the dialog. If
properly configured, click **Exit Mapper** button to save the change.

![](images/200/Twitter36.png)

Now the integration can invoke Twitter to retrieve interested tweets from user’s account.
Next step is to enable writing those tweets to Data Lake in Oracle Storage Cloud. Services from
the Oracle Storage Cloud can be leveraged implement the function.

The integration will first authenticate to the Oracle Storage Cloud to retrieve a security token
for following requests. Select pre-defined Oracle Storage Cloud connection from **INVOKES** pop up
toolbox in the left. Then drag the connection to the position between the Twitter node and the
end node in the flow.

![](images/200/Twitter37.png)

Following dialog will appear to configure the service invocation. The REST service endpoint
at Oracle Storage Cloud is a HTTP service. The authentication process is wrapped in HTTP
communication. Credential information is wrapped in a HTTP GET request, server returns
authentication result in the HTTP response.

![](images/200/Twitter38.png)

Specify the relative URI of the authentication service at the Oracle Storage Cloud, it is
_/auth/v1.0_ in this demo. Select to use GET method to send HTTP request. Customization need to
be enabled for both preparing Request headers and analyzing Response headers.

Click **Next** button to move to following page. The page allows configure HTTP headers that
are specific to the authentication process. Click button to add a new header declaration. A
name must be given in left column and an optional description in right column.

![](images/200/Twitter39.png)

Two headers, **X-Storage-User** and **X-Storage-Pass** , are defined. They wrap username and
password for authentication respectively.

After declaring both request headers, click **Next** button to move to following page. This page
will declare response headers specific to the authentication process.

![](images/200/Twitter40.png)

The response header **X-Auth-Token** is pre-defined to wrap the token if authentication
succeeds.

After declaring the header click **Next** to move to following page. User can check the
configuration in the page. If all configurations are correct, click **Done** button to commit the
configuration.

![](images/200/Twitter41.png)

Next, we will provide value for parameters (request headers) in the request. Select the
invocation node and click button in the pop up toolbox to launch the Mapper dialog.

![](images/200/Twitter42.png)

Click each HTTP header declared previously. In the demo, we will use static value for both
headers. Values for both headers are from Oracle Storage Cloud configuration. Format for 

X-Storage-User is  "Storage-\<identity domain\>:\<login name\>".


![](images/200/Twitter43.png)
![](images/200/Twitter44.png)
![](images/200/Twitter45.png)


After committing the values, click **Exit Mapper** button to return to Integration Designer. Next
action in the integration flow is to write data to Oracle Storage Cloud.

![](images/200/Twitter46.png)

Select the Oracle Storage Cloud connection from the INVOKES toolbox, and drag it between
authentication result node and end node in the flow. Following dialog appears again to configure
REST invocation.

![](images/200/Twitter47.png)


The URI for the data object upload service in Oracle Storage Cloud is in the format:
/v1/Storage-\<Identity Domain\>/\<Container\>/\<Object Name\>. The service leverages HTTP PUT
method to upload the data object. Content of the data object is sent as payload in a HTTP


request. **X-Auth-Token** header must be included in the HTTP request as the authentication proof
to the service.

To enable the integration flow to control data object name at runtime, we use the template
/v1/Storage-\<Identity Domain\>/\<Container\>/{Object Name} for the service URL. The container
must be created in advance before the demo.

Select **PUT** as the request method, and check **Configure a request payload for this endpoint**
to enable payload customization. Also need to enable request header customization in order to
append **X-Auth-Token** header in the request.

Click **Next** button to move to following page. User can add additional query parameters for
the URI.

![](images/200/Twitter48.png)


However, there is no query parameter defined for the service. So simply click **Next** button to
move to the following page.

In the page, user needs to customize format of the payload. First, user need to select type of
the payload. For different payload type, there are different ways to describe the format. For
example, user can select an XSD schema file as format for a XML-based payload. Integration
Platform will parse the format selected in the page to build data object at runtime.

In the demo, payload of the request is in XML format. A XSD schema file has been created to
describe the XML document architecture.


![](images/200/Twitter49.png)

Select XML as type of payload and also upload the XSD schema file. Then click **Next** button
to following page.

![](images/200/Twitter50.png)

Add **X-Auth-Token** as a required HTTP header in the request. The exact value of the header
will map the security token returned from the previous step.


Click **Next** button to the **Summary** page to check your configuration. If everything looks OK,
click **Done** button to commit the invocation.

![](images/200/Twitter51.png)

Next, we will customize mapping for parameters in the invocation. Click invocation node in
the flow and click button in the pop up toolbox to launch following Mapper dialog.

The first parameter is **X-Auth-Token** header in the HTTP request. The value for the request
header should be identical as the token returned from the authentication action.

![](images/200/Twitter52.png)

The result of invocation to authenticate to Oracle Storage Cloud is a source in the left.
Collapse the source to find the custom response header **X-Auth-Token** , and then drag it to the


**X-Auth-Token** header as target in the right. A link is established between the source and target as
below.

![](images/200/Twitter53.png)


Next parameter must be customized is **objectName** in the URI template. It will dominate
name of the data object in Oracle Storage Cloud. Click the parameter to launch following
Mapping dialog.

![](images/200/Twitter54.png)

In the demo, current date will be used as name of the data object. To get value of current
date, we will use pre-defined function in the Integration platform.

Function is a kind of Mapping Component which is defined to return a value. All available
functions can be selected from Mapping Components catalog in the left.

![](images/200/Twitter55.png)

Select **Mapping Components** catalog in the left, locate the **current-date** function from the
_Functions -> Date_ path. Drag the function to the target parameter on the right. Following page
will indicate that the parameter will use the function to retrieve current date as name of the data
object.

```
Click Save action, then click Close button to save the mapping.
```
![](images/200/Twitter56.png)

The last parameter in the invocation is the payload in the request. In the demo, the payload
will be generated from the result retrieved from Twitter previously. The result of that invocation
is a XML document too. So the standard and easiest way is to transform the document into the
payload with a XSL template.

To make the demo simpler, we use same schema for the payload as that for the retrieved
tweets. The XSL template only needs to iterate elements in the source document and generate
elements with same name, with same number in the payload. All child elements are mapped
one-to-one from source to target.

![](images/200/Twitter57.png)

The Mapper Designer supports creating a XSL template interactively. In the schema tree, an
element that can repeat more than once is decorated with an icon ahead. Those elements are
always starting point of the template design. In the demo, we will start from the “ **statuses** ”
element. Click the element in the target schema tree will launch following dialog.

![](images/200/Twitter58.png)

The transform process will iterate corresponding elements in the source document then
generate elements in the target. To enable the iteration process, select the statement in the right,
then click Actions button on the right-top of the dialog. Following menu will pop up.

![](images/200/Twitter59.png)


```
Select Insert Parent from the menu, an empty control is added as the parent.
```
![](images/200/Twitter60.png)

Next, you can add the iteration control to the parent statement. XSL Elements is a kind of
Mapping Component in the tool. You can list available elements within **Mapping Components**
catalog.

![](images/200/Twitter61.png)

The **for-each** element is designed to iterate elements in a XML document. You can find it
under the **XSL Elements** node. Drag and drop it onto the parent. The empty parent will be
replaced by **for-each** element.

![](images/200/Twitter62.png)

The **for-each** element requires a **select** attribute to specify name of the elements in the
source document. User can map value of the attribute with an element in the schema of source
document.

![](images/200/Twitter63.png)

Find the source document schema from the **Source** catalog, and then locate the element
that will be transformed to the target document. In this demo, it is the element with identical
name. Drag and drop the **statuses** element to the **select** attribute under the **for-each** element in
the right.

![](images/200/Twitter64.png)

Click Save action on top of the dialog then click Close button and return to Mapper Designer
page.
Next, we need to map child elements. Collapse the statuses element in the schema tree on
both sides. All child elements are listed so that you can easily establish the map.

![](images/200/Twitter65.png)

The mapping rules used in this demo include:
```
1. Map the elements with identical name between source and target.
2. Only need to map those elements you want them appear in target document.
```

To implement those rules, user can simply drag selected child elements in the source to the
elements with identical name in the target.

![](images/200/Twitter66.png)

When required element mappings are done, click **Save** action to keep your modification safe.
Then click **Exit Mapper** button and return to the Integration Designer.

![](images/200/Twitter67.png)

Now the integration flow is completed. User can further customize tracking for the
integration. Tracking is a mechanism of Oracle Integration Cloud Service to enable administrators
to identify a running integration. Tracking record is composed of information or business
identifier from the running integration.

Click **Tracking** action in the upper right to launch following dialog to customize tracking for
the integration. User can select up to three business identifiers available from the list in the left
as tracking fields. One of them must be marked as primary tracking field.

![](images/200/Twitter68.png)

In this demo, we only rely on the time when the integration was launched to identify a
running integration. Drag the schedule variable **startTime** from the left and drop it into Tracking
Field column in the right, then click **Done** button in the dialog.

![](images/200/Twitter69.png)

Congratulation, you have done all design efforts for the integration. Click **Save** action in the
Integration Designer to save your work then click **Exit Integration** button.

## Step 4: Activate the Integration

The integration is ready to run. In this step, we will demonstrate how to activate an
integration and monitor it after execution.

**4 .1 Activate an integration flow**

In the following page, find the integration we just created. You may notice that it is not
activated yet.

![](images/200/Twitter70.png)


Click button in the right of the integration, a menu as below will pop up. Select **Activate**
item in the menu.

![](images/200/Twitter71.png)

```
Following dialog will appear to let user control how the integration is activated.
```
![](images/200/Twitter72.png)

Click **Activate and Schedule...** button to schedule the integration right now. Following
designer gives user additional control on the integration schedule.

![](images/200/Twitter73.png)

In this demo, we will customize **Frequency** of execution of the integration. From the
drop-down menu you can see that the integration can be scheduled at fine-grained level.

![](images/200/Twitter74.png)

In this demo, select **Hours and Minutes** to schedule the integration repeatedly. Controls in
the dialog as shown below let user customize the schedule.

![](images/200/Twitter75.png)

Increase the **hour(s)** field to 1 to schedule the integration every 1 hour. Click **Save** action in
the upper right, then click **Exit Scheduler**. Following page will display and let user to review the
schedule and decide when to submit the schedule.

![](images/200/Twitter76.png)

```
Click Submit Now button to schedule the integration immediately.
```
**4.2 Track and monitor an integration flow**

After the integration is scheduled, user can track and monitor the integration through Oracle
Integration Cloud Service. All monitoring functions are consolidated in the following monitoring
page. User can go to the page by clicking **Monitoring** link on the top.

The dashboard in the page will give user an overview of the whole Integration Service
instance from workloads to performance. The panel on the left is a quick navigation to different
monitoring functions.

![](images/200/Twitter77.png)

Select **Integrations** from the left panel will show following Integration Monitoring page. In
the page, user can see clearly statistics of execution history of integrations.

![](images/200/Twitter78.png)

Select **Tracking** from the left panel will show following Integration Tracking page. In the page,
user can see every scheduled execution of integrations. You may notice that the tracking fields
you selected for integrations are displayed here. It helps users to uniquely identify an integration
execution.

![](images/200/Twitter79.png)

Click an integration execution in the list will jump to following page. User can view the
progress and state of the integration flow.

![](images/200/Twitter80.png)


