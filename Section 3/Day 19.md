# What is Microsoft Intune
It is an enterprise grade platform used to manage and protect endpoints at scale. This is where you can configure an ASR rule.

# Attack Surface Reduction (ASR) Rules

ASR rules are a set of protections that help block suspicious malware behaviour like:
- Office macros spawing Powershell
- Ransomware encryption behaviour
- strange execution patterns
- unusual app behaviors
- Malcious links or files from the internet executing code etc.

These rules are used by organizations to harden their endpoints.

# Enroll an Endpoint into Intune
Following are the steps to join your test user account to a test VM and enable RDP from that user account.

- Navigate to [Microsoft Intune admin center](https://intune.microsoft.com/#home)
- From the sidebar select `Devices -> Device onboarding -> Enrollment`. Under `Enrollment options`, select `Automatic Enrollment`.
![alt text](images/image-12.png)
- Under `MDM user scope` select `All` and click `Save`
![alt text](images/image-13.png)
- RDP into your test Windows VM
- Open `access work or school`, click on `Connect` for `Add a work or school account`. Then select `Join this device to Microsoft Entra ID` and sign in with your test user (`CyberLearner`) account. Going forward this VM is going to be that user's (`CyberLearner`) device.
![alt text](images/image-14.png) </br>
![alt text](images/image-15.png) </br>
![alt text](images/image-16.png) </br>
![alt text](images/image-17.png) </br>
![alt text](images/image-18.png) </br>
![alt text](images/image-19.png)

- Now let's sign in with our `CyberLearner` user account
- Open the RDP app from your host machine, click `Show Options`. Go to `Advanced` tab and enable `Use a web account to sign in to the remote computer`. Do note with this option checked you are no longer able to RDP into the test VM with its public IP address.
![alt text](images/image-20.png)
![alt text](images/image-21.png)
- Head over to your Azure portal, select your VM. Copy computer name under `Overview -> properties`. Now go back to RDP app and replace the IP with copied computer name.
![alt text](images/image-22.png)
- We get another error, because our host machine cannot resolve this hostname  (mydifr-win11-vm) to an IP address. 
![alt text](images/image-23.png)
- To bypass this, lets open our local host DNS settings.
 - Open Notepad with administrative access
 - Open `hosts` file from `C:\Windows\System32\drivers\etc`
 ![alt text](images/image-24.png)
 - Enter the public Ip address of your test VM followed by the computer name and save.
 ![alt text](images/image-25.png)
 - Now go to RDP client and connect. You should get a pop-up allowing you to sigin in with your test account. 
 ![alt text](images/image-26.png) </br>
 ![alt text](images/image-27.png) </br>

- Now in Microsoft Intune admin center select `Devices` and under `Windows` section we should see a device connected.
![alt text](images/image-29.png)
Go to `Endpoint security -> Setup -> Microsoft Defender for Endpoint` and turn the following settings on and save
![alt text](images/image-30.png)
We can see the connection status is enabled and last synchronized date and time
![alt text](images/image-31.png)

Now we can push out policies to our endpoints to automatically onboard onto Microsoft Defender for Endpoint or configure policies for additional protections, which is covered in next section.

# Configure ASR rules in Intune

In above section we enrolled our endpoint into intune. Now lets create an ASR policy in Intune:

- Go to `Endpoint security -> Attack surface reduction` click on `Creat Policy` and select the following example settings:
![alt text](images/image-32.png)
![alt text](images/image-33.png)
![alt text](images/image-34.png)
- These policies can be applied to only groups. You can either select the group from the drop down or create a custom group by clicking on `Groups` in the left side bar.
![alt text](images/image-35.png)
![alt text](images/image-36.png)
- For this example we will select `All devices` group and save the policy
![alt text](images/image-37.png)
- The policy has been created
![alt text](images/image-38.png)
- To determine, if the policy was applied successfuly just click into the policy
![alt text](images/image-48.png)


