---
title: Setup
---

<a name="toc"></a>
# Setting up your accounts

Below are the steps you'll need to take in order to get your CCR accounts fully activated. 
We ask that you configure your accounts prior to June 30 so the CCR staff can address any issues that may arise prior to their scheduled support break (summer understaffing).
 
You have been provided two accounts (via direct emails from the CCR), which can be a little confusing. 
One is an account that gets you access to the University at Buffalo's VPN network and the other is the account you'll use on CCR's resources 
like the cluster. **In order to connect to our machines, you have to be on the UB network.**  If you're attending the workshop in-person, 
**when on-campus you'll use the Eduroam or UB Guest WiFi network**. Instructions for using these can be found on the university's IT website.
When you're off-campus, you'll use the UB VPN to access UB's network prior to connecting to CCR.

 
## Step 1: Setup two factor authentication for your UB VPN account, following these instructions. 

The username for this account is: itorg\uccr.UBID 

> NOTE: Your username and VPN password will be sent in a separate email. Everywhere you see "UBID" in these instructions, substitute the username provided.

 
## Step 2: Download and install UB's Cisco VPN client. 

[For Windows](http://www.buffalo.edu/ubit/service-guides/software/downloading/windows-software/managing-your-software/anyconnect.html), 
[For MacOS](http://www.buffalo.edu/ubit/service-guides/software/downloading/macintosh-software/managing-mac-software/anyconnect.html) 

You will be receiving a separate email from Globus with the link to download this software. 
If you do not already have a Globus account you will instructed to create one at this point. 
The UB account provided here will not work for the Globus service.

> NOTE: this link is only accessible using the email address this is getting sent to. If you cannot access it, please let CCR staff know.

 
## Step 3: Connect to the CCR VPN – following these instructions.

* When you start the Cisco software the first time you will need to enter the following in the box labeled "Connect to:" `vpn.buffalo.edu` 

* Select CCR from the group drop down menu

* Enter the UB VPN username WITHOUT the itorg in front (e.g. `uccr.UBID` - remember to substitute UBID with you actual username) and password provided. 

* You'll be prompted to ask how you want to received the second factor from Duo.

Now that you have setup the UB account and connected to the VPN, you'll be able to move forward with your CCR account.


## Step 4:  

* Make sure you're connected to the UB VPN and go to [CCR's identity management portal](https://idm.ccr.buffalo.edu),

* Enter your CCR username (e.g. UBID) and click the Next button. 

* Click the "forgot your password?" link to generate a one-time password reset link. The link contained in this email only lasts for 15 minutes.

> NOTE: If you see a "403" or "something bad happened" or a blank page, please clear your browser cache and cookies and restart your browser (or use a different browser).
 

## Step 5: Enable two factor authentication on your CCR account following these instructions. 

Instructions can be found [here](https://docs.ccr.buffalo.edu/en/latest/2fa/)

 
**FINALLY ... Connect to CCR!**


## Step 6: There are two ways to connect to our systems:

Once connected to the UB network, you may login to our front end login machines using:

* a SSH client (server name: vortex.ccr.buffalo.edu)

![](/fig/setup/putty_login.png){:width="720px"}

If you choose to use a SSH client, you may login to our pool of front end servers with the 
address: vortex.ccr.buffalo.edu. You must use SSH keys as we do not accept passwords over SSH. 
We have information about this [here](https://docs.ccr.buffalo.edu/en/latest/hpc/login/)

* or using the [OnDemand web portal](https://ondemand.ccr.buffalo.edu)

![](/fig/setup/ub-ondemand-login.png){:width="720px"}

All documentation for using our systems can be found [here](https://docs.ccr.buffalo.edu)


## Duration of accounts

Your access to both the UB VPN and CCR's resources will be terminated on August 31, 2026.

We provide detailed documentation on our services and recommend you begin with the Getting Started guide.
If you have any questions or problems while using our systems, please do not hesitate to contact us at `ccr-help@buffalo.edu`.

Thank you and welcome to UB CCR!


# Working directories

The key resources are located here: `/projects/academic/cyberwksp21`

You can use the `/projects/academic/cyberwksp21/Students/<your username>` folders for keeping your key data/scripts + your home directory

> Note: you'll need to create that folder yourself

The key software for the workshop is available in the following subfolders: `SOFTWARE`,`SOFTWARE_2026`, and `SOFTWARE_NEW_ENV` further instructions will be provided in 
specific tutorials

It is advisable that your run your larger calculations in the scratch directory: `/vscratch/grp-cyberwksp21/`

> Note: vscratch is a faster-access memory, so the calculations should go faster too, but the content is purged periodically, so make sure to
  save your valuable data before too long


{% include links.md %}
