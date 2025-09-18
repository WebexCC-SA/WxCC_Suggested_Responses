---
#icon: material/folder-open-outline
icon: material/medal
---


## Mission Objective

In this mission, you will download the Webex Connect flow and configure it to work with you Webex AI agent. 

## Build

### Task 1. Create New Webex Connect flow from template. 

1. Download the Webex Connect flow using the following link:
[Webex Connect Flow](https://cisco.box.com/s/w1iqxeeoz2k6abl68lhmhijv9g0jtcy5){:target="_blank"}

2. Go to Webex Connect portal and open your service with the name **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Service">Your_Attendee_ID</span>_2000_Service<span   class="copy" title="Click to copy!"></span></span>**
   ![Profiles](../graphics/Lab1_AI_Agent/4.27.gif)

3. Click on **Flows** and then click on **Create Flow**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.28.gif)

4. Name the flow as **Chat_AI_Agent_<span class="attendee-id-placeholder">Your_Attendee_ID</span>** and select **Upload flow** option from the list.
   ![Profiles](../graphics/Lab1_AI_Agent/4.29.png)

5. Click on **Choose File**, select the fild that you have downloaded in the step 1, then click on **Create**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.30.png)

6. On the following page click on **Save**
   ![Profiles](../graphics/Lab1_AI_Agent/4.31.png)

### Task 2. Configure the Webex Connect Flow. 

1. Open up **Resolve Conversation** block and configure the **Flow Id** with the same that you can find in the URL. Click on **Save**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.32.gif)

2. Open up **AI Agent** block and select from the list the AI Agent that you have created earlier. The name can be **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_AutoAI_Lab">Your_Attendee_ID</span>_2000_AutoAI_Lab<span   class="copy" title="Click to copy!"></span></span>**
   ![Profiles](../graphics/Lab1_AI_Agent/4.33.gif)

3. Open up Queue Task and select the queue **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Chat_Queue">Your_Attendee_ID</span>_2000_Chat_Queue<span   class="copy" title="Click to copy!"></span></span>** from the list that is related to your config. 
   ![Profiles](../graphics/Lab1_AI_Agent/4.34.gif)

4. Open up New Webex Connect Window, go to Applicaitons and find the AppID that is related to your Chat Application with name **Chat_App_<span class="attendee-id-placeholder">Your_Attendee_ID</span>_2000**
   ![Profiles](../graphics/Lab1_AI_Agent/4.35.gif)

5. Go to your Webex Connect Flow, open up **Flow Settings**, click on **Custom Variables** and adjust the appID with the one you copied in the previous step. 
   ![Profiles](../graphics/Lab1_AI_Agent/4.36.gif)

6. For better tracking purposes, also change the **liveChatDomain** in the **Custom Variables** settings from *.glitch.me to the website that is associated with your user account. For example for my test account it is shine-rapid-freesia.glitch.me. For your account please refare the table below. <span style="color: red;">[NEED to Add Table]</span> 
   ![Profiles](../graphics/Lab1_AI_Agent/4.41.gif)


6. Open the first **Receive** node and **Save** it.
   ![Profiles](../graphics/Lab1_AI_Agent/4.37.gif)

7. Open the second **Receive** node and **Save** it.
   ![Profiles](../graphics/Lab1_AI_Agent/4.38.gif)

8. **Save** and **Make Live** the flow. On the following page, select the Chat Application that you have created earlier. The name can be **Chat_AI_Agent_<span class="attendee-id-placeholder">Your_Attendee_ID</span>**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.39.gif)

9. If you noticed any error while making the flow Live, please wait until the flow is published and publish it one more time. 
   ![Profiles](../graphics/Lab1_AI_Agent/4.39.gif)

<p style="text-align:center"><strong>Congratulations, you have officially completed this mission! 🎉🎉 </strong></p>
