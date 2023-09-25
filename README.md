# SDR Lead-Call Analysis
SDR(Sales development representative) Lead-Call Analysis case study

## Table of contents
- [Case study overview](#case-study-overview)
- [Data sources](#data-sources)
- [Tools](#tools)
-  [Data cleaning/Preperation](#data-cleaningpreperation)
-  [Exploratory Data Analysis(EDA)](#exploratory-data-analysiseda)
-  [Result/Findings](#resultfindings)
-  [Dashboard(image)](#dashboardimage)
  
### Case study overview
In this case study, we will follow the steps of the data analysis process: prepare, analyze, share in order to answer the key business questions for an **Telecalling CRM Company**.

### Data sources
 The primary Data source used for this analysis is "SDR_analysis_Dataset" excel workbook with tables about **call logs , leads and an index table for 20 days of  3 SDR's of the  Telecalling CRM company**

###  Tools
- Excel - Clean and transform the data to prepare for analysis
- SQL(BQ) -Conduct descriptive analysis to get the desired metrics from Lead and Call Logs and to Run a few calculations to get a better sense of the data layout and populate the results in Key Metrics Table.
- PowerBI - Creating a dashboard

###  Data cleaning/Preperation
 1. Data loading and Making columns consistent . 
 2. Handling missing values
 3. Cleaning and transforming data to prepare for analysis.

### Exploratory Data Analysis(EDA)

 EDA involves analysis  of the dataset to get the desired metrics from Lead and Call Logs and  Run a few calculations to get a better sense of the data layout and populate the results in Key Metrics Table

 ```
 SELECT contact_number, creation_date, lead_stage, lead_tag, SDR, count(call_attempt_serial) Total_Call_Attempted,
 sum(case when call_connected=true then 1 else 0 end) total_call_connected, 
 sum(case when call_duration_sec_>10 then 1 else 0 end) Effective_Call_Connected,
 sum(case when call_connected=false then 1 else 0 end) total_call_not_connected,

 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'USER_DISCONNECTED' then 1 else 0 end)USER_DISCONNECTED,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'NOT_PICKED' then 1 else 0 end)NOT_PICKED,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'BUSY' then 1 else 0 end)BUSY,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'SWITCH_OFF' then 1 else 0 end)SWITCH_OFF,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'CALL_NOT_CONNECTED' then 1 else 0 end)CALL_NOT_CONNECTED,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'NETWORK_ISSUE' then 1 else 0 end)NETWORK_ISSUE,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'INCOMING_CALLS_NOT_AVAILABLE' then 1 else 0 end)INCOMING_CALLS_NOT_AVAILABLE,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'NUMBER_NOT_IN_USE' then 1 else 0 end)NUMBER_NOT_IN_USE,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected= 'INVALID_NUMBER' then 1 else 0 end)INVALID_NUMBER,
 sum(case when call_connected=false and call_not_connected_reason_if_last_call_not_connected like 'other%' then 1 else 0 end) Other,
 sum(call_duration_sec_)Total_Talk_Time,
 avg(call_duration_sec_)Average_Time_Spent,
 sum(case when lead_stage= 'Discovery pending' then 1 else 0 end)Discovery_pending,
 sum(case when lead_stage= 'Discovery done' then 1 else 0 end)Discovery_done,
 sum(case when lead_stage= 'Demo scheduled' then 1 else 0 end)Demo_scheduled,
 sum(case when lead_stage= 'Demo done' then 1 else 0 end)Demo_done,
 sum(case when lead_stage= 'LOST' then 1 else 0 end)LOST,
 sum(case when call_connected=true and  lead_stage= 'Discovery pending' then 1 else 0 end)cc_Discovery_pending,
 sum(case when call_connected=true  and  lead_stage= 'Discovery done' then 1 else 0 end)cc_Discovery_done,
 sum(case when call_connected=true and  lead_stage= 'Demo scheduled' then 1 else 0 end)cc_Demo_scheduled,
 sum(case when call_connected=true  and  lead_stage= 'Demo done' then 1 else 0 end)cc_Demo_done,
 sum(case when call_connected=true  and  lead_stage= 'LOST' then 1 else 0 end)cc_LOST,
 sum(case when call_connected=true  and  lead_stage= 'Demo done' then call_duration_sec_ else 0 end)cc_Demo_done_total_time,
 sum(case when call_connected=true  and  lead_stage= 'LOST' then call_duration_sec_ else 0 end)cc_LOST_total_time,

FROM `project-1-trail-131997.Neodove.Call_logs`
--where contact_number=9361728473
group by contact_number, creation_date, lead_stage, lead_tag, SDR
```
### Result/Findings
1. The 3 SDR's(Ayesha ,Bhavana, Rakesh) have reached out to 769 leads in 20 days.
2. Out of the 3 SDR's Ayesha had made bulk of the calling (724 calls i.e.,42.5% of the total calls of the 3 ) 
3. Rakesh has least number of lead losts.
4. Most of the leads are in lead stage of Discovery pending.
5. Average time per connected call is 111.18 seconds(1.8 minutes)

###  Dashboard(image)  

### Limitations
 This dataset has/had lot of blanks and had been replaced with NA .


