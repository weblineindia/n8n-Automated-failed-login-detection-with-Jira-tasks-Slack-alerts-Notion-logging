# Automated Failed Login Detection with Jira Tasks, Slack Alerts & Notion Logging

This n8n workflow monitors failed login attempts from any application, detects repeated failures within a configurable time window, and automates your incident response by creating Jira security tasks, sending Slack alerts, and logging all events into a Notion database. It provides fast, structured response automation for potential account compromise or brute‑force attacks. :contentReference[oaicite:1]{index=1}

---

## ⚡ Quick Implementation Steps

1. Import the workflow JSON into your n8n instance. :contentReference[oaicite:2]{index=2}
2. Connect your application to the **Failed Login** webhook endpoint. :contentReference[oaicite:3]{index=3}
3. Add **Jira Cloud API credentials**. :contentReference[oaicite:4]{index=4}
4. Add **Slack API credentials**. :contentReference[oaicite:5]{index=5}
5. Add **Notion API credentials** and configure the database for storing login attempts. :contentReference[oaicite:6]{index=6}
6. Enable the workflow — it’s ready to run! :contentReference[oaicite:7]{index=7}

---

## 📌 What It Does

This workflow automates failed login monitoring and response:

- Accepts **POST** requests containing failed login data (username, IP, timestamp, error). :contentReference[oaicite:8]{index=8}
- Normalizes input to ensure consistent processing. :contentReference[oaicite:9]{index=9}
- Validates required fields (username, IP); notifies Slack if missing. :contentReference[oaicite:10]{index=10}
- Detects multiple attempts within a **sliding time window** (default: 5 minutes). :contentReference[oaicite:11]{index=11}
- Creates **Jira Security tasks** for either single or grouped repeated attempts. :contentReference[oaicite:12]{index=12}
- Sends **Slack alerts** with detailed information. :contentReference[oaicite:13]{index=13}
- Logs all attempts in a **Notion database** for auditing and analysis. :contentReference[oaicite:14]{index=14}

---

## 👥 Who’s It For

This workflow is ideal for:

- Security teams monitoring authentication logs. :contentReference[oaicite:15]{index=15}
- DevOps / SRE teams maintaining infrastructure access logs. :contentReference[oaicite:16]{index=16}
- SaaS platforms with high login traffic. :contentReference[oaicite:17]{index=17}
- Organizations automating breach detection and alerts. :contentReference[oaicite:18]{index=18}
- Teams using **Jira, Slack, Notion and n8n** for incident workflows. :contentReference[oaicite:19]{index=19}

---

## 🛠 Requirements

To run this workflow, you need:

- **n8n instance** (cloud or self‑hosted). :contentReference[oaicite:20]{index=20}
- Source application capable of POSTing failed login events. :contentReference[oaicite:21]{index=21}
- **Jira Software Cloud API credentials** (Email, API Token, Domain). :contentReference[oaicite:22]{index=22}
- **Slack Bot Token** with message‑posting permissions. :contentReference[oaicite:23]{index=23}
- **Notion API credentials** with access to a database for storing attempt logs. :contentReference[oaicite:24]{index=24}

---

## 🧠 How It Works

1. **Webhook Trigger** — Workflow starts when a failed login event is POSTed to the webhook. :contentReference[oaicite:25]{index=25}
2. **Normalization** — Handles arrays or single objects, and ensures required fields (`username`, `IP`, `timestamp`, `error`). :contentReference[oaicite:26]{index=26}
3. **Validation** — Checks for missing fields; sends Slack alert if validation fails. :contentReference[oaicite:27]{index=27}
4. **Detect Multiple Attempts** — A function node tracks repeated attempts within the time window and sets a flag if multiple attempts are detected. :contentReference[oaicite:28]{index=28}
5. **Branching Logic**:
   - **Single Attempts** — Creates a Jira ticket, sends Slack alert, logs in Notion. :contentReference[oaicite:29]{index=29}
   - **Multiple Attempts** — Builds a detailed summary, groups events, creates a detailed Jira ticket, sends a Slack summary, logs to Notion. :contentReference[oaicite:30]{index=30}
