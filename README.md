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

### Step 4. Obtain Webex Teams API Token

In order to send the Webex Teams messages, you have two options:
  - **Option 1 (For tests only):** Use your own Webex Teams API token that will need to be updated manually every 12 hours.
  - **Option 2 (Recommended for production):** Use Webes Teams Bot to send messages.
      - Create Webex Teams Bot following these instructions: [Create a Bot](https://developer.webex.com/docs/bots)
      - Record its API Token
      - Add Bot to the Webex Teams Room so that it can send notifications.

### Step 5. Import Atomic Workflows

SXO workflow is represented by the file in JSON format, that contains definitions and description of all the activities, targets, variables and atomic workflows that are in use. In this step, we will use file import to add these workflows to SecureX orchestration environment.

> **Note:** Refer to documentation for more information about workflow import options: https://ciscosecurity.github.io/sxo-05-security-workflows/importing

1. Save the following workflows included in this reposiroty as json files on your computer: [Threat Response - Update Casebook](https://github.com/oxsannikova/sxo-solarwinds-blogpost-to-incident/blob/main/ThreatResponse-UpdateCasebook__definition_workflow_01KZ9WT3B47KT7c8MSYAvSw1lvTXdYqVSBV/definition_workflow_01KZ9WT3B47KT7c8MSYAvSw1lvTXdYqVSBV.json) and [Sys time to ISO format](https://github.com/oxsannikova/sxo-solarwinds-blogpost-to-incident/blob/main/sys-time-to-iso-format__definition_workflow_01JKYEUJWEVDG4IDBLpUhlliADd4SbrNwv2/definition_workflow_01JKYEUJWEVDG4IDBLpUhlliADd4SbrNwv2.json)
2. In SecureX orchestration left hand-side menu, go to **Workflows** -> **Atomic Actions** -> **Import** -> **Browse** and import the atomic workflows.

### Step 6. Import the main workflow

1. Save the following workflow included in this reposiroty as json files on your computer [talos-solarwinds-blogpost-to-incident](https://github.com/oxsannikova/sxo-solarwinds-blogpost-to-incident/blob/main/talos-solarwinds-blogpost-to-incident__definition_workflow_01KZ8MF3FCJ985zVbgULIwPFrSx9qslb5lx/definition_workflow_01KZ8MF3FCJ985zVbgULIwPFrSx9qslb5lx.json)

2. In SecureX orchestration left hand-side menu, go to Workflows -> My Workflows -> Import -> Browse and import the workflow called [talos-solarwinds-blogpost-to-incident](https://github.com/oxsannikova/sxo-solarwinds-blogpost-to-incident/blob/main/talos-solarwinds-blogpost-to-incident__definition_workflow_01KZ8MF3FCJ985zVbgULIwPFrSx9qslb5lx/definition_workflow_01KZ8MF3FCJ985zVbgULIwPFrSx9qslb5lx.json)

You will be presented with the following warning:

![](/assets/import_warning.png)

Don't get scared and click "Update" :)

4. This is where you will provide your Webex Token:

![](/assets/token_request.png)

Copy your personal Webex Teams API Token or your Webex Teams Bots' API Token into the VALUE field. This is Secure String variable and it will be stored securely in the SXO.

5. You should see the new workflow being added to the list. Click on the workflow when import is complete.

6. If import was successful, you should see zero warnings at the top of the workflow canvas.

![](/assets/inside_workflow.png)

### Step 7. Update local variables

1. You will need to update local variable called **Webex Room Name**. To do so, oepn the workflow editor and click on the variable name in the workflow properies panel on right hand side.

2. Modify the VALUE field to match the name of your Webex Teams Triag Room to receive notifications.

### Step 8. Run the workflow

1. To execute the workflow, click RUN at the right top corner in the action pane.

![](/assets/action_pane.png)

2.  Observe workflow execution.

> As the workflow progresses, you should see activities turning green. Don't be alarmed if some activities turn red, it is expected behavior.

## Notes
Please test this workflow before implementing in a production environment. This is a sample workflow!

## Author(s)
Oxana Sannikova (Cisco)
