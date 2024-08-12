# SIEM-Project
Creating a home lab using Elastic SIEM and a Kali VM.

# Overview

In this guide, we set up a home lab environment using Elastic SIEM and a Kali Linux virtual machine (VM). Here’s what we accomplished:

 - Data Forwarding: We configured the Elastic Beats agent on the Kali VM to send data to the Elastic SIEM.

 - Event Generation: We used Nmap on the Kali VM to generate security events.

 - Log Analysis: We queried and analyzed these logs within the Elastic SIEM using its web interface.

 - Dashboard Creation: We developed a dashboard to visualize security events for better understanding and monitoring.

 - Alert Setup: Finally, we created an alert within the SIEM to detect and notify us of specific security events.

# Purpose

This home lab serves as a practical environment for learning and honing the skills required for effective security monitoring and incident response using Elastic SIEM. By working through these steps, you will gain hands-on experience with using a Security Information and Event Management (SIEM) system, enhancing your security monitoring capabilities. This knowledge is essential for becoming a proficient security analyst or engineer.


# Step 1. : 
Log in to your Elastic SIEM instance and go to the Integrations page. You can do this by clicking the main menu bar at the top left of the Kibana interface and then selecting "Integrations" at the bottom.

![image](https://github.com/user-attachments/assets/118844ca-1aa2-4f78-920b-54b489311569)

# Step 2:
Search for “Elastic Defend” and click on it to open the integration page.

![image](https://github.com/user-attachments/assets/6f999ef1-96df-4aa2-b790-92b638271dc1)

# Step 3:  
Click on “Install Elastic Defend” and follow the instructions provided on the integration page to install the agent on your Kali VM.

![image](https://github.com/user-attachments/assets/6a3f23a7-7847-405d-a84a-5991a0b11ae6)

Install and copy the Linux Tar.

![image](https://github.com/user-attachments/assets/09bbf6bd-3d7c-4128-b519-a3a519d3f3a0)

Paste that command into the Kali terminal (command line).

![image](https://github.com/user-attachments/assets/ae33ce30-d7f0-4c07-9feb-3d7237cfea44)

# Step 4:  
Run an nmap scan.

![image](https://github.com/user-attachments/assets/43c3c985-8a3e-4a63-9218-29953bfe52d7)

# Step 5: Querying for Security Events in the Elastic SIEM
Now that we have forwarded data from the Kali VM to the SIEM, we can start querying and analyzing the logs in the SIEM.

Inside your Elastic Deployment, click on the menu icon at the top-left with the three horizontal lines and then click on the “Logs” tab under “Observability” to view the logs from the Kali VM.

![image](https://github.com/user-attachments/assets/f34b9dd4-ddb2-49a1-8a7a-8b29c66ea43a)

Enter a search query in the search bar to filter the logs. For instance, to find logs related to Nmap scans, use the query: event.action:"nmap_scan" or process.args:"sudo".

Click the “Search” button to run the query. Note that there might be a delay before the events appear in the SIEM, so this query may not show results immediately.

The results of your search will be displayed in the table below. To view more details about an event, click the three dots next to it.

![image](https://github.com/user-attachments/assets/d90f4aff-1a17-487f-9f5e-61dfba798117)

![image](https://github.com/user-attachments/assets/f671d9cf-e5ec-4b67-a0cb-4a0ff80c94a9)

By generating and analyzing different types of security events in Elastic SIEM, such as the example above or by creating authentication failures (like entering an incorrect password for a user or attempting SSH logins with the wrong credentials), you can gain a deeper understanding of how security incidents are detected, investigated, and responded to in real-world scenarios.

# Step 6: Create a Dashboard to Visualize the Events
You can also use the visualizations and dashboards in the SIEM app to analyze the logs and identify patterns or anomalies in the data. For example, you can create a simple dashboard that shows a count of security events over time.

![image](https://github.com/user-attachments/assets/0ec0fd24-04ca-4d8e-b652-ea4ae24cd1d4)

Click on the “Create dashboard” button on the top right to create a new dashboard.

Click on the “Create Visualization” button to add a new visualization to the dashboard.

Select “Area” or “Line” as the visualization type, depending on your preference. This will create a chart that shows the count of events over time.

![image](https://github.com/user-attachments/assets/b50d771f-a4f9-4e69-bcaa-a976094bd1b9)

In the “Metrics” section of the visualization editor on the right, choose “Count” as the vertical field type and “Timestamp” for the horizontal field. This setup will display the number of events over time.

![image](https://github.com/user-attachments/assets/e02a1160-92fd-49dd-9f46-5015dbe52543)

![image](https://github.com/user-attachments/assets/8b13a601-25de-40bc-8172-12ade2b4ef18)

![image](https://github.com/user-attachments/assets/532f3c28-2360-447e-9974-9f2443af1bf8)

Click on the “Save” button to save the visualization and then complete the rest of the settings.

![image](https://github.com/user-attachments/assets/2d14569b-fee7-439c-b709-f60d07d0d809)

# Step 7: Creating an Alert.

In a SIEM, alerts are an essential feature for detecting security incidents and ensuring a quick response. These alerts are generated based on predefined rules or custom queries and can be configured to initiate specific actions when certain conditions are met. In this task, we will guide you through the steps to create an alert in the Elastic SIEM instance that detects Nmap scans. By following these steps, you will set up an alert that monitors your logs for Nmap scan events and notifies you upon their detection.

![image](https://github.com/user-attachments/assets/fbafd84a-857a-4d50-a9ee-a9b4e0d0ceb8)

3. Click on the “Create new rule” button at the top right.

4. Under the “Define rule” section, select the “Custom query” option from the dropdown menu.

5. Under “Custom query,” set the conditions for the rule. You can use the following query to detect Nmap scan events.

![image](https://github.com/user-attachments/assets/4dfa7956-b870-42b1-9346-f19209116034)

This query will match all events with the action “nmap_scan.” Once you have entered the query, click “Continue.”

In the “About rule” section, provide a name and a description for your rule (e.g., “Nmap Scan Detection”).

Next, set the severity level for the alert to help prioritize alerts based on their importance. Leave the remaining settings under “Schedule rule” at their defaults, and then click “Continue.”

![image](https://github.com/user-attachments/assets/84608ad7-9875-4029-b541-e804837a28d4)

In the “Actions” section, choose the action to be performed when the rule is triggered. You can select to send an email notification, create a Slack message, or activate a custom webhook.

Click the “Create and enable rule” button to finalize and activate the alert.

Once you’ve created the alert, it will monitor your logs for Nmap scan events. If an Nmap scan event is detected, the alert will be triggered and the selected action will be taken. You can view and manage your alerts on the “Alerts” section under “Security.”

![image](https://github.com/user-attachments/assets/049389cf-4655-45cd-80d7-586434b0bbb4)

