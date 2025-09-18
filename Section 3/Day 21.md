
## What is Threat Hunting?
It is a proactive search for signs of compromise. In threat hunting you already assume that something might already be wrong instead of waiting for an alert to trigger regarding a potentiall malicious activity.

In an alert driven investigation, you react to an activity that has triggered. Threat hunting is a hypothesis driven approach where you ask a question, explore your data, invetigate and try to find evidence that supports or rejects the hypothesis. Threat hunting helps you to:
- Understand your environment better
- Spot weak signals beofre they become major incidents
- Builds the investigative mindset

## Types of hunts
There are 3 main types of hunts.

### Structured hunting
Based on known attacker behaviour. You use known frameworks (like MITRE ATTACK) to form a hypothesis. For example, an attacker might be trying to dummp credentials from LSASS or an attacker might be trying to harvest credentials. So based on our tools and data we will try to prove or disapprove this theory. 

### Unstructured hunting
This is starts with Indicators of compromise (IOCs) like known malicious IPs, Hashes, or domains. Then based on these indicators we ask questions like:
Has this been seen in our environment (for let's say past 90 days)?
Is this IOC related with any process?
Where did the IOC come from (maybe a user clicked on a link in a Phishing email)?
Did anyone interact witht the IOC?

### Situational hunting
In this type of hunting you focus on a specific asset, user or application based on risk. You prioritise hunts around high value targets based on context, for example your company's finance server is critical and requires extra protection.

## How to form a hypothesis
A good hypothesis is specific, testable and focuses on behaviour. Most threat hunts begin with a simple question
- What techniques are attacker using lately?
- What would an attacker do after getting access?

### Example Hypothesis
> PowerShell is rarely used by normal users to download files. If PowerShell has directly launched or spawned by another process, reaching out to external IPs or URLs, this may indicate command and control or malicious download activity.


## Exercise

> Reflect on what kind of hunting feels most useful to you: structured, unstructured, or situational and why?

> Write down two example hypotheses you might want to explore in your test lab

> Review the MITRE ATT&CK framework and pick a few techniques you find interesting.

I think it depends on the context of what type hunt you want to perform.

### Example of unstructured hunting

If you have read an article (or contacted by your Threat Intelligence team) with IOCs regarding an ongoing Phishing campaign that targets users into clicking malicious links in the email and enter their credentials. In this case you will perform a unstructured hunt.

**Hypothesis**:

The threat actor is attempting to steal users' credentials by sending them Phishing emails and baiting them into clicking malicious links.

**Investigation steps**

- Who is the sender?
- Is there one or multiple sender or sender domains?
- Who are the recipients?
- How many recipients have received the Phishing emails from - this sender?
- Has any recipient clicked the malicious links, if so did they - enter their credentials?
- Was this hunt a TruePositive?
- Is this Phishing campaign impacting our company's environment?
- Was there any business impact?

**MITRE ATT&CK Tactics**

[Initial Access](https://attack.mitre.org/tactics/TA0001/)

**MITRE ATT&CK Techniques**

- [Phishing - T1566](https://attack.mitre.org/techniques/T1566/)

### Example of structured hunting

An office document (word, excel, PowerPoint) launching CMD or PowerShell scripts could be an example of structured hunting.

**Hypothesis**

The threat actor may attempt to abuse Office document macros to spawn CMD or PowerShell processes, which could then connect to a command-and-control (C2) server

Normally, Office applications should not launch CMD or PowerShell. If this behavior is observed, it strongly suggests malicious activity which requires an investigation.

**Investigation steps**

- Which user and host are involved in this activity?
- Where did the office document come from (check the source)?
- Is the hash of the document malicious?
- Check parent and child processes, along with command-line arguments, to identify any suspicious flags or files executed by the script.
- Check network activity, were there any unusual connections made by cmd or powershell towards any C2.
- Check the affected device's timeline to look for suspicious activities

**MITRE ATT&CK Tactics**

[Execution](https://attack.mitre.org/techniques/T1059/)

**MITRE ATT&CK Techniques**

- [Command and Scripting Interpreter: PowerShell - T1059.001](https://attack.mitre.org/techniques/T1059/001/)
- [Command and Scripting Interpreter: Windows Command Shell - T1059.003](https://attack.mitre.org/techniques/T1059/003/)
- [User Execution: Malicious Link - T1204.001](https://attack.mitre.org/techniques/T1204/001/)
- [User Execution: Malicious File - T1204.002](https://attack.mitre.org/techniques/T1204/002/)

### Example of situational hunting

The logon attempt either failed or successful to an emergency (break glass) account that is tier 0 (which typically has domain admin or equivalent privileges).

**Hypothesis**

Emergency accounts or break-glass accounts should not be used during normal operations. Any logon attempt (successful or failed) to such an account may indicate unauthorized access attempts, credential misuse, or malicious activity.

**Investigation steps**

- Was the logon attempt successful or failed?
- Which user and host/IP/device initiated the attempt?- Was this logon attempt during an approved break-glass event, or is it unexpected? Verify the activity with Tier-0 team.
- Has this account been used before, or is this the first activity in months/years?
- Check the timeline of the device and account to correlate with other suspicious events.

**MITRE ATT&CK Tactics**

- [Persistence](https://attack.mitre.org/tactics/TA0003/)
- [Privilege Escalation](https://attack.mitre.org/tactics/TA0004/)
- [Credential Access](https://attack.mitre.org/tactics/TA0006/)
- [Defense Evasion](https://attack.mitre.org/tactics/TA0005/)

**MITRE ATT&CK Techniques**

- [Valid Accounts: Domain AccountsValid Accounts: Domain Accounts - T1078.002](https://attack.mitre.org/techniques/T1078/002/)