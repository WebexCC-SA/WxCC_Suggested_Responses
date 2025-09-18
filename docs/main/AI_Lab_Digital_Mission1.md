---
#icon: material/folder-open-outline
icon: material/medal
---


## Mission Objective

In this mission, you need to complete web chat configuration tasks, including creating a Chat Asset, linking it to a Channel, and test website.
## Build

### Task 1. Find your Service.
1. Login to Webex Connect Portal.
Go to **Services** and look for the service that you have created earlier. The name should be **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Service">Your_Attendee_ID</span>_2000_Service<span   class="copy" title="Click to copy!"></span></span>**
   ![Profiles](../graphics/Lab1_AI_Agent/4.1.png)

### Task 2. Configure and Register Chat Asset.

1. While on Webex Connect portal, go to ***Assets*** -> ***Apps***, press ***Configure New App*** and select ***Mobile / Web*** option.
   ![Profiles](../graphics/Lab1_AI_Agent/4.2.png)


2.  Input ***Name*** as **Chat_App_<span class="attendee-id-placeholder">Your_Attendee_ID</span>_2000**

3.  Toggle/enable ***Live Chat / In-AppMessaging*** to ***ON*** and choose ***Primary Transport Protocol*** as **`MQTT`** & ***Secondary Transport Protocol*** as **`Web Socket`** then tick ***Use Secured Port*** checkbox and press ***Save*** button.
   ![Profiles](../graphics/Lab1_AI_Agent/4.3.png)
>**Note**: If there is an error that your request cannot be processed, please press ***Save*** button one more time.



4.  Once asset is saved, press ***Register To Webex Engage*** at the top. 
   ![Profiles](../graphics/Lab1_AI_Agent/4.4.png)

5. Choose **<span class="attendee-id-placeholder">Your_Attendee_ID</span>_2000_Service** from the drop-down list and press ***Register*** button.
   ![Profiles](../graphics/Lab1_AI_Agent/4.5.png)

6.  Check and make sure the asset has been succesfully registered to the service and  ***Register To Webex Engage*** button has been greyed out.
   ![Profiles](../graphics/Lab1_AI_Agent/4.6.png)


7.  Return to ***Assets*** -> ***Apps***, find ***ChatAsset***, copy ***App ID***, paste it into the text file and save. We will use it when configuring chat flow later.
   ![Profiles](../graphics/Lab1_AI_Agent/4.7.png)


### Task 3. Create Entry Point for Chat

1. Login to Control Hub and go to Channels and click on **Create Channel**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.8.png)


2.  Input ***Name*** as **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Chat_Channel">Your_Attendee_ID</span>_2000_Chat_Channel<span   class="copy" title="Click to copy!"></span></span>**
   ![Profiles](../graphics/Lab1_AI_Agent/4.9.png)

3. Select **Chat** from the ***Channel Type*** drop-down list. Select **Chat_App_<span class="attendee-id-placeholder">Your_Attendee_ID</span>_2000** as an ***Asset Name***. Set ***Service Level Threshold*** as **`360`** and click on **Save**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.10.png)




### Task 4. Create Queue for Chat

1.  While on the **Control Hub** portal go to Queues and click on **Create a queue**.
   ![Profiles](../graphics/Lab1_AI_Agent/4.11.png)



2. Input ***Name*** as **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Chat_Queue">Your_Attendee_ID</span>_2000_Chat_Queue<span   class="copy" title="Click to copy!"></span></span>**. Also select **`Chat`** in the ***Channel Type*** section.
   ![Profiles](../graphics/Lab1_AI_Agent/4.12.png)

3. Scroll down to **Chat Distribution** click on ***Add Group*** and select **<span class="attendee-id-container"><span class="attendee-id-placeholder" data-suffix="_2000_Team">Your_Attendee_ID</span>_2000_Team<span   class="copy" title="Click to copy!"></span></span>**
   ![Profiles](../graphics/Lab1_AI_Agent/4.13.gif)

4. Set ***Service Level Threshold*** as **`7200`** seconds (2 hours). Set ***Maximum Time in Queue*** as **`10800`** seconds (3 hours). Click on ***Save*** after comparing your values with the screenshot below.
   ![Profiles](../graphics/Lab1_AI_Agent/4.14.png)


### Task 5. Website Widget Configuration

1.  Login to Webex Engage Portal.
   ![Profiles](../graphics/Lab1_AI_Agent/4.15.gif)


2.  Go to ***Assets*** -> search and edit **Chat_App_<span class="attendee-id-placeholder">Your_Attendee_ID</span>_2000** which you have created in Connect Portal.
   ![Profiles](../graphics/Lab1_AI_Agent/4.16.gif)


3. Scroll down and click on ***Save Changes*** button.
   ![Profiles](../graphics/Lab1_AI_Agent/4.17.gif)

4.  Scroll to top of the page and choose ***Websites*** tab. Click on ***ADD Website***.
   ![Profiles](../graphics/Lab1_AI_Agent/4.18.gif)


5.  Fill in the respective fields as per the table below:

    | **Parameter Name**                | **Parameter Value**            |
    | ----------------------------- | -------------------------- |
    | Chat Widget Language          | English-US                 |
    | Display Name                  | Flower Shop                |
    | Byline Text                   |                            |
    | Button Text                   | Start Chat                 |
    | First message                 | Hello! Welcome to the chat |
    | PCI Compliance Banner Message | This chat is PCI compliant |
    | Domain                        | *.glitch.me                |
    | Set wait time                 | Disabled                   |
    | Set Chat Announcement         | Enabled                    | 


6. Review the configurations and **Save changes**
   ![Profiles](../graphics/Lab1_AI_Agent/4.19.gif)


7.  Scroll up, select ***Appearance*** and change the settings:
	- \[Optional\] Widget Color
	- \[Optional\] Widget Button Type
	- \[Optional\[ Logo
	- Enable Emojis
	- Enable Attachments
  Press ***Save changes*** button at the bottom of the page.
     ![Profiles](../graphics/Lab1_AI_Agent/4.20.gif)


 
8.  Scroll up, select ***Widget Visibility*** tab and make sure that ***Force Turn Off Widget*** switch is disabled.  Then select ***Widget Visibility*** as ***Show without any restrictions*** and save changes.
     ![Profiles](../graphics/Lab1_AI_Agent/4.21.gif)



9.  Now click on ***<*** arrow near ***Website Settings*** and go-back to edit your chat asset.
     ![Profiles](../graphics/Lab1_AI_Agent/4.22.gif)



10. Select ***Installation*** then click on ***Copy*** to copy the chat script to clipboard.
     ![Profiles](../graphics/Lab1_AI_Agent/4.23.gif)


### Task 6. Paste the script to the test website. 

1. In this lab, we are using the glitch.com platform to test our chat functionality on a sample website. Using your personal gmail plesae login to glitch.com and create your own custom website where you can embed the chat widget. Open index.html file to see the structure of the website. 
     ![Profiles](../graphics/Lab1_AI_Agent/4.45.gif)

2. While having index.html file open, copy the script that you have save in notepad in the prevouse Task and paste it between ***footer*** and ***body*** tags. 
     ![Profiles](../graphics/Lab1_AI_Agent/4.25.gif)

4. Click on the website preview, and you should see the chat bubble appear in the bottom-right corner.
     ![Profiles](../graphics/Lab1_AI_Agent/4.26.gif)

<p style="text-align:center"><strong>Congratulations, you have officially completed this mission! 🎉🎉 </strong></p>


