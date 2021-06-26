# UR3-Analytics

Objective: Demonstrate the usage of Thingworx Analytics by using it to determine the weight of an object that a UR3 robot is holding.
In this exercise, you will perform:
<ul>
<li>Setup - Dowload and configure files and devices</li>[Overview](https://github.com/PTC-Education/UR3-Analytics#Setup)
<li>Data Collection - Collect joint amperage data from the UR3</li>
<li>Modeling - Create a machine learning model</li>
<li>Deployment - Perform automated real time predicitons</li>
</ul>

## Setup
<li>UR Teaching Pendant</li>
Find ip address
Set up modbus profile
[screenshots]

<li>Thingworx Composer</li>
import project file

<details>
<summary>Create appkey</summary>
<br>

You must create an application key to give the Kepware server authorization to communicate with the Thingworx server. 
1. Select New and type 'app' and select **application key**

![Create Appkey](./images/create-key.png)

2. Fill out the app key general information</br>
    A. Name the app key 'UR3-appkey'</br>
    B. Set the project to 'UR3-Analytics'</br>
    C. Under 'User Name Reference', select your own Thingworx username.</br>

![Name Appkey](./images/name-key.png)

3. Set the expiration date for a future date.

![appkey_expiration](./images/set-expirationdate.png)

4. Select the button to copy the app kay to the clipboard.

![copy-key](./images/copy-key.png)



</details>

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
