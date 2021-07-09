# UR3-Analytics

Objective: Demonstrate the usage of Thingworx Analytics by using it to determine the weight of an object that a UR3 robot is holding.
In this exercise, you will perform:

1. [Setup](https://github.com/PTC-Education/UR3-Analytics#Setup) - Download and configure files and devices
2. [Data Collection](https://github.com/PTC-Education/UR3-Analytics#Data-Collection) - Collect joint amperage data from the UR3
3. [Modeling](https://github.com/PTC-Education/UR3-Analytics#Modeling) - Create a machine learning model
4. [Deployment](https://github.com/PTC-Education/UR3-Analytics#Deployment) - Perform automated real time predicitons

![map](./images/UR3-Analytics-TWX-Deployment.png)

![robot](./images/UR_singlePos.PNG)

## Setup

<li>Getting Started</li>

To do this exercise, you need:
    <ol>
    <li>Thingworx Kepware installed.</li>
    <li>Access to a Thingworx instance.</li>
    <li>A UR robot</li>
    </ol>
    
Please download the folder, [main](main).



<li>Kepware Configuration</li>

With Kepware installed, open the file called **UR3_kepwareConfig.opf**. This configuration file is setup to communicate with the UR3 but you will need to change a few things:
    <ol>
    <li>The Thingworx Host address.</li>
    <li>The Thingworx port number.</li>
    <li>The application key.</li>
    <li>The device ID or ip address.</li>
    </ol>
    
The Thingworx host address and port is the URL used to reach the server. An example of a URL is shown below.

>http://servername:PORT/Thingworx/Composer

In the case above, the host is **servername** and the port is **PORT**.</br>

<li>Thingworx Composer</li>

Navigate to your Thingworx composer on your browser. Click **Import/Export** and select the file, **UR3-project.twx**. 


Click **Import**.

![import-thingworx](./images/import-thingworx.png)


This file contains the **UR3-analytics** project. Navigate to the project in in composer by searching for it in the search bar.

![search-thingworx](./images/search-thingworx.png)

Confirm that each of the entities shown in the image below are present.

<details>
<summary>Create an Application Key in Thingworx</summary>
<br>

You must create an application key to give the Kepware server authorization to communicate with the Thingworx server. Navigate to your Thingworx composer on your browser.

1. Select New and type 'app' and select **application key**

![Create Appkey](./images/create-key.png)

2. Fill out the app key general information</br>
    A. Name the app key 'UR3-appkey'</br>
    B. Set the project to 'UR3-Analytics'</br>
    C. Under 'User Name Reference', select your own Thingworx username.</br>

![Name Appkey](./images/name-key.png)

3. Set the expiration date for a future date.

![appkey_expiration](./images/set-expirationdate.png)

4. Select **Save** and the application key will appear under **Key ID**. Select the copy button to the right of the **Key ID** to copy it to the clipboard.

![copy-key](./images/copy-key.png)

</details>

Right click **Project** and select **Properties**>**Thingworx**. Input your host address and port number into the **Host** and **Port** fields. Paste your application key into the **application key** field.


Click **Apply** and **OK**.

![Kepware-Thingworx](./images/kepware-thingworx_highlights.png)

On the UR3 teaching pendant, find the ip address of your UR3 by selecting **Hamburger Menu**>**Settings**>**System**>**Network**. Choose **Static Address** as the network method. Choose an ip address and subnet mask which will allow the UR3 to be on the same network as your computer running the Kepware server.

![UR3-network](./images/network_highlights.png)

In the Kepware configuration, Under **Project**>**Connectivity**>**UR_Channel**, Right click **UR3** and select **Properties**>**General**. Enter the ip address into the **ID** field.

![UR3-device](./images/device_ip_highlights.png)

<li>UR Teaching Pendant</li>

Create a new Modbus client by selecting **Installation**>**Fieldbus**>**MODBUS**>**Add MODBUS Unit**. Enter the same ip address into the **IP Address** field. Add the following modbus signals by selecting **Add New Signal**.

|   Type	        |   Address |   Name	        |
|---	            |---	    |---	            |
|   Register Input	|   128	    |   TWX_Weight	    |
|   Register Input	|   129	    |   AnalysisDone    |
|   Register Output	|   130 	|   ObjectWeight    |
|   Register Output	|   131 	|   position	    |
|   Register Output	|   132 	|   SortingDone	    |

![UR3-device](./images/modbus.png)




## Data Collection

<details>
<summary>UR3 Setup</summary>
<br>
  
  <ul>
<li>Setup Modbus profile on teaching pendant</li>
<li>Download UR programs</li>
<li>Get IP address for Kepware</li>
    For this connection to work, you will need to change the IP address of the target device in the Kepware settings to the IP address of your UR3 robot. The IP address of your robot is found on the teaching pendant under **Hamburger menu>Settings>Network**. <br />
</ul>
  
  </details>
<details>
<summary>Thingworx Setup</summary>
<br>
  We will read and send data bewteen the UR3 and Thingworx with Kepware.<br />
  First download the **Remote Thing** file and the **Gateway Thing** file provided below and import it into your Thingworx instance.<br />
  
  > [UR3_thing](https://www.google.com) (Remote Thing)
  > [UR3_gateway](https://www.google.com) (Gateway)
  
  In Thingworx, select **Import/Export** and import the UR3_Thing and the UR3_gateway<br />

Download the Kepware configuration file shown below.<br />
  
  > [UR3_kepwareConfig.opf](https://www.google.com)
  
  
 Inside of Kepware, right click on UR3 and select properties. Under **General>ID**, input the IP address of your UR3.<br />
  
  Create an app key in Thingworx and input the app key into Kepware.<br />
  
  Ensure all thing properties are good quality in Thingworx.<br />
 
  
  </details>
  
  <details>
<summary>Onshape Model data</summary>
<br>
  
  Create a digital twin in Onshape which mirrors the robots positions.
  
  In addition to adding joint data to the model, we will add object distance from base.<br />
  
  </details>

  
  <details>
<summary>Collect Data</summary>
<br>
  
Have 5 different weights on hand for the robot to hold. Weights cannot exceed the max weight specified by the robot.<br />
  
  Run the program called, "weight_training," from UR teaching pendant.<br />
  The teaching pendant will require user input throughout the program. When the program asks to place a weight into the robot gripper, hold the object in between the jaws and press continue on the pendant. The program will wait 1 second and then close the gripper.<br />
  
  It will then perform the movements to generate the data needed to train the machine learning model. 
  
  Run the program with each of the 5 objects.<br />
  
  </details>
  

## Modeling
  <details>
<summary>Export and clean Data</summary>
<br>
  
Export the data into a CSV.<br />
Open the CSV file in Micosoft Excel<br />
Delete bad data<br />
  
  </details>
  
  <details>
<summary>Thingworx Analytics</summary>
<br>
  
Upload data into Thingworx analytics.<br />
Create model using default settings.<br />

  
  </details>
  
  ## Deployment
  
   <details>
<summary>Connect inputs and output to thing properties</summary>
<br>
  
Connect predictions to UR3_thing properties.<br />
  
  </details>
  
  <details>
<summary>Testing</summary>
<br>
  
Run program called, "weight_detection."<br />
Predicted values will appear on teaching pendant and in Thingworx.<br />
Test the model by giving robot unseen weights.<br />
  
  </details>
