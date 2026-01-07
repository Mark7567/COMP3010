#### COMP3010
## Introduction:
In this report, I will be analysing the BOTSv3 dataset within Splunk. The BOTSv3 dataset is a public dataset made up of 2,083,056 events which simulates an incident to allow cyber security professionals to practice event analysis in a simulated environment. By utilising the 3 tiers of SOC – triage, investigation and hunting – I will answer a series of questions to determine how the incident occurred, including information about the user(s) and device(s) involved. This report will focus on 8 of those questions, explaining their relevance to SOC, as well as how to install Splunk and how to prepare the BOTSv3 dataset for analysis.

Screenshots and a video walkthrough can be found here: https://github.com/Mark7567/COMP3010

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## SOC Roles and Incident Handling Reflection:
# SOC:
The Security Operations Centre (SOC) consists of 3 tiers, each having unique roles and responsibilities surrounding cyber security prevention and analysis. Tier 1 - triage - involves monitoring dashboards and events to determine if an incident has occurred. Since attacks cannot be 100% prevented, tier 1 acts as a way to catch incidents early, as well as filter out false positives which prevention methods may have caught. 

Once an event has been flagged as an incident, tier 2 - investigation - takes place. This involves checking logs and confirming that an incident has occurred and containing them to prevent any more damage from occurring. Tier 2 also involves determining how the incidents occurred by performing an in-depth analysis. 

Lastly, tier 3 - hunting - involves performing an advanced analysis on the incident and improving overall security following it. The BOTSv3 dataset focusses predominantly on tier 2 of SOC, since the dataset contains incidents which have already occurred, with the purpose of the dataset being to confirm this and investigate how they happened.


# Prevention:
Prevention is an incident handling methodology which involves mitigating the risk of an incident occurring rather than directly stopping it, since it is not possible to 100% prevent an attack. Rules and proper system configurations are implemented to make a system as secure as it can be in an attempt to reduce the risk of successful attacks. Prevention relates to the BOTSv3 exercise since the events in the dataset can help to determine normal user behaviour which may make any outliers more obvious as potentially malicious. Furthermore, it links with tier 1 of SOC as there are links with monitoring dashboards and analysing behaviour.


# Detection:
Detection is an incident handling methodology that involves identifying incidents which could be considered suspicious and may indicate an incoming incident. Typical detection methods include analysing network traffic and timestamping user actions or system events to find concerning behaviour. The BOTSv3 dataset involves using filters and searching within Splunk to analyse millions of events and identify information about them, such as which users were involved and which operating system their device was running. This links to tiers 1 and 2 of SOC since detection involves flagging potentially malicious events and analysing them to determine their causes.


# Response:
Response is an incident handling methodology which involves containing an incident to prevent it from causing any more damage to a system, as well as investigating how the incident occurred. The BOTSv3 dataset contains a variety of incidents which need to be confirmed as valid, as well as investigating into how they occurred by gathering information about the events using Splunk filters. Since it is a premade dataset, Splunk cannot contain the incidents in any way, but it can be used to investigate them. Response has strong links with tier 2 of SOC as the purpose of this methodology is to investigate how the incident occurred, which is also the main idea behind SOC tier 2.


# Recovery:
Recovery is an incident handling methodology which involves restoring damaged systems after an incident has been resolved. It also includes improving security to reduce the risk of a similar incident happening in future. While there is no active recovery within the BOTSv3 dataset, it helps with this methodology as the dataset is premade to contain events for analysis which can then be reviewed to prevent further incidents.
