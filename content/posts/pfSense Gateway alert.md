+++
title = 'pfSense Gateway Alerts'
date = 2025-08-26T09:46:47+05:30
draft = true
+++

# How to Get Alerts When Your Gateway Changes in pfSense or OPNsense

If you use pfSense or OPNsense, you know how important gateways are—they decide how your internet traffic leaves your network. But sometimes, gateways switch without you noticing. This could be because of:

- Failover in a multi-WAN setup
- ISP issues
- Wrong configuration

### What This Does
I made a small script that checks your gateways and sends an alert if one changes. Out of the box, it sends alerts to Google Chat, but you can easily change it to send to Slack, Telegram, Email, Grafana, or whatever tool you use.

### Steps to Set It Up

#### 1. Get the Script
Download the script [gateway_check.php](https://github.com/rahmanhanan7/Pfsense-GW-change-alert/blob/main/gateway_check.php) from GitHub and upload it to your pfSense or OPNsense box.

#### 2. Upload & Make It Executable
Connect to your firewall with SSH:

```bash
ssh admin@<your-pfsense-ip>
```

Go to the shell, put the script in a folder, then run:

```bash
chmod +x /path/to/gateway_check.php
```

#### 3. Edit the Script
Open the file and update two things:

- Add your Google Chat webhook URL
- Map your gateway IPs (use public IP address) to names, like:

```bash
"192.168.1.1" => "ISP_1"
"10.0.0.1" => "ISP_2"
```

#### 4. Automate with Cron
Install the Cron package in pfSense/OPNsense:

- Go to System → Package Manager → Available Packages
- Install Cron

Then create a cron job that runs the script every minute (or however often you like).

#### 5. Test It
Unplug or disable one WAN connection. You should get a message when the gateway changes.

## Customization
You can make the script send alerts to:

- Email
- Slack
- Telegram

Or any other tool you prefer, and if you want, you can expand it to track other network events too.