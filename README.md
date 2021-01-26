# TALOS - SOLARWINDS BLOG POST TO SECUREX CASEBOOK & INCIDENT
This workflow is an example of how we can use Cisco SecureX and other tools to address SolarWinds and future security threats using SecureX orchestration.

## Features

This workflow takes a Talos blog post, conducts an investigation into it using Cisco Threat Response, and then puts the results in a casebook. If targets are found, an incident is created. If a Webex Teams room name and bot token are provided, a message with the investigation's results will be sent.

## Required Targets

* Target Group: Default TargetGroup
* Targets Used: CTR_For_Access_Token, CTR_API, Private_CTIA_Target, Webex Teams

## Required Account Keys
* CTR_Credentials
* Webex Teams Token

## Required Global Variables
* SolarWinds Casebook ID

## Required Atomic Workflows
* Sys Time in ISO Format (published in this repo)
* Threat Response - Update Casebook (published in this repo)

## Setup instructions

### Step 1. Browse to your SecureX orchestration instance

The URL will be a different depending on the region your account is in:
- US: https://securex-ao.us.security.cisco.com/orch-ui/workflows/
- EU: https://securex-ao.eu.security.cisco.com/orch-ui/workflows/
- APJC: https://securex-ao.apjc.security.cisco.com/orch-ui/workflows/

### Step 2. Setup Targets

> **Note:** **CTR_API**, **CTR_For_Access_Token** and **Webex Teams** are the standard targets that are pre-configured in SecureX orchestration out of the box.

### Step 3. Create Webex Teams Room for notifications

> It is assumed that Webex Teams Room for notifications will be created in advance (see prerequisites section).

Create Teams Room and add all necessary people. SXO will need to know the Room Name in order to send notifications.

### Step 5. Obtain Webex Teams API Token

In order to send the Webex Teams messages, you have two options:
  - **Option 1 (For tests only):** Use your own Webex Teams API token that will need to be updated manually every 12 hours.
  - **Option 2 (Recommended for production):** Use Webes Teams Bot to send messages.
      - Create Webex Teams Bot following these instructions: [Create a Bot](https://developer.webex.com/docs/bots)
      - Record its API Token
      - Add Bot to the Webex Teams Room so that it can send notifications.
