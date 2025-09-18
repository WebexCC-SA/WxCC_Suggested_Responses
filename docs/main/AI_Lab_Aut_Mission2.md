---
#icon: material/folder-open-outline
icon: material/medal
---



# Mission 2: Configure Action and create an order.

 **<details><summary>What is Action? <span style="color: orange;">[Optional]</span></summary>**
Action is a task that an AI agent performs by understanding user intents and completes by connecting to external systems.

For more information visit [Webex Documentation](https://help.webex.com/en-us/article/ncs9r37/Webex-AI-Agent-Studio-Administration-guide#concept-template_5ea99e1f-a679-4cf9-8e33-7a4f83d9f66a){:target="_blank"}


</details>
---


## Mission overview
Your mission is to:

Configure an action to collect order details from the customer and send them to a third-party application via APIs.

---

## Build

### Task 1. Create Service and AI Agent Flow in Webex Connect. 

1. From Control Hub, go to **Contact Center** and open up **Webex Connect** Portal. 
    ![Profiles](../graphics/Lab1_AI_Agent/2.9.gif)



2. Create new Service with name **<copy><w class="attendee"></w>_2000_Service</copy>**
    ![Profiles](../graphics/Lab1_AI_Agent/2.10.gif)


3. Click on **Flows** and create new flow with the name ***<copy>Create_Ordedr_Flowers</copy>***
    ![Profiles](../graphics/Lab1_AI_Agent/2.11.gif)

4. From the Integrations list select AI Agent. 
    ![Profiles](../graphics/Lab1_AI_Agent/2.12.gif)

5. For now, save the flow and **Make it live**. We will return to configuring this flow later. Creating it now is necessary to complete configurations in the AI Studio Portal.
    ![Profiles](../graphics/Lab1_AI_Agent/2.13.gif)

### Task 2. Configure Action in the AI Studio.

1. If not logged-in in AI Agent Studio, login to the AI Studio Portal.
    ![Profiles](../graphics/Lab1_AI_Agent/2.14.gif)

2. Select your AI agent with name **<copy><w class="attendee"></w>_2000_AutoAI_Lab</copy>** that we created earlier, go to **Actions**. You will see one Action is already created by default for the Agent Handoff. We will be creating more actions.

    ![Profiles](../graphics/Lab1_AI_Agent/2.17.gif)

3. Click on creat <b>New Action</b>. Configure it with name ***<copy>Create_New_Order</copy>*** and the Action Description ***<copy>Collect order details, delivery address, total and response with the orderNumber once the order is completed.</copy>***. In the Action score select <b>Slot filling and fulfillment</b>.
    ![Profiles](../graphics/Lab1_AI_Agent/2.18.gif)

4. Scroll down and click to create **New input entity**. Fill up the table with the following and then click on **Add**. <br>
Entity Name: ***<copy>address</copy>*** <br>
Entity Typs: <b>string</b> <br>
Description: ***<copy>Collect the customer's delivery address</copy>***<br>
Example: ***<copy>548 Catalina Drive, Cary, NC 27515</copy>*** <br>
Required: <b>Yes</b>
    ![Profiles](../graphics/Lab1_AI_Agent/2.19.gif)

5. By following the same pattern, create an entity that specifies whether the customer requires delivery. <br>
Entity Name: ***<copy>delivery</copy>***<br>
Entity Types: <b>string</b> <br>
Description: ***<copy>Check if the customer needs delivery or not. Event if they want to proceed with order without specifying the delivery details. If the customer wants to confirm the order but didn't specify if they need delivery or not, ask one more time if they need the delivery or not.</copy>***<br>
Example: ***<copy>Yes,No</copy>***<br>
Required: <b>Yes</b>

6. By following the same pattern, create an entity to collect the customer's phone number.<br>
Entity Name: ***<copy>phoneNumber</copy>***<br>
Entity Typs: <b>string</b> <br>
Description: ***<copy>Collect customer's phone number. Before the customer complete the order, ask if they would like to receive confirmation over the SMS. If so, collect the phone number.</copy>***<br>
Example: ***<copy>3477579861</copy>***<br>
Required: <b>Yes</b>

7. By following the same pattern, create an entity to collect the customer's order details.<br>
Entity Name: ***<copy>orderDetails</copy>***<br>
Entity Typs: <b>string</b> <br>
Description: ***<copy>Collect the flowers and bouquets information that customer orders. Make sure to do correct math. If one rose is 20 dollars and the customer would like buy 9 roses then the price should be 180 dollars. Don't use double quotes (") in the generated responses.</copy>***<br>
Example: ***<copy>Romantic Roses standard bouquet and one more bouquet with 9 roses</copy>***<br>
Required: <b>Yes</b>

8. By following the same pattern, create an entity to store the total price information of the order.<br>
Entity Name: ***<copy>orderTotal</copy>***<br>
Entity Typs: <b>string</b> <br>
Description: ***<copy>After the customer inform if they need delivery or not, and confirm that they would like to proceed with completing the order, collect the Total information and assigned it to this slot.</copy>***<br>
Example: ***<copy>150 dollars, 70 dollars</copy>***<br>
Required: <b>Yes</b>

9. By following the same pattern, create an entity to store the order status information.<br>
Entity Name: ***<copy>status</copy>***<br>
Entity Typs: <b>string</b> <br>
Description: ***<copy>Always create it as "new"</copy>***<br>
Example: ***<copy>new</copy>***<br>
Required: <b>Yes</b>

10. At this point you should see 6 created entities. Please double check it. 
    ![Profiles](../graphics/Lab1_AI_Agent/2.61.png)

11. In the Webex Connect Builder Fulfillment select Service: **<copy><w class="attendee"></w>_2000_Service</copy>** and Flow: <b>Create_Order_Flowers</b> Click **Add**
   ![Profiles](../graphics/Lab1_AI_Agent/2.22.gif)

12. Publish the update of your AI Agent. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.23.gif)

