# Simulate a Phishing attack - Method 1
Send a Phishing email from attacker's account

![alt text](images\image-23.png)

![alt text](images\image-24.png)

"You don't often get email from cyberlearner500@gmail.com" indicates that our Anti-Phishing policy is in place.


# Simulate a Phishing attack - Method 2

- Go to Microsoft Defender XDT ->  Email & collaboration -> Attack simulation training -> Simulations
![alt text](images\image-25.png)
- Select a technique you want to simulate on 
![alt text](images\image-26.png)
- Name the simulation
![alt text](images\image-27.png)
- Select pre-built payload or create your own. You can customize how your payload should like like. Also  higher the "Predicted Compromise Rate (%)" is the higher is the likelihood of someone clicking on it. Lets select "# Expense report sharing" payload.
![alt text](images\image-28.png)
![alt text](images\image-29.png)
![alt text](images\image-30.png)
- Select Target users
![alt text](images\image-31.png)
- Exclude users, if you want to
![alt text](images\image-32.png)
- Assign training to users who clicked the link
![alt text](images\image-33.png)
- Select Phish landing page
![alt text](images\image-34.png)
- Select end user notification
![alt text](images\image-35.png)
- Select Launch details and  Submit
![alt text](images\image-36.png)

You can use "Send a test" to check if the configuration is properly in place.
Note: In a production environment always use "Send a test" to make sure it working as expected. 

Now we can see that the simulated Phishing email in our mailbox. 

![alt text](images\image-37.png)

- If the recipient clicks the link, it redirects them to a fake Microsoft credential harvester. After the user has entered their credentials, they are redirected to the Phishing simulation page indicating that they have been Phished or in other words failed the Phishing awareness test. As a result they have received an email to do an awareness training. In a real scenario, if a user enters their credentials this could lead to user account compromise. 

![alt text](images\image-38.png)
![alt text](images\image-39.png)
![alt text](images\image-40.png)

- Now back in Defender XDR, we can see that our Phishing test simulation has started and is in progress. If you click on the simulation, you and see the simulation report details. Since we only have one test user in our tenant, who clicked the link and didn't report it so we have a 100% compromise rate.

![alt text](images\image-41.png)
![alt text](images\image-42.png)

- Under `Users` tab, you can see a list of users the simulation was sent  and the actions they took. For example, Sal got compromised, didn't report the email and didn't start the training yet. When you click on the user itself you can get a step-by-step activity that occurred (e.g. they read the message, clicked message link and supplied credentials).

![alt text](images\image-43.png)
![alt text](images\image-44.png)

You will not see simulated emails under Email & collaboration -> Explorer, but if you want to check whether a user has clicked on a link or not you can check that under the `URL clicks`. This allows you to answer certain questions like:
- Who clicked the link?
- What is the link?
- Which users require instant responsive actions (in case of credential harvesting, the user should change their password) if they have clicked any links?

![alt text](images\image-45.png)