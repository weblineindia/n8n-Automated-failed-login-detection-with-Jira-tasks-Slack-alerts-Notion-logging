
# Automated Failed Login Detection with Jira Tasks, Slack Alerts & Notion Logging

This **n8n workflow** monitors failed login attempts from any application, detects repeated failures within a configurable time window, and automates incident response by creating **Jira security tasks**, sending **Slack alerts**, and logging all events in a **Notion database**.

It enables fast, structured response automation for potential account compromise or brute-force attacks.

---

## ⚡ Quick Implementation Steps

1. Import the workflow JSON into your **n8n** instance.
2. Connect your application to the **Failed Login** webhook endpoint.
3. Add **Jira Cloud API credentials**.
4. Add **Slack API credentials**.
5. Add **Notion API credentials** and configure a database for logging attempts.
6. Activate the workflow — it’s ready to run.

---

## 📌 What It Does

This workflow automates failed login monitoring and response by:

* Accepting **POST** requests containing failed login data (username, IP, timestamp, error).
* Normalizing input for consistent processing.
* Validating required fields (`username`, `IP`) and notifying Slack if missing.
* Detecting multiple attempts within a **sliding time window** (default: 5 minutes).
* Creating **Jira Security issues** for single or repeated login failures.
* Sending **Slack alerts** with detailed incident context.
* Logging all attempts in a **Notion database** for auditing and analysis.

---

## 👥 Who’s It For

This workflow is ideal for:

* Security teams monitoring authentication events
* DevOps / SRE teams managing access logs
* SaaS platforms with high login traffic
* Organizations automating incident detection and response
* Teams using **Jira, Slack, Notion, and n8n** for security workflows

---

## 🛠 Requirements

To run this workflow, you need:

* **n8n instance** (cloud or self-hosted)
* An application capable of POSTing failed login events
* **Jira Software Cloud credentials** (Email, API Token, Domain)
* **Slack Bot Token** with message-posting permissions
* **Notion API credentials** with access to a logging database

---

## 🧠 How It Works

1. **Webhook Trigger**
   The workflow starts when a failed login event is sent to the webhook.

2. **Normalization**
   Handles single objects or arrays and standardizes fields (`username`, `IP`, `timestamp`, `error`).

3. **Validation**
   Checks for required fields and sends a Slack alert if validation fails.

4. **Multiple Attempt Detection**
   A function node tracks attempts within a configurable sliding window and flags repeated failures.

5. **Branching Logic**

   * **Single Attempt**

     * Create Jira issue
     * Send Slack alert
     * Log event in Notion
   * **Multiple Attempts**

     * Group related events
     * Create a detailed Jira security issue
     * Send summarized Slack alert
     * Log grouped data in Notion

6. **Slack Alerts**
   Messages are formatted differently for single vs. repeated attempts and can include Jira links.

7. **Notion Logging**
   Stores structured data such as username, IP, total attempts, error messages, and incident type.

---

## 🛠 How to Set Up

### 1. Import the Workflow

In n8n, go to **Workflows → Import from File** and upload the JSON.

### 2. Configure the Webhook

Copy the webhook URL from the **Failed Login Trigger** node and configure your application to send POST requests to it.

### 3. Configure Credentials

* **Jira** — Select project, issue type, and authentication
* **Slack** — Connect bot token and choose alert channel
* **Notion** — Select the database used for logging login attempts

### 4. Test the Workflow

Send test payloads:

* Missing fields
* Single failed login
* Multiple failed logins within the time window

Verify:

* Jira tickets
* Slack alerts
* Notion database entries

### 5. Activate

Enable the workflow once everything works as expected.

---

## 🔧 Customization Options

* **Webhook Path** — Rename the endpoint to match your system naming
* **Normalization Logic** — Add fields like device, OS, location, or user-agent
* **Detection Rules** — Adjust time window and attempt threshold
* **Jira Configuration** — Customize issue type, priority, labels, or project
* **Slack Formatting** — Add severity tags or route alerts to multiple channels
* **Notion Schema** — Store metadata like geolocation, browser, or risk level

---

## 📈 Use Case Examples

1. Detect brute-force login attacks on web or mobile apps
2. Automatically create security incidents for SOC teams
3. Monitor admin portal login failures
4. Trigger instant alerts for suspicious authentication behavior
5. Centralize authentication failure auditing in Notion

---

## 🧪 Troubleshooting Guide

| Issue                          | Possible Cause                     | Solution                            |
| ------------------------------ | ---------------------------------- | ----------------------------------- |
| Workflow not receiving events  | Webhook misconfigured              | Verify webhook URL and POST payload |
| Jira issue creation fails      | Invalid credentials or permissions | Reconnect Jira credentials          |
| Slack alert not sent           | Bot permissions or channel error   | Check Slack scopes and channel ID   |
| Repeated attempts not detected | Sliding window misconfigured       | Adjust detection logic or threshold |
| Notion logging fails           | Wrong database or missing access   | Update database ID and permissions  |

---

## 💬 Need Help?

If you need help setting up, customizing, or extending this workflow — including advanced security enrichment (geo-IP, threat feeds, SIEM integrations) — **WeblineIndia’s n8n automation experts** can help you design and scale professional security automation solutions.

Happy automating & stay secure 🔐🚀
