---
#icon: material/folder-open-outline
icon: material/medal
---


# Mission 2: Configure Fulfillment.



## Mission overview
Your mission is to:

Configure the fulfillment flow to track the status of existing orders. This functionality will allow the system to track the status of an order after the customer provides the order number, so the agent does not have to do any manual work and can simply deliver the order status to the customer. 

---

## Build

### Task 1. Create flow in Webex Connect. 

1. From the Control Hub login to Webex Connect.
    ![Profiles](../graphics/Lab1_AI_Agent/9.16.png)


2. Navigate to the Service that you have created in the previous lab - **<copy><w class="attendee"></w>_Service</copy>**
    ![Profiles](../graphics/Lab1_AI_Agent/9.17.gif)

3. Creat new flow. Name it **<copy>Track_Order_Flowers</copy>**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.18.gif)

4. Select **Integration** as **AI Agent**. Parse the values in the AI Agent block and **Make Live** the flow. We will configure it in a later Task. For now, we just need to create the flow that will be used to complete the Action Configuration on the AI Studio side.
    ![Profiles](../graphics/Lab1_AI_Agent/9.19.gif)

### Task 2. Configure Action in AI Studio portal. 

1. Go to the **AI Studio** portal. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.20.png)

2. Select AI Dashboard and find the **Skill** that you created earlier - **<copy><w class="attendee"></w>_Suggested_Responses_Skill</copy>**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.21.gif)

3. Select **Actions** and create new Action. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.22.gif)

4. Name the Action as **<copy>track_order</copy>**. <br>
<br>
 In the **Action description** provide the following: **<copy>If the customer want to track and order, collect the order number. With the order number execute the fulfillment and return the customer the order status. </copy>**. <br>
 <br>
  Select the **Action scope** as **Slot filling and fulfillment.** 
    ![Profiles](../graphics/Lab1_AI_Agent/9.23.png)

5. Add **New input entity**. Configure it with the following: <br>
Name: **<copy>orderNumber</copy>**. <br>
Entity type: **String**. <br>
Entiry description: **<copy>If the customer wants to track an order, collect the order number to this entity. </copy>**. <br>
Entity example: **<copy>17</copy>**. <br>
Required: **Yes**
    ![Profiles](../graphics/Lab1_AI_Agent/9.24.png)

6. For the fulfillment flow select the Service **<copy><w class="attendee"></w>_Service</copy>** and the flow **<copy>Track_Order_Flowers</copy>**, that you have created in the previous Tasks. Then click **Add**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.25.png)

7. Publish the recent changies of the Skill. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.26.png)

### Task 3. Configure Fulfillment flow in Webex Connect. 

1. Open up Webex Connect. Findthe service **<w class="attendee"></w>_Service** and open up flow: **Track_Order_Flowers**. Click on **Edit** the flow. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.27.gif)

2. Add **HTTP Request** node to the flow and connect **Configure AI Agent Event** node to this **HTTP Reqeust** node. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.28.gif)

3. Open up **Configure AI Agent Event** node and replace the Sample JSON body with the following. Then click on **Parse** and **Save** the changies of the node. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.29.gif)

    ``` JSON
    {
      "orderNumber": "numbr"
    }
    ```

4. Open up **HTTP Request** node and configure it with the following:

    > Method: **GET**
    > <br>
    > Endpoint URL: ***<copy>https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder?id=$(n2.aiAgent.orderNumber)</copy>***<br>
    > Header: ***<copy>Content-Type</copy>***: ***<copy>application/json</copy>*** 
    > <br>
    > 
    > Output Variable Type: <b>JSON</b><br>
    > Click on **+Add Variable**<br>
    > Output Variable Name: ***<copy>orderStatus</copy>***<br>
    > Response Entity: ***<copy>Body</copy>***<br>
    > Response Path ***<copy>$[0].status</copy>***<br>
    > 
    >    ![Profiles](../graphics/Lab1_AI_Agent/9.30.png)

5. Save changies and click on **Make Live**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.31.gif)

### Task 4. Deliver data from Webex Connect to AI studio for the response to the customer. 

1. While on your Webex Connect flow, click on **Edit** the flow then click on the **Settings** and on the top select **Flow Outcomes** and expand **Last Execution Status**. In the **Define key-value pairs to be sent to the AI Agent** select **Enter JSON**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.32.gif)

2.  You need to add the key-value pair to the existing JSON body. Add the comma after the last pair and insert **"orderStatus": "$(n3.orderStatus)"**. Make sure there is no comma after the pair that you inserted. Then click on **Save**. Then click on **Make Live** option to publish the flow. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.33.gif)

### Task 5. Test the Suggested Responses feature with fulfillment. 

1. Login to **Agent Deskop**.

2. Please the call to the number that is related to you Channel - <w class="attendee"></w>_2000_Channel

3. Ask the AI Agent to transfer the call to the human agent. 

4. Once the call is connected to the Agent Desktop, select the AI widgit and then click on Get suggestions. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.34.png)

5. As the caller say that you would like to track an order. You will see the suggestion will come up to ask for the order number. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.35.png)

6. As the caller, provide your order number, and you should see the AI execute the fulfillment to place an API call to the third-party application to retrieve the response. For this lab, all order statuses are "new," so you should see that the AI responds that the order status is "new."
    ![Profiles](../graphics/Lab1_AI_Agent/9.36.png)

7. (Optional) To see all order infomations you can by placing this URL in your browser. <br>
https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder  <br>
    ![Profiles](../graphics/Lab1_AI_Agent/9.37.png)



