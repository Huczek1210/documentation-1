---
title: "Setting Up System Email"
description: "Provides instructions on configuring email using SMTP or GMail OAuth and setting up the email alert service in TrueNAS."
weight: 30
tags:
 - email
 - alerts
keywords:
- enterprise storage solutions
- nas storage solutions
- software storage solutions
aliases:
 - /scale/gettingstarted/scalesystememail/
 - /scale/scaletutorials/toptoolbar/settingupsystememail/
---

An automatic script sends a nightly email to the administrator account containing important information such as disk health.
Configure the system to send these emails to the administrator remote email account for fast awareness and resolution of any critical issues.

{{< hint type=note >}}
[Scrub Task]({{< relref "ScrubTasksSCALE.md" >}}) issues and [S.M.A.R.T. reports]({{< relref "SMARTTestsSCALE.md" >}}) are mailed separately to the address configured in those services.
{{< /hint >}}

## Setting Up User Accounts

Configure the email address for the admin user as part of your initial system setup or by using the procedure below.
You can also configure email addresses for additional user accounts as needed.

### Configuring the Admin User Email Address

Before configuring anything else, set the local administrator email address.
{{< expand "Click here for instructions" "v" >}}
Go to **Credentials > Users**, and click on the admin user row to expand it. Select **Edit** to display the **Edit User** configuration screen.
In the **Email** field, enter a remote email address the system administrator regularly monitors (like *admin@example.com*) and click **Save**.
{{< /expand >}}

### Configuring User Emails

