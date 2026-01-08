# COMP3010
## Introduction:
In this report, I will be analysing the BOTSv3 dataset within Splunk. The BOTSv3 dataset is a public dataset made up of 2,083,056 events which simulates an incident to allow cyber security professionals to practice event analysis in a simulated environment. By utilising the 3 tiers of SOC – triage, investigation and hunting – I will answer a series of questions to determine how the incident occurred, including information about the user(s) and device(s) involved. This report will focus on 8 of those questions, explaining their relevance to SOC, as well as how to install Splunk and how to prepare the BOTSv3 dataset for analysis.

Screenshots can be found here: https://github.com/Mark7567/COMP3010
Video walkthrough: https://www.youtube.com/watch?v=ijebfZ6ZJcI

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## SOC Roles and Incident Handling Reflection:
### SOC:
The Security Operations Centre (SOC) consists of 3 tiers, each having unique roles and responsibilities surrounding cyber security prevention and analysis. Tier 1 - triage - involves monitoring dashboards and events to determine if an incident has occurred. Since attacks cannot be 100% prevented, tier 1 acts as a way to catch incidents early, as well as filter out false positives which prevention methods may have caught. 

Once an event has been flagged as an incident, tier 2 - investigation - takes place. This involves checking logs and confirming that an incident has occurred and containing them to prevent any more damage from occurring. Tier 2 also involves determining how the incidents occurred by performing an in-depth analysis. 

Lastly, tier 3 - hunting - involves performing an advanced analysis on the incident and improving overall security following it. The BOTSv3 dataset focusses predominantly on tier 2 of SOC, since the dataset contains incidents which have already occurred, with the purpose of the dataset being to confirm this and investigate how they happened.


### Prevention:
Prevention is an incident handling methodology which involves mitigating the risk of an incident occurring rather than directly stopping it, since it is not possible to 100% prevent an attack. Rules and proper system configurations are implemented to make a system as secure as it can be in an attempt to reduce the risk of successful attacks. Prevention relates to the BOTSv3 exercise since the events in the dataset can help to determine normal user behaviour which may make any outliers more obvious as potentially malicious. Furthermore, it links with tier 1 of SOC as there are links with monitoring dashboards and analysing behaviour.


### Detection:
Detection is an incident handling methodology that involves identifying incidents which could be considered suspicious and may indicate an incoming incident. Typical detection methods include analysing network traffic and timestamping user actions or system events to find concerning behaviour. The BOTSv3 dataset involves using filters and searching within Splunk to analyse millions of events and identify information about them, such as which users were involved and which operating system their device was running. This links to tiers 1 and 2 of SOC since detection involves flagging potentially malicious events and analysing them to determine their causes.


### Response:
Response is an incident handling methodology which involves containing an incident to prevent it from causing any more damage to a system, as well as investigating how the incident occurred. The BOTSv3 dataset contains a variety of incidents which need to be confirmed as valid, as well as investigating into how they occurred by gathering information about the events using Splunk filters. Since it is a premade dataset, Splunk cannot contain the incidents in any way, but it can be used to investigate them. Response has strong links with tier 2 of SOC as the purpose of this methodology is to investigate how the incident occurred, which is also the main idea behind SOC tier 2.


### Recovery:
Recovery is an incident handling methodology which involves restoring damaged systems after an incident has been resolved. It also includes improving security to reduce the risk of a similar incident happening in future. While there is no active recovery within the BOTSv3 dataset, it helps with this methodology as the dataset is premade to contain events for analysis which can then be reviewed to prevent further incidents.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Installation and Data Preparation:
This section will explain how Splunk was installed within an Ubuntu Linux virtual machine hosted by VMWare, and how the BOTSv3 dataset was loaded. As I performed the installation before taking screenshots for this section, the screenshots display later timestamps compared to those for the guided questions. To effectively demonstrate the installation of Splunk, I reinstalled it on the same virtual machine ensuring the configuration of the machine remained the same throughout this report. The reason for using a Linux virtual machine is to mimic real world SOC environments which would typically use Linux-based systems. By installing Splunk locally on my device, this allowed me to have full control over the configuration, and which data was ingested, keeping the integrity and accuracy of the analysis. 

### Splunk Installation:
I opened Firefox inside an Ubuntu Linux virtual machine and searched for “splunk enterprise download”, clicking on the first link in the search results. 

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/337d6d21-9235-4e50-8ee9-09b2a250a2b9" />


  
This link took me to the official Splunk website, where I logged into an account which I had already created.

