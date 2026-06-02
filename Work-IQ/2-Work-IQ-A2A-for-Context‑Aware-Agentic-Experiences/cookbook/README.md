# Episode 2 Cookbook: A2A for Context‑Aware, Agentic Experiences

This folder contains the hands-on cookbook for Episode 2 of The Work IQ Series.

## 📋 Prerequisites

- **Microsoft 365 Tenant** with proper licensing
- **Node.js** 22 or later installed
- **Python 3.10+** installed
- **A2A Inspector** downloaded and running on your environment
- **Work IQ** enabled in your target tenant with **Administrative consent** for the **Work IQ application**
- **Work IQ CLI** installed

## 🛠️ Downloading and running A2A Inspector

**A2A Inspector** is an open-source, web-based tool for visualizing, debugging, and validating Agent-to-Agent (A2A) protocol interactions. It helps you inspect agent conversations, message flows, and protocol details in real time, making it easier to develop and troubleshoot agentic applications.

The official GitHub repository is: [https://github.com/a2aproject/a2a-inspector](https://github.com/a2aproject/a2a-inspector)

---

### Prerequisites

- Python 3.10+
- [uv](https://github.com/astral-sh/uv) (for Python dependency management)
- Node.js and npm

---

### 1. Clone the repository

```sh
git clone https://github.com/a2aproject/a2a-inspector.git
cd a2a-inspector
```

### 2. Install dependencies

**Backend (Python):**

From the project root:
```sh
uv sync
```

**Frontend (Node.js):**

```sh
cd frontend
npm install
cd ..
```

---

### 3. Run the application

You can run A2A Inspector either locally (recommended for development) or using Docker.

#### Option 1: Run Locally (with live reload)

**Recommended:** Use the provided script to start both frontend and backend with live reload:

```sh
chmod +x scripts/run.sh   # (first time only)
bash scripts/run.sh
```

Or, run manually in two terminals:

**Terminal 1 (Frontend):**
```sh
cd frontend
npm run build -- --watch
```

**Terminal 2 (Backend):**
```sh
cd backend
uv run app.py
```

Once both are running, open your browser at: http://127.0.0.1:5001

#### Option 2: Run with Docker

If you prefer Docker, from the project root:

```sh
docker build -t a2a-inspector .
docker run -d -p 8080:8080 a2a-inspector
```

Then open your browser at: http://127.0.0.1:8080

---

For more details and troubleshooting, see the [A2A Inspector GitHub page](https://github.com/a2aproject/a2a-inspector).

## ⚙️ Enabling Work IQ in your tenant

Follow this brief enablement flow as a tenant admin:

1. Verify licensing requirements are satisfied for users who need Work IQ.
1. Sign in with an eligible admin role (for example, Global Administrator or Application Administrator).
1. Grant tenant-wide admin consent using this URL:
  `https://login.microsoftonline.com/{your-tenant-id}/adminconsent?client_id=ba081686-5d24-4bc6-a0d6-d034ecffed87`
  Replace `{your-tenant-id}` with your tenant ID (GUID) or tenant domain, open it in a browser, sign in as admin, then click **Accept**.
1. If the consent page returns access-denied/AADSTS errors, run the enablement script to provision missing service principals, then retry consent:
  `https://github.com/microsoft/work-iq/blob/main/scripts/Enable-WorkIQToolsForTenant.ps1`
1. Validate in Microsoft Entra admin center > Enterprise applications > Work IQ CLI > Permissions, and confirm all required permissions are granted for your organization.
1. Optionally restrict access by setting Assignment required? to Yes and assigning only approved users/groups.

For complete prerequisites, exact URLs/scripts, troubleshooting, and security guidance, see the full admin guide: https://github.com/microsoft/work-iq/blob/main/ADMIN-INSTRUCTIONS.md

## 🏗️ Installing Work IQ CLI

Work IQ CLI can be installed in multiple ways depending on your setup. Choose the method that best fits your workflow:

### Option 1: Using GitHub Copilot CLI (Recommended)

The fastest way to get started:

```bash
# Open GitHub Copilot CLI
copilot

# Add the plugins marketplace (one-time setup)
/plugin marketplace add github/copilot-plugins

# Install Work IQ
/plugin install workiq@copilot-plugins

# Restart Copilot CLI
```

### Option 2: Install Globally

Install Work IQ globally using npm:

```bash
npm install -g @microsoft/workiq
```

### Option 3: Run with npx (No Installation Required)

Use Work IQ directly without installation:

```bash
npx -y @microsoft/workiq mcp
```

### Option 4: Install in VS Code

Click one of these links to add Work IQ as an MCP server in VS Code:

- [Install in VS Code](https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fworkiq%22%2C%22mcp%22%5D%2C%22name%22%3A%22workiq%22%7D)
- [Install in VS Code Insiders](https://insiders.vscode.dev/redirect?url=vscode-insiders%3Amcp%2Finstall%3F%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fworkiq%22%2C%22mcp%22%5D%2C%22name%22%3A%22workiq%22%7D)

### Option 5: Manual MCP Configuration

Add the following configuration to your MCP settings file:

```json
{
  "workiq": {
    "command": "npx",
    "args": [
      "-y",
      "@microsoft/workiq",
      "mcp"
    ],
    "tools": [
      "*"
    ]
  }
}
```

### Accept the End User License Agreement

Before using Work IQ for the first time, accept the EULA:

```bash
workiq accept-eula
```

### Prerequisites

Before installing, ensure you have:

- Node.js installed on your machine
- A Microsoft 365 subscription with a Copilot license
- Administrative consent for the Work IQ application in your Microsoft Entra tenant
- GitHub Copilot CLI (optional, but recommended)

> **Note:** To access Microsoft 365 organization data, the Work IQ CLI needs administrative consent in your organization. If you're not an organization administrator, contact your admin for access.

### Platform Support

Work IQ supports:
- Windows (x64 and ARM64)
- Linux (x64 and ARM64)
- macOS (x64 and ARM64)
- Windows Subsystem for Linux (WSL) with browser support

For more information, see the [Work IQ CLI documentation](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq-cli).

## 📓 Lab Instructions

The [**Work IQ Lab for Episode 02**](./work-iq-lab02.md) walks you through the basic capabilities of Work IQ, step by step:

1. Asking a prompt via Work IQ A2A
1. Asking a second prompt via Work IQ A2A within the same conversation context

## Additional Resources

- [Episode 2 README](../README.md)
- [Work IQ overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq)
- [Copilot Dev Camp - Work IQ](https://microsoft.github.io/copilot-camp/pages/work-iq/)
