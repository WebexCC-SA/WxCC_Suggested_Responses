---
#icon: material/folder-open-outline
icon: material/medal
---


# Mission 1: Configure Suggested Responses with Knowledgebase.



## Mission overview
Your mission is to:

Create a Knowledge Base for the AI Assistant skill to use. This knowledge base will contain document will provide the necessary information for the AI Assistant to knowledgeably provide suggestions to the agent.

---

## Build

### Task 1. Create Knowledgebase. 

1. From Control Hub, go to Contact Center and open **Webex AI Agent Studio** portal.
    ![Profiles](../graphics/Lab1_AI_Agent/9.1.png)

2. Select **Knowledge** and click on **Create Knowledge base**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.2.png)

3. Provide the name as <copy><w class="attendee"></w>_Suggested_Responses_Knowledge</copy> and click on **Create**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.3.png)

4. Add **Flower_Catalog** file. The same file that you used for the Autonomous AI Agent lab.
    ![Profiles](../graphics/Lab1_AI_Agent/9.4.png)

5. Process the file. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.5.png)

### Task 2. Creat AI Assistant skills.

1. Select **AI Dashboard** and click on **Creat skills**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.6.png)

2. Select **Start from scretch** and click **Next**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.7.gif)

3. Name the skill as <copy><w class="attendee"></w>_Suggested_Responses_Skill</copy>. Discribe the goals as **<copy>Answer question about flower suggestion, flower availability, prices, delivery cost and order status.</copy>**. And then click on **Creat**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.8.png)

4. Link the knowledge base to the skill in the **Knowledge** section. **Save** and **Publish** the changies. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.9.gif)

### Task 3. Assigned AI skills to your queue.  

1. In the Webex Control Hub, go to Contact Center, scroll down until you see the **AI Assistant** module. Open it and scroll down to the **Suggested Responses** feature. Click on Assign AI Assistant skills. In the following window, select the skill that you created in the previous tab, <copy><w class="attendee"></w>_Suggested_Responses_Skill</copy>, and add your queue <copy><w class="attendee"></w>_2000_Voice_Queue</copy>. Then click **Save**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.10.gif)

### Task 4. Add "Start Media Stream" block to the voice flow. 

1. In the Webex Control hub find and open your flow, **<copy>AutonomousAI_Flow_2000_<w class="attendee"></w></copy>**.
    ![Profiles](../graphics/Lab1_AI_Agent/9.11.gif)

2. Click on **Edit** and select **Event Flows**. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.12.gif)

3. Drag and drop **Start Media Stream** block and connect **AgentAnswered** block to the **Start Media Stream** block. Drag and drop **End Flow** node and connect **Start Media Stream** block to the **End Flow** block. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.13.gif)

4. (Optional) You can adjust your links layout using the Curved Links option. 
    ![Profiles](../graphics/Lab1_AI_Agent/9.14.png)

### Task 5. Test Suggested Respondes Feature.

1. Log in to the Agent Desktop. If you were previously logged in, the suggestion is to re-login, as we did a lot of configurations related to the Queue and the Team.
    ![Profiles](../graphics/Lab1_AI_Agent/9.15.png)


2. end the call to the number that is related to your <copy><w class="attendee"></w>_2000_Channel</copy>.  Once you connect to the AI agent, ask to speak to a human agent.

3. Once the call is connected to your Agent Desktop, click on the AI Assistance module. You will see the option **Get Suggestion**. Click on it and try to order some flowers. You should see that the AI Agent will suggest flower availability and prices to the human agent based on the Knowledge Base.
    ![Profiles](../graphics/Lab1_AI_Agent/9.14.gif)