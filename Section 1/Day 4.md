Let's connect our first data source to Sentinel and use KQL. For that purpose we will connect `AzureActivity` to Sentinel.

## Enable Azure Activity logs
- In Azure portal, search for `Subscriptions -> select your subscription -> click Activity log -> click Export Activity logs`. </br></br>

![alt text](images/image-14.png)
![alt text](images/image-15.png)
![alt text](images/image-16.png)

-  Click on `+ Add diagnostic setting`, and we can select what kind of logs and destination where they should be ingested in this case we want to send to our LA workspace.</br></br>
![alt text](images/image-17.png)
![alt text](images/image-18.png)


## Connect Azure Activity to Sentinel
- To connect our Azure Activity to our Sentinel instance, got to `Microsoft Sentinel -> Select the correct LA workspace -> Content Management -> Content Hub` (there used to be content here but now its moved to Defender XDR as of August 8,2025). </br></br>
![alt text](images/image-19.png) </br></br>
- In Day 3, we already connected our LA workspace to Defender XDR. Now we to access the content hub, click on the `Microsoft Sentinel` tab within Defender portal and select `Content Management > Content Hub`.</br></br>
- Search for `Azure Activity` and install it. </br></br>
![alt text](images/image-20.png) </br></br>
- If you click on `Manage`, you can see the installed content along with `Azure Activity` data connector that allows us to ingest Azure Activity into Sentinel. 
![alt text](images/image-21.png)
![alt text](images/image-22.png)
- You can use the following KQL provided by Microsoft to track Azure Activity
```
 let Now = now();
        (range TimeGenerated from ago(7d) to Now-1d step 1d
                | extend Count = 0
                | union isfuzzy=true
                (AzureActivity
                | summarize Count = count() by bin_at(TimeGenerated, 1d, Now))
                | summarize Count=max(Count) by bin_at(TimeGenerated, 1d, Now)
                | sort by TimeGenerated
                | project Value = iff(isnull(Count), 0, Count), Time = TimeGenerated, Legend = "AzureActivity") | render timechart 
```
- After some time, you can see the logs in Sentinel
![alt text](images/image-28.png)

### Example KQLs based on AzureActivity

#### Get distinct OperationNameValue for a specific resource group
```
AzureActivity
| where ResourceGroup contains "MYDIFR-SAL-RG"
| distinct OperationNameValue
```

![alt text](images/image-29.png)

#### Get successful workbook write operations
Suppose we want to monitor latest write operations to workbooks

```
AzureActivity
| where TimeGenerated >= ago(30d)
| where ResourceGroup contains "MYDIFR-SAL-RG"
| where ActivityStatusValue == "Success"
| where ActivitySubstatusValue == "OK"
| where OperationNameValue == "MICROSOFT.INSIGHTS/WORKBOOKS/WRITE"
| summarize arg_max(TimeGenerated, *) by _ResourceId
```

![alt text](images/image-30.png)


## Setup Microsoft Sentinel Training Lab
We can install the "Microsoft Sentinel Training Lab" which contains sample events to practice KQL skills on.
- Go to Azure Portal in the search bar type Microsoft Sentinel Training, select and install it. It will take 15–20 minutes to install.
![alt text](images/image-23.png)
![alt text](images/image-24.png)
![alt text](images/image-25.png)
![alt text](images/image-26.png)
- No in Sentinel click on `Logs` and then select Tables icon, and we can see under `Custom Logs` tables were created after the installation of "Microsoft Sentinel Training Lab" 
![alt text](images/image-27.png)

### Get failed login counts for higher than 1000
```
SecurityEvent_CL
| where EventID_s == "4625"
| summarize FailedLoginCount = count() by  Account_s
| where FailedLoginCount > 1000
```
![alt text](images/image-31.png)