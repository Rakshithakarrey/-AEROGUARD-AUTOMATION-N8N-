# ✈️ AeroGuard – AI-Powered Aircraft Maintenance Workflow

AeroGuard is an AI-powered **n8n workflow** that receives aircraft maintenance reports, analyzes them using an AI Agent, identifies the issue severity, and triggers the appropriate action or alert.

## 🔄 Workflow

```text
Webhook
   ↓
AI Agent
   ↓
Severity Check
   ↓
HIGH / MEDIUM / LOW
   ↓
Alert / Review / Monitor
   ↓
Respond to Webhook
```

## 🛠️ Technologies

* n8n
* AI Agent
* Google Gemini / supported Chat Model
* Webhooks
* JSON
* IF/Switch conditions
* Gmail (optional)

## 📥 Import Workflow in n8n

1. Open **n8n**.
2. Create a new workflow.
3. Open the **workflow menu (...)**.
4. Select **Import from File**.
5. Select the AeroGuard `.json` workflow file.
6. The nodes and connections will appear automatically.

## ⚙️ Configure Before Execution

After importing:

1. Open the **AI Agent** node.
2. Connect a supported **Chat Model**.
3. Add your AI API credentials.
4. Select an available AI model.
5. If using Gmail alerts, configure your **Gmail credentials**.
6. Check the Webhook and other node expressions.
7. Save the workflow.

> API keys, passwords, access tokens, and other credentials must not be included in the workflow file or shared publicly.

## 📄 Sample Input

Send this JSON to the Webhook:

```json
{
  "aircraft_id": "AF-102",
  "component": "Engine Sensor A",
  "report_date": "2026-09-28",
  "observation": "Sensor reading fluctuated above the normal demo threshold.",
  "technician": "Demo Technician",
  "location": "Demo Hangar 1"
}
```

## ▶️ How to Execute in n8n

### Step 1 – Open the Workflow

Open the imported **AeroGuard** workflow.

### Step 2 – Test the Webhook

Open the **Webhook** node.

Click:

**Listen for Test Event / Execute Workflow**

n8n will wait for incoming data.

### Step 3 – Send the JSON

Use Postman, PowerShell, or another API client to send a **POST** request to the Webhook Test URL.

Example PowerShell:

```powershell
$body = @{
    aircraft_id = "AF-102"
    component = "Engine Sensor A"
    report_date = "2026-09-28"
    observation = "Sensor reading fluctuated above the normal demo threshold."
    technician = "Demo Technician"
    location = "Demo Hangar 1"
} | ConvertTo-Json

Invoke-RestMethod `
    -Uri "YOUR_N8N_WEBHOOK_TEST_URL" `
    -Method POST `
    -ContentType "application/json" `
    -Body $body
```

### Step 4 – Workflow Execution

Once the request is received:

```text
POST Request
     ↓
Webhook receives JSON
     ↓
AI Agent analyzes report
     ↓
AI generates severity
     ↓
Severity is checked
     ↓
HIGH / MEDIUM / LOW branch
     ↓
Alert / Review / Monitor
     ↓
Respond to Webhook
```

### Step 5 – Check the Execution

In n8n, open the execution data for each node.

Verify:

* Webhook received the aircraft data.
* AI Agent executed successfully.
* AI returned a severity.
* Severity condition selected the correct branch.
* Alert node executed when required.
* Respond to Webhook returned the final result.

## 🧠 Example AI Result

```text
SEVERITY: MEDIUM
POTENTIAL ISSUE: Abnormal engine sensor fluctuation
EXPLANATION: Sensor reading is above the expected demo threshold.
NEXT ACTION: Inspect the engine sensor and monitor the system.
```

## 📊 Severity Routing

| Severity | Action                        |
| -------- | ----------------------------- |
| HIGH     | Send urgent maintenance alert |
| MEDIUM   | Send for maintenance review   |
| LOW      | Monitor or record             |

## 🔐 Important

The workflow JSON contains the workflow structure, but **your credentials must be configured separately in n8n**.

Do not share:

* API keys
* Access tokens
* Passwords
* Gmail credentials
* Private webhook credentials

## 🎯 Result

AeroGuard demonstrates how **AI + n8n automation** can analyze aircraft maintenance reports and automatically route maintenance actions based on issue severity.

> **Note:** AeroGuard is a learning/demo project and does not replace certified aircraft maintenance procedures or professional aviation safety systems.