### Task 3. Deliver collected order information to Webex Connect for fulfillment.

1. Login to the Webex Connect, go to the Service **<copy><w class="attendee"></w>_2000_Service</copy>** and click on <b>Manage</b> the flow that you have created earlier.
   ![Profiles](../graphics/Lab1_AI_Agent/2.24.gif)

2. Click on **Edit** the flow on the right top. Then double click on the AI Agent event. In the Provide Sample JSON, replace the standard JSON body with the following: 
<br>
    ``` JSON
    {
      "orderDetails": "ID",
      "orderTotal": "Type",
      "delivery": "Type",
      "address": "Type",
      "status": "Type",
      "phoneNumber": "Type"
    }
    ```

3. Then click on **Parse** and **Save** the change.
   ![Profiles](../graphics/Lab1_AI_Agent/2.62.gif)

4. Drag and drop **HTTP Request** node from the left side of the Webex Connect Flow Builder. Connect **AI Agent** block to the **HTTP Request** block. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.27.gif)


5. Open up HTTP Request node and configure it with the following HTTP Request: <br>

    > Method: **POST**
    > <br>
    > Endpoint URL: ***<copy>https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder</copy>***<br>
    > Header: ***<copy>Content-Type</copy>***: ***<copy>application/json</copy>***
    > <br>
    > Body: <br>
    >       ``` JSON
    >       {
    >        "orderDetails": "$(n2.aiAgent.orderDetails)",
    >        "orderTotal": "$(n2.aiAgent.orderTotal)",
    >        "delivery": "$(n2.aiAgent.delivery)",
    >        "address": "$(n2.aiAgent.address)",
    >        "status": "$(n2.aiAgent.status)",
    >        "phoneNumber": "$(n2.aiAgent.phoneNumber)"
    >       }
    >       ```   
    > <br>
    > 
    > Output Variable Type: <b>JSON</b><br>
    > Click on **+Add Variable**<br>
    > Output Variable Name: ***<copy>orderNumber</copy>***<br>
    > Response Entity: ***<copy>Body</copy>***<br>
    > Response Path ***<copy>$.id</copy>***<br>
    > 
    >    ![Profiles](../graphics/Lab1_AI_Agent/2.63.gif)


