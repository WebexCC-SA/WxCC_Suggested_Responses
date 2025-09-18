---
#icon: material/folder-open-outline
icon: material/medal
---

### Mission Details

In the previous **Mission 3**, you created intents, entities, and responses to enable the Scripted Agent to understand and respond to order-tracking requests. However, no logic or API calls were configured yet to retrieve the order information. In this mission, you will configure the fulfillment flow to use an API call to retrieve the order status and send it back to the caller.

### Build

#### Task 1. Configure a Custom Event to send data from AI Studio to WxCC Voice Flow. 

1. The fulfillment for Scripted AI Agent currently is done in the WxCC Voice Flow in order to comply with all policies and regulations.

2. Open up **AI Studio** portal go to **Scripts** > **responses** and open up response ***track_order***<span class="copy-static" title="Click to copy!" data-copy-text="track_order"><span class="copy"></span></span>. Go to Voice Channel. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.38.gif) 

3. Add **Custom Event** and configure it with the following: </br>
Event Name: ***order_details***<span class="copy-static" title="Click to copy!" data-copy-text="order_details"><span class="copy"></span></span></br>
Event payload: **{"ordernumber":"${entity.order_number}"}**.</br>
**Save** the updated response. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.39.gif) 

4. Save and Publish your changes. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.54.gif) 

4. Understanding why we need to use a Custom Event for fulfillment: The API call to retrieve the order status can be made from the Voice Flow. By using a Custom Event, we send the order_number entity that the Scripted Agent collects during the call to retrieve the status.
    ![Profiles](../graphics/Lab1_AI_Agent/6.40.png) 


#### Task 2. Make API call from Voice Flow to retrieve the order status. 

1. From [Control Hub](https://admin.webex.com){:target="_blank"}, go to Contact Center click on flows. Open up your flow. If you follow all lab steps the name should be **<span class="attendee-id-container">Autonomous_Scripted_Flow_2000_<span class="attendee-id-placeholder" data-prefix="Autonomous_Scripted_Flow_2000_">Your_Attendee_ID</span><span class="copy" title="Click to copy!"></span></span>**. Or if you have different name, find your flow. Click on it to open the Flow. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.41.gif) 

2. Select **Edit** for the flow, click anywhere on the gray area in the flow, and look for the **Flow Variables** on the right side.
    ![Profiles](../graphics/Lab1_AI_Agent/6.42.gif) 

3. Create 3 empty String Variables with names:</br>
***order_id***<span class="copy-static" title="Click to copy!" data-copy-text="order_id"><span class="copy"></span></span></br>
***MetaData_Scripted_Agent***<span class="copy-static" title="Click to copy!" data-copy-text="MetaData_Scripted_Agent"><span class="copy"></span></span></br>
***order_status***<span class="copy-static" title="Click to copy!" data-copy-text="order_status"><span class="copy"></span></span>
    ![Profiles](../graphics/Lab1_AI_Agent/6.43.gif) 

4. The fulfillment will go over the Handled output. So in your Voice flow, remove the **Disconnect Contact** block and add **SetVariable block**. Connect Handled output to the SetVariable block. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.46.gif) 

5. In the next step, you will assign the flow variable **MetaData_Scripted_Agent**, which we created earlier, with the value of the MetaData from the **VirtualAgentV2** block. This will allow us to decrypt and review the MetaData from the **VirtualAgentV2** block, which could be useful for troubleshooting any issues with the fulfillment flow.</br>

6. Click on the **VirtualAgentV2** block, scroll down to Activity Output Variables, and copy the MetaData variable name. Then, open the **SetVariable** block and configure the **MetaData_Scripted_Agent** variable with the variable value you copied from the VirtualAgentV2 block. Make sure to enclose it in curly brackets.
    ![Profiles](../graphics/Lab1_AI_Agent/6.47.gif) 

7. Add **Parse** node and connect it to **SetVariable** node. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.48.gif) 

8. Configure the **Parse** node with the following:</br>
Input Variable: **MetaData_Scripted_Agent**</br>
Content Type: **JSON**</br>
Output Variable: **order_id** </br>
Path Expression: **$.ordernumber**
    ![Profiles](../graphics/Lab1_AI_Agent/6.49.gif) 

9. Understanding the **Parse** node configuration: The goal of the Parse node is to extract the **order_number** entity received from AI Studio and assign it to the flow variable named **order_id**. This variable will be used later in the API call.
    ![Profiles](../graphics/Lab1_AI_Agent/6.50.png) 

10. Add **HTTPRequest** node and connect it to **parse** node. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.51.gif)

11. Configure the HTTP block with the following:</br>
Use Authenticated Endpoint: **off**</br>
Request URL: **https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder**</br>
Method: **GET**</br>
Queue Parameters: </br>
Key: **id**</br>
Value: **{{order_id}}**</br>
Content Type: **Application/JSON**</br>
Parse Settings:</br>
Content Type: **JSON**</br>
Output Variable: **order_status**</br>
Path Expression: **$[0].status**</br>
    ![Profiles](../graphics/Lab1_AI_Agent/6.52.gif)

12. Add **Disconnect Contact** and connect **HTTPRequest** node to the **Disconnect Contact** node. Validate and Publish the flow. 
    ![Profiles](../graphics/Lab1_AI_Agent/6.53.gif)

13. Please test the call by dialing the number configured with the **Channel** and **Flow**. Select option 2 in the IVR and say, "I want to track my order." Provide the order number that you created earlier. The call will then be disconnected. Open the Debug mode for your flow, find the latest call, and review the logs. You should see the status of your order.
    ![Profiles](../graphics/Lab1_AI_Agent/6.55.gif)

14. In the next **Mission 5** you will configure the flow to return the order status details back to the caller. 

<p style="text-align:center"><strong>Congratulations, you have officially completed this mission! 🎉🎉 </strong></p>