6. **Slack Alerts** — Formatted messages differ for single vs. multiple attempts and can include Jira links. :contentReference[oaicite:31]{index=31}
7. **Notion Logging** — Stores structured attempt data including username, IP, total attempts, errors, and attempt type. :contentReference[oaicite:32]{index=32}

---

## 🛠 How to Set Up

1. **Import the Workflow** — In n8n, go to “Workflows → Import from File” and upload JSON. :contentReference[oaicite:33]{index=33}
2. **Configure Webhook** — Copy the webhook URL from the **Failed Login Trigger** node and point your application at it. :contentReference[oaicite:34]{index=34}
3. **Add Credentials** —
   - **Jira** — Connect to both Jira nodes and set project/issue type. :contentReference[oaicite:35]{index=35}
   - **Slack** — Connect Slack Bot and choose alert channel. :contentReference[oaicite:36]{index=36}
   - **Notion** — Connect Notion account, and select the database for logging. :contentReference[oaicite:37]{index=37}
4. **Test the Workflow** — Send test JSON (missing fields, single vs. multiple attempts) and verify Slack, Jira, and Notion behavior. :contentReference[oaicite:38]{index=38}
5. **Activate** the workflow once validations succeed. :contentReference[oaicite:39]{index=39}

---

## 🔧 Customization Options

- **Webhook Node** — Change endpoint path to match your system’s naming conventions. :contentReference[oaicite:40]{index=40}
- **Normalization Function** — Add fields such as device, OS, location, or user‑agent. :contentReference[oaicite:41]{index=41}
- **Sliding Window Logic** — Modify time window duration and threshold for repeated attempts. :contentReference[oaicite:42]{index=42}
- **Jira** — Customize issue type, priority, labels, or project. :contentReference[oaicite:43]{index=43}
- **Slack Formatting** — Adjust message blocks, add severity tags, or route to multiple channels. :contentReference[oaicite:44]{index=44}
- **Notion Logging** — Extend database fields to store metadata like geolocation or device info. :contentReference[oaicite:45]{index=45}

---

## 📈 Use Case Examples

1. Detect brute‑force login attempts across web or mobile applications. :contentReference[oaicite:46]{index=46}
2. Support security ops with automatic incident task creation. :contentReference[oaicite:47]{index=47}
3. Monitor admin portal login failures and escalate via Jira. :contentReference[oaicite:48]{index=48}
4. Alert security teams instantly when unusual login patterns emerge. :contentReference[oaicite:49]{index=49}
5. Centralize failed login tracking across services with persistent Notion logs. :contentReference[oaicite:50]{index=50}

---

## 🧪 Troubleshooting Guide

| **Issue**                      | **Possible Cause**                    | **Solution**                                  |
| ------------------------------ | ------------------------------------- | --------------------------------------------- | --------------------------------------- |
| Workflow not receiving events  | Webhook misconfigured                 | Verify webhook URL & POST payload format      |
| Jira ticket creation fails     | Invalid credentials                   | Update Jira credentials & permissions         |
| Slack alert not sent           | Bot lacks permission or wrong channel | Fix Slack scopes and channel ID               |
| Multiple attempts not detected | Sliding window logic misaligned       | Adjust detection threshold or code node logic |
| Notion logging fails           | Wrong database or missing access      | Update Notion credentials & database ID       | :contentReference[oaicite:51]{index=51} |

---

## 💬 Need Help?

If you need assistance setting up, customizing, or extending this workflow — from advanced security enrichments (geo‑lookup, threat feeds) to automation strategies — **WeblineIndia**’s n8n experts can help with professional automation solutions and tailored workflow development. :contentReference[oaicite:52]{index=52}

---