6. Compare your settings with the screenshot below to make sure you configured the HTTP Request correctly. Make sure you **Save** the changies. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.29.png)


7. Save changies and click on **Make Live**.
   ![Profiles](../graphics/Lab1_AI_Agent/2.32.gif)

### Task 4. Deliver data from Webex Connect to AI studio for the response to the customer. 

1. <span style="color: red;">[Read Only]</span> Once the HTTP request is completed a new object will be created on the third-party application. You can see all objects by using the this link [https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder](https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder){:target="_blank"}. Below you can see the screenshot with all orders information. Currently there are only 2 orders, but by the time of this lab there could be more.
   ![Profiles](../graphics/Lab1_AI_Agent/2.64.png)
Each order/object will contain all the information that we sent from AI Studio but one - id. This key is created automatically once we create the object. The goal of this Task is to send the value of the **id** back to the AI Agent so AI Agent can provide it to the customer while they are still in live contact, like you can see on the picture below.<br>
   ![Profiles](../graphics/Lab1_AI_Agent/2.31.png)

2. <span style="color: red;">[Read Only]</span> When you were configuring HTTP Request in your previous Task, on the bottom of the request you were configuring the Output Variable. This variable will be used to parse the unique order **id** and pass the value to the Output Variable with name **orderNumber**. See the screenshot below. In the next step we will be configuring this orderNumber variable to be sent to Webex AI studio.</br>
   ![Profiles](../graphics/Lab1_AI_Agent/2.65.png)

3. While on your Webex Connect flow, click on **Edit** the flow then click on the **Settings** and on the top select **Flow Outcomes** and expand **Last Execution Status**. In the **Define key-value pairs to be sent to the AI Agent** select **Enter JSON**.
   ![Profiles](../graphics/Lab1_AI_Agent/2.66.gif)

4. We need to add the key-value pair to the existing JSON body. Add the comma after the last pair and insert ***"orderNumber": "$(n3.orderNumber)"***. Make sure there is no comma after the pair that you inserted. Then click on **Save**.
   ![Profiles](../graphics/Lab1_AI_Agent/2.37.png) <br>
   <br>
Also see this change in action below. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.38.gif)

5. Click on **Make Live** to publish the flow. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.67.gif)

### Task 5. Configure SMS confirmation. 

1. If it is not open, navigate to **Webex Connect** portal. Find your Service **<copy><w class="attendee"></w>_2000_Service</copy>**, navigate to the flow and click on **Manage** the flow. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.39.gif)


2. On the right top click on **Edit**. Then from the available Utilities on the left side find the **SMS** and drag and drop the block to the flow. Connect **HTTP Request** node to the **SMS** node. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.68.gif)

3. Double click on the SMS block and configure the following:

     > Destination: ***<copy>$(n2.aiAgent.phoneNumber)</copy>***<br>
     > From Number: ***<copy>12066478712</copy>***<br>
     >Message Type: **Text**<br>
     ><br>
     >Message as below:<br>
     ><br>
     ><b>Here is your order details:<br>
     >orderNumber: "$(n3.orderNumber)"<br>
     >orderDetails: "$(n2.aiAgent.orderDetails)"<br>
     >orderTotal: "$(n2.aiAgent.orderTotal)"<br>
     >delivery: "$(n2.aiAgent.delivery)"<br>
     >address: "$(n2.aiAgent.address)"<br>
     >status: "$(n2.aiAgent.status)"<br>
     >phoneNumber: "$(n2.aiAgent.phoneNumber)"<br></b>
     >
     >
     >
   ![Profiles](../graphics/Lab1_AI_Agent/2.69.gif)

4. Save and Click on **Make Live**. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.70.gif)


### Task 6. Test the order creating and details delivery over SMS. 

1. In the Webex AI Agent Studio, click on preview and order flowers for you friend. 
   ![Profiles](../graphics/Lab1_AI_Agent/2.72.gif)

2. Check if the confirmation SMS was received on your phone. </br>
   ![Profiles](../graphics/Lab1_AI_Agent/2.73.png)

<p style="text-align:center"><strong>Congratulations, you have officially completed this mission! 🎉🎉 </strong></p>