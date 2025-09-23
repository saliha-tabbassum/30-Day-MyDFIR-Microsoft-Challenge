# Conditional Access 

Create a CA policy if the sign-in is coming from a country that we do not do business with. In this case block the access entirely.

- Sign-in with your test user account in Outlook. Once we sign in this will create a sign-in event within Entra ID. This will be used as our legitimate activity. 
- Navigate to [Microsoft Entra admin center](https://entra.microsoft.com/#home). Go to `Monitoring & health -> sign-in logs` and filter on your test user assume this activity to be legitimate from that location and IP.
![alt text](images/image-1.png)
![alt text](images/image-8.png)

## Simulate risky sign-in 
Create a VM in a region different from your test account who logged into Outlook (as above because we will consider that as legit activity). For that purpose we will create a VM in Vultur.

- Navigate to Vultur portal 
- Go to `Compute -> Deploy Server`
- Select `Shared CPU` and the region where you want to create the VM. In this example it is Asia (Singapore) and select VM specs and then click on `Configure Software`
![alt text](images/image-3.png)
![alt text](images/image-4.png)
- Selected Windows Server 2016 and named it as `EvilMyDifr`
![alt text](images/image-5.png)
- In Additional Features, remove automatic backups
![alt text](images/image-6.png)
![alt text](images/image-7.png)
- Click `Deploy`
- Click into the VM and click `View Console` button to check if it has deployed or not
- ![alt text](images/image-2.png)
- Now lets copy the IP address of this VM (`66.42.53.29`) and RDP into it from our host machine.
![alt text](images/image-9.png)
- Downloaded Google Chrome on this VM (reason is that Internet Explorer block lots of content when browsing from a server. To bypass those security controls we need chrome or any other browser)
- Browse to "https://www.whatismyip.com/" to find the public IP of this VM, to make sure it's sourcing from Singapore
![alt text](images/image-10.png)
- Now open Outlook and sign-in as our test user (`CyberLearner`) and it asks us for MFA. So here the assumption is that the attacker has acquired `CyberLearner's` credentials and when the attacker sign-ins, they see the following:
![alt text](images/image-11.png)
![alt text](images/image-12.png)
- In Entra ID we see the event generated based on above malicious sign-in attempt with IP `66.42.53.29` from Singapore and MFA is enabled. We can more information by clicking the events and going through different tabs inside it. For example if you click on Conditional Access, you will see an MFA policy called `Security defaults` applied by default. These are defaults that are enabled for all Entra ID P1 and P2 plans. The control for this policy makes sure that for the sign-in to be successful it must require MFA. When the attacker did not provide MFA, this event became `Interrupted`, hence the Status is `Failure`.
![alt text](images/image-13.png)
![alt text](images/image-14.png)
![alt text](images/image-15.png)
![alt text](images/image-16.png)
![alt text](images/image-17.png)
- Let see if the Sign-in risk was detected in `Risky sign-ins`
![alt text](images/image-18.png)

## Create a Conditional Access policy
Let's create CA policy to block connections from Singapore, as we do not do business with it.

- Go to `ID Protection -> Dashboard -> Protect -> Conditional Access -> Manage -> Named locations -> + Countries location` to create a list of countries to block (in this case Singapore) 
![alt text](images/image-19.png)
- Go to `Conditional Access -> Policies -> New Policy`. But first we have to disable existing `security defaults` 
![alt text](images/image-20.png). In a new tab, go to the `Entra Admin portal -> Entra ID -> Overview -> Properties -> Manage security defaults`
![alt text](images/image-21.png)
![alt text](images/image-22.png)
- Again go back to `Conditional Access -> Policies -> New Policy` and refresh the page, and now we no longer see the warning to disable `security defaults`.
![alt text](images/image-23.png)
- `Name`: Create a new policy `MyDFIR-Sal-CAPolicy`
- `Assignments`: Select the user(s)
![alt text](images/image-24.png)
- `Target resources`: All resources
- `Network`: select the following
![alt text](images/image-25.png)
- `Conditions`: Keep default
- `Access controls` → `Grant` → select `Block access`
![alt text](images/image-26.png)
- `Enable policy`: select `On` and click `Create`
![alt text](images/image-27.png)

On our CA, policy is in place let's try to log in again with our `CyberLearner` account from m our `EvilMyDifr` VM. Now the access is blocked, and we don't see the MFA prompt because it's sourcing from a blocked country
![alt text](images/image-28.png)