<img width="940" height="530" alt="image" src="https://github.com/user-attachments/assets/1d09d2ba-9c1d-40f5-8043-1b8389e265d5" />



I selected “Copy wget link” for the .tgz version of Splunk, to ensure that all packages were downloaded alongside the main Splunk software. This meant I did not have to individually download all relevant packages to complete this coursework.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/63b6d83f-bd0e-4448-96fd-25c9c9333a89" />



I downloaded Splunk directly from the Linux terminal by pasting the wget link directly into the terminal and running it. I received a confirmation message in the terminal to state that Splunk had been successfully downloaded.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/8ed597fa-93a2-4290-90e8-c08e27ea069b" />



I ran the command “sudo tar xvzf splunk-10.0.2-e2d18b4767e9-linux-amd64.tgz -C /opt” which installed Splunk and all its dependencies into the /opt folder. 

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/8d5dcb09-dac5-40ce-a95e-790d5d0e9e03" />



To start Splunk, I ran the command “sudo ./splunk start” from within the “/opt/splunk/bin” folder. Since this was my first time running Splunk on this installation, I had to include the command “--accept-license” which accepted the user license agreement for Splunk. I had to set a username and password for the administrator account which I could then use to sign in once on localhost:8000.

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/0e52d162-eddf-4f57-b16e-57150d122e9b" />



After setting up the initial login details, Splunk generated the web server on localhost:8000, providing a clickable link to the website to allow access into Splunk.

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/fdc70691-2bbc-4792-a786-4d3a61d730bc" />



Searching for localhost:8000 on Firefox took me to the Splunk enterprise login page. I entered the username and password I created previously.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c3827ef5-0fc3-45c7-be58-0c491df54b17" />


 
I was able to see the dashboard which houses all of the features I used to answer the guided questions, most notably the “Search & Reporting” tab, which will be explained below.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/7d821217-c5c5-492c-b62e-4219b9902457" />



 
### BOTSv3 Dataset Preparation:
I visited the link https://github.com/splunk/botsv3 and clicked on the link under dataset in the table to download BOTSv3 to my virtual machine. 

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/f19322e7-ce2a-4e41-8edf-ba89cd090d2a" />



Clicking on the link downloaded the file botsv3_data_set.tgz onto my virtual machine as shown in the downloads tab on Firefox.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/42e23c9f-b925-4364-8537-30c58db2b571" />



I opened up my file explorer and found the file in the downloads folder where I then extracted it.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/d77bcce0-234b-43db-8210-47b26afdc6a2" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/e5ccd373-f2b3-4d8e-9466-524b8b07fb25" />



To copy the folder to the correct path for Splunk, I entered root mode in the Linux terminal by running the command “sudo su” and entering the password for my virtual machine.

<img width="940" height="530" alt="image" src="https://github.com/user-attachments/assets/d6213350-ab51-40ef-8176-188861cd76a7" />



Once in root mode, I ran the command “cp -r botsv3_data_set /opt/splunk/etc/apps/” to copy the file (botsv3_data_set) into the correct path (/opt/splunk/etc/apps/) to allow it to load into Splunk correctly.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/56612ad2-bd39-48ed-ada7-08064d0cedd8" />



I navigated to the correct path to confirm that the file had been correctly copied.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/dbf9e86b-8c50-4e54-ad7e-2efe66c9e491" />



I started Splunk using the command “./splunk start”. I did not have to include the “sudo” command at the beginning of the line as I was still in root mode.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/beb47ae4-f2ee-4b3f-bdbc-ea8824c151e4" />



I opened Splunk by searching for localhost:8000 on Firefox. I navigated to the Search & Reporting page then applied the filter index=”botsv3”.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/32b5ba47-0d4e-4d85-9817-4ff0d825e301" />



Running the search with the filter index=”botsv3” and setting the time range to filter for all time, I confirmed that the dataset had correctly installed as I had the correct number of 2,083,056 search results. This meant my data was correctly prepared and ready for me to answer the questions. Validating the correct number of events was important to keep data integrity, which is critical in SOC environments since incorrect data could lead to incorrect results.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/fc0172da-3636-49c5-a4b2-2365b5644b8b" />

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Guided Questions:
This section answers some of the 200-level questions relating to BOTSv3, showing a typical real-world SOC workflow, determining an attacker and identifying information surrounding an incident. There are 8 questions total that I will answer, outlining which Splunk filters I used and what my results were.

