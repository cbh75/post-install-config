<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Post-Install Configuration</h1>

This tutorial outlines the post-install configuration of osTicket and is a continuation of [osTicket: Prerequisites and Installation](https://github.com/cbh75/osticket-prereqs).

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11</b> (22H2)

<h2>Configuration Steps</h2>

Login to your osTicket panel using the admin account created in [osTicket: Prerequisites and Installation](https://github.com/cbh75/osticket-prereqs). Once taken to the open tickets page, navigate to **Admin Panel** located in the top right corner of the page.

Once at the Admin Panel, click the **Agents** tab at the top, then click on **Roles**.

![image](https://github.com/cbh75/post-install-config/assets/62080815/55b015e8-d95e-4946-94a9-41d55c9eb979)

At the Roles page, click **Add New Role**, and name the role "Supreme Admin". Navigate to the **Permissions** tab, and check all the boxes under **Tickets**, **Tasks**, and **Knowledgebase**. After all boxes are checked, click **Add Role**. You should see the new Supreme Admin role along with the premade osTicket roles in the Roles list.

![image](https://github.com/cbh75/post-install-config/assets/62080815/53737e08-b712-4671-adc5-0ad3c21e4edc)

Next, navigate to the **Departments** tab, and click on **Add New Department**. Name this new role "System Administrators", and leave the settings at their defaults for now. Click **Create Dept**. The new department we created will be added to the list.

Navigate to the **Teams** tab, click on **Add New Team**, and name it "Level II Support**. osTicket provides us with the Level I Support role already, so there is no need to create that one. In the **Members** tab, add your admin user to this role. Click **Create Team**.

Next, we want to allow anyone to create new tickets. To do this, navigate to the **Settings** tab, then go to **Users**. Under Authentication Settings, make sure the "Require registration and login to create tickets" box is **not** checked, then click **Save Changes**.

![image](https://github.com/cbh75/post-install-config/assets/62080815/c3d6fad6-216b-48cc-9861-532af48857cc)

Now we want to configure some agents. Navigate to the **Agents** tab, then click **Add New Agent**.

Under the Account tab, enter a name, email address, and username for your user.

![image](https://github.com/cbh75/post-install-config/assets/62080815/f77d817a-7bdf-4d15-bc50-9b14d23a77e8)

Once all of that is filled out, click on **Set Password**. Uncheck the "Send the agent a password reset email" box, as we can just set them a password manually. Once you have typed and confirmed their password, be sure to uncheck the "Require password change at next login" box at the bottom, then click **Set**.

![image](https://github.com/cbh75/post-install-config/assets/62080815/9cd328d4-8e5c-4cc5-b7c7-35a1159904f5)

Next, click on the **Access** tab. Here, under Primary Department, set the department to our newly created **System Administrators** account, and set the role to **Supreme Admin**.

![image](https://github.com/cbh75/post-install-config/assets/62080815/c4b4c438-87e9-48c0-8a53-c0e322a12aea)

Under **Teams**, assign the user the **Level II Support** team and then click **Create**. This will create our new agent.

Next, make a second agent using the same steps, except for the **Access** tab, set their department to **Support** and their role to **View only**. We can forget about the Permissions and Teams tabs for this agent, so go ahead and click **Create**.

Once created, we can click on the **Agents** tab again and see both of the users we created, along with the admin user we created during setup.

![image](https://github.com/cbh75/post-install-config/assets/62080815/ceb7755c-fda7-41a1-bc1b-2d2cc589427d)

Next, we will want to create some users. Navigate back to the **Agent Panel in the top-right corner, then click on the **Users** tab, then click **Add User**. In the create user box, type in an email address and name for the user. The email doesn't have to be a real email, so just make one up. Once you have an email and name, click **Add User**.

![image](https://github.com/cbh75/post-install-config/assets/62080815/2b14aaa1-2360-4330-a656-23d3e12cfb66)

You will be taken to the page of your new user, so click on the **Users** tab again and make another user. Once the two users are made, they should both be listed in the User Directory.

![image](https://github.com/cbh75/post-install-config/assets/62080815/80cd69b2-c82b-41e1-b546-f1c480423d0f)

Now that our users are created, we want to manage our SLAs. To do this, go back to the **Admin Panel**, click on the **Manage** tab, then **SLA**.

> SLA stands for Service Level Agreement. These are intended to provide timeframes in which the help desk admin expects tickets to be closed.

On the Service Level Agreements page, click **Add New SLA Plan**. Name the plan "Sev-A", as this will be our highest priority SLA plan. We will use this plan for the most important tickets, such as tickets that could highly disrupt business if left unattended for too long. For the Grace Period, type in **1**. This makes it so that if a ticket in Sev-A is left unattended for longer than one hour, it will be marked as overdue. For Schedule, choose **24/7**. This means that even if Sev-A tickets are created over the weekend, past business hours, or over a holiday, they will still need to be attended to within the hour or they will be marked as overdue. Once these are filled out, click **Add Plan.

![image](https://github.com/cbh75/post-install-config/assets/62080815/bd2b21f5-d36a-404d-85d6-14266515d53c)

Next, create a second SLA plan with the following attributes:

Name: **Sev-B**  
Grace Period: **4**  
Schedule: **24/7**

This SLA is very similar to Sev-A, but gives the IT department four hours to attend to the ticket, instead of just one. This plan will be assigned to tickets that are still high priority, but not quite as important as Sev-A.

Once this SLA is created, create a third plan with these attributes:

Name: **Sev-c**  
Grace Period: **8**  
Schedule: **Monday - Friday 8am-5pm with U.S. Holidays**

As you can see, this plan is much lower priority than Sev-A and Sev-B, as not only is the department given eight hours to service these tickets, they are not required to be serviced outside of business hours.

Once these three SLA plans are configured, navigate back to **SLA**. Here, we will see the three SLA plans we created along with the default SLA created by osTicket.

![image](https://github.com/cbh75/post-install-config/assets/62080815/a4d2b87e-fc26-448b-82a5-717336612b29)

Next, we want to configure our help topics. To do this, navigate to **Help Topics** under the **Manage** tab. osTicket provides some premade topics, but we are going to create a few more. Click on **Add New Help Topic**, and for the topic, type "Business Critical Outage". The rest of the options can be left to their defaults, so click **Add Topic**.

Once this is created, create three more topics with the following topic names:

Personal Computer Issues  
Equipment Reset  
Password Reset

Once all of the topics are created, navigate back to **Help Topics**. Here, all of the topics we created will be listed, along with the ones already provided by osTicket. 

![image](https://github.com/cbh75/post-install-config/assets/62080815/156b180c-423c-4e36-b18b-254f7f9c9656)

And with that, congratulations! You have created most of the core configs that are required to create tickets in osTicket! Feel free to mess around inside of osTicket by creating some new tickets, assigning SLA plans, and logging in with the different users you have made to see what certain users can and cannot do.
