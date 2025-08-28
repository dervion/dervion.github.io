---
layout: post
title: "My Cyber Lab Setup"
date: 2025-08-25
---

To setup my test labs, I registered to Digital Ocean and Oracle Free Cloud Tier.

1. I deployed 2 virtual machines(VMs) of Ubuntu.

1a. I deployed 1 via Digital Ocean.
1b. I deployed 1 via Oracle Free Cloud Tier.

2. I installed Datadog agents and verified metrics.

2a. I generated an API key for Digital Ocean and Oracle Ubuntu VMs.

For Digital Ocean it's straightforward to navigate. 
I launched the console via the website and entered the commands to install Datadog agent into the VM.

DD_API_KEY=xx bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script.sh)"

sudo datadog-agent status

I had an issue with entering the Datadog API key as I was trying to install the Application Key instead.
I verified this time that the API key is valid:

curl -s -X GET "https://api.us5.datadoghq.com/api/v1/validate?api_key=xx"

I encountered some issue due to region difference of my Datadog account to the code that I was using so I had to troubleshoot first installing it.

Then edited the old API key and installed the region:

sudo nano /etc/datadog-agent/datadog.yaml

api_key: xx
site: us5.datadoghq.com

I restarted the agent:
sudo systemctl restart datadog-agent

Then ran again:

sudo datadog-agent status

This time it was valid API.

I managed to verify that the agent is working when I checked the Datadog host map.

For Oracle:
I launched my terminal.
Then ran:

ssh -i /location/privatekey ubuntu@IPxx

The site was important as without it, errors might be encountered. This was missing when I was doing this in Digitalocean VM.
DD_API_KEY=xx DD_SITE="us5.datadoghq.com" bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script.sh)"

sudo datadog-agent status

Then I verified the Datadog agent is installed via host map again. It take 3-5 minutes for it to show up.
