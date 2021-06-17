# UR3-Analytics
An exercie to demonstrate the usage of Thingworx Analytics by using it to determine the weight of an object that a UR3 robot is holding.
In this exercise, you will:
<ul>
<li>Collect joint amperage data from the UR3</li>
<li>Create a machine learning model</li>
<li>Perform automated real time predicitons</li>
<li>Test model with unseen weights</li>
</ul>


<details>
<summary>Data Collection</summary>
<br>
  We will read and send data bewteen the UR3 and Thingworx with Kepware.<br />
  First download the **Remote Thing** file and the **Gateway Thing** file provided below and import it into your Thingworx instance.<br />
  
  > [UR3_thing](https://www.google.com) (Remote Thing)
  > [UR3_gateway](https://www.google.com) (Gateway)
  
  In Thingworx, select **Import/Export** and import the UR3_Thing<br />

Download the Kepware configuration file shown below.<br />
  
  > [UR3_kepwareConfig.opf](https://www.google.com)
  
  For this connection to work, you will need to change the IP address of the target device in the Kepware settings to the IP address of your UR3 robot. The IP address of your robot is found on the teaching pendant under **Hamburger menu>Settings>Network**. <br />
 Inside of Kepware, right click on UR3 and select properties. Under **General>ID**, input the IP address of your UR3.
  
</details>