Add a new user as an administrative or non-administrative account and set up email for that user.
Follow the directions in [Configuring the Admin User Email Address](#configuring-the-admin-user-email-address) above for an existing user or see [Managing Users]({{< relref "ManageLocalUsersSCALE.md" >}}) for a new user.

## Setting Up System Email

After setting up the admin email address, you need to set up the send method for the email service.

There are two ways to access email configuration options.
Go to the **System > General Settings** screen and locate the **Email** widget to view the current configuration or click the **Alerts** <span class="iconify" data-icon="mdi:bell"></span> icon in the top right of the UI, then click the gear <span class="iconify" data-icon="mdi:cog"></span> icon, and select **Email** to open the **General Settings** screen.
Click **Settings** on the **Email Widget** to open the **Email Options** configuration screen.

**Send Mail Method** shows three different options:

* [**SMTP**](#configuring-email-using-smtp)
* [**GMail OAuth**](#configuring-email-using-gmail-oauth)
* [**Outlook OAuth**](#configuring-email-using-outlook-oauth)

The configuration options change based on the selected method.

After configuring the send method, click **Send Test Mail** to verify the configured email settings are working.
If the test email fails, verify that the **Email** field is correctly configured for the admin user.
Return to **Credentials > Users** to edit the [admin user](#configuring-the-admin-user-email-address).

**Save** stores the email configuration and closes the **Email Options** screen.

### Configuring Email Using SMTP

To set up SMTP service for the system email send method, you need the outgoing mail server and port number for the email address.

{{< expand "Click here for more information" "v" >}}
Click the **SMTP** radio button.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOptionsSMTP.png" alt="SMTP Email Options" id="SMTP Email Options" >}}

Enter the email address you want to use in **From Email** and the name in **From Name**.
This is the email that sends the alerts and the name that appears before the address.

Enter the SMTP server host name or IP address in **Outgoing Mail Server**.
Enter the SMTP port number in **Mail Server Port**.
Typically, this is 25/465 (secure SMTP) or 587 (submission).

Select the level of security from the **Security** dropdown list.
Options are **Plain (No Encryption)**, **SSL (Implicit TLS)**, or **TLS (STARTTLS)**.

Select **SMTP Authentication** for TrueNAS to reuse authentication credentials from the SMTP server.
Enter the SMTP credentials in the new fields that appear.
Typically, **Username** is the full email address, and **Password** is the password for that account.

Click **Send Test Email** to verify you receive an email.

Click **Save**.
{{< /expand >}}

### Configuring Email Using GMail OAuth

To set up the system email using **Gmail OAuth**, you must log in to your Gmail account through the TrueNAS web UI.

{{< expand "Click here for more information" "v" >}}
Click the **GMail OAuth** radio button.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOptionsGmailOAuth.png" alt="Gmail OAuth Login" id="Gmail OAuth Login" >}}

Click on **Log In To GMail**.

The GMail **Authorization** window opens.

{{< trueimage src="/images/SCALE/SystemSettings/EmailGmailAuthorization.png" alt="Gmail Authorization Screen" id="Gmail Authorization Screen" >}}

Click **Proceed** to open the **Sign in with Google** window.

{{< trueimage src="/images/SCALE/SystemSettings/EmailGmailChooseAccount.png" alt="Choose Account" id="Choose Account" >}}

Select the account to use for authentication or select **Use another account**.

If prompted, enter the Gmail account credentials.
Type in the GMail account to use and click **Next**.
Enter the password for the GMail account you entered.

When the **TrueNAS wants to access your Google Account** window displays, scroll down and click **Allow** to complete the setup or **Cancel** to exit the setup and close the window.

{{< trueimage src="/images/SCALE/SystemSettings/EmailGmailAllow.png" alt="Allow Access" id="Allow Access" >}}

After setting up Gmail OAuth authentication, the **Email Options** screen displays **Gmail credentials have been applied**, and the button changes to **Log In To Gmail Again**.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOptionsGmailOAuthApplied.png" alt="Gmail Credentials Applied" id="Gmail Credentials Applied" >}}

Click **Send Test Email** to verify you receive an email.

Click **Save**.

{{< /expand >}}

### Configuring Email Using Outlook OAuth

To set up the system email using **Outlook OAuth**, log in to your Outlook account through the TrueNAS web UI.

{{< expand "Click here for more information" "v" >}}
Click the **Outlook OAuth** radio button.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOptionsOutlookOAuth.png" alt="Outlook OAuth Login" id="Outlook OAuth Login" >}}

Click **Log In To Outlook**.

The Outlook **Authorization** window opens.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOutlookAuthorization.png" alt="Outlook Authorization Screen" id="Outlook Authorization Screen" >}}

Click **Proceed** to open the **Sign in** window.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOutlookSignIn.png" alt="Outlook Sign In Screen" id="Outlook Sign In Screen" >}}

Enter the email, phone number, or Skype username associated with your Outlook account, then click **Next** to enter your password.

When the **TrueNAS wants to access your Outlook Account** window displays, you can scroll down and click **Allow** to complete the setup or **Cancel** to cancel the setup process.

After setting up Outlook OAuth authentication, the **Email Options** screen displays **Outlook credentials have been applied** and the button changes to **Logged In To Outlook**. Ensure that you populate the **From Email** field with the user account email address to use for the *From* email address.

{{< trueimage src="/images/SCALE/SystemSettings/EmailOptionsOutlookOAuthApplied.png" alt="Outlook Credentials Applied" id="Outlook Credentials Applied" >}}

Click **Send Test Email** to verify you receive an email.

Click **Save**.

{{< /expand >}}

## Setting Up the Email Alert Service

If the system email send method is configured, the admin email receives a system health email every night/morning.

You can also add/configure the **Email Alert Service** to send timely warnings when a system alert hits a warning level that is specified in [**Alert Settings**]({{< relref "/SCALE/SCALEUIReference/toptoolbar/alerts/alertsettingsscreen.md" >}}).

From the **Alerts** <span class="material-icons">notifications</span> panel, select the <span class="material-icons">settings</span> icon and then **Alert Settings**, or go to **System > Alert Settings**.

Locate **Email** under **Alert Services**, select the <span class="material-icons">more_vert</span> icon, and then click **Edit** to open the **Edit Alert Service** screen.

{{< trueimage src="/images/SCALE/SystemSettings/EditAlertServiceEmailScreen.png" alt="Edit Email Alert Service" id="Edit Email Alert Service" >}}

Add the system email address in the **Email Address** field.

Use the **Level** dropdown to adjust the email warning threshold or accept the default **Warning**.

Use **Send Test Alert** to generate a test alert and confirm the email address and alert services work.