### Question 1:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/2e9b4ebd-914c-4450-9bdb-d3324dac2bee" />


 
I used the provided hint to filter Splunk by sourcetype=”aws:cloudtrail”. I then searched through the available filters to find anything which could be related to usernames. Here I found the filter for  “userIdentity.username”, which I then applied to show me the 4 usernames; bstoll, btun, splunk_access and web_admin. This links to tier 1 of SOC as I am monitoring the dashboards to find if an incident has occurred by checking which users have access.


### Question 2:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/0ee5e80a-16c6-4b3e-a5c4-c6b7d4c8fedc" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/d4b2e099-65a8-4cb2-a585-0bdccfb2e420" />


  
I kept the same filter as question 1 and searched additionally for *MFA* using the provided hint to find anything relating to multi-factor authentication. I then searched for “mfa” in the additional filters which led me to find the filter userIdentity.sessionContext.attributes.mfaAuthenticated. 


### Question 3:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/bbfec4d8-5727-4b4b-9730-221ac63d06c4" />


 
I changed the filter to be sourcetype=”hardware” using the provided hint, which then showed me the list of hardware being used to connect to the server. Looking into these values, I found the value CPU_TYPE which was listed as the model number E5-2676. 


### Question 4:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c6affbfe-3628-4aaa-b281-980b6b834ef3" />


 
I changed the filter back to sourcetype=”aws:cloudtrail”, and added a filter for eventName=”PutBucketAcl” based on the provided hints. From here, I noticed 2 separate events with different event IDs. I assumed that one event would be the user making the S3 bucket public, and the other event would be the user making the S3 bucket private again. Taking the ID of the newest event, this gave me the answer of ab45689d-69cd-41e7-8705-5350402cf7ac. 


### Question 5:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/4bdb2614-e27d-4d8b-bcd7-25e8f6bddfbf" />


 
I applied the same filters as question 4. From there, I opened the userIdentity field within the relevant event and found that the username was bstoll. 


### Question 6: 

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/f8cdfffd-75bf-4a43-b920-c05a1ceb7b5c" />


 
I applied the same filters as question 4. From there, I opened the requestParameters field within the relevant event and found that the bucketName was frothlywebcode. 


### Question 7:

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/0e016b5b-eec5-4808-a8bb-9395a4008b95" />


 
I changed the filter to sourcetype=”aws:s3:accesslogs” based on the provided hint. Then, knowing that the events in questions 4 to 6 occurred between 2pm and 3pm, I added a filter for date_hour=14 to check specifically between these times. Next, I added another filter for HTTP PUT requests, since the question involved uploading a file to the S3 bucket. I lastly added a filter for *txt* since the question mentioned a text file being uploaded which hinted to me that it would be a .txt file. This led me to find the uploaded text file “OPEN_BUCKET_PLEASE_FIX.txt”. 


### Question 8:
 
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/5f387501-d151-4ac1-ac11-e16a33b8d686" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/964dbfb3-8aea-4748-8ca5-0a7caf17716a" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/8fe21ade-291a-472e-b64c-16b73bf138f6" />


 
I started by filtering for sourcetype=”winhostmon” using the provided hint. I then searched through the filters to find a filter for “operatingsystem” and an additional filter for OS=”Microsoft Windows 10 Enterprise”. This operating system only had 30 uses, which all came from one user – BSTOLL-L. Once I had this user, I then removed my operatingsystem and OS filters, and instead added a filter for host=”BSTOLL-L”. I searched the filters list again for anything relating to FQDN, however  I could not find anything. I instead searched the additional filters for anything relating to “name”, where I found the filter ComputerName which when inspected had the value of BSTOLL-L.froth.ly. 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Conclusion:
This report has demonstrated the real-world application of SOC tiers when analysing the BOTSv3 dataset within Splunk. I have mainly applied tier 2 of SOC, however, have also applied other incident handling methodologies to investigate and identify security incidents within the dataset. Overall, this report has highlighted the importance of real-world SOC operations in identifying and analysing security incidents.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## References:
BOTSv3 GitHub download: https://github.com/splunk/botsv3 

ChatGPT: https://chatgpt.com/ 

Splunk Enterprise download: https://www.splunk.com/en_us/download/splunk-enterprise.html 

SOC roles explanation: https://www.paloaltonetworks.com/cyberpedia/soc-roles-and-responsibilities#:~:text=A%20security%20operations%20center%2C%20or,security%20solutions%2C%20tools%20and%20products. 

NIST incident handling methodology: https://www.nist.gov/cyberframework/getting-started/online-learning/five-functions

