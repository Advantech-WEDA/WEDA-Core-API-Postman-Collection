# WEDA Postman API Collection

## What is WEDA Postman API Collection?

This Postman collection provides ready-to-use API requests for the **WEDA platform**. Instead of manually constructing API calls, you can use these pre-configured requests to quickly test and integrate WEDA APIs.

**What's Included:**

- ✅ Authentication & Authorization
- ✅ Organization & Device Management
- ✅ Container Stack Deployment
- ✅ Telemetry Data Collection
- ✅ Tunnel Management for Remote Access
- ✅ AI Model Management

---

## Why Use This Collection?

### Problems It Solves

**1. Complex API Dependencies**  
WEDA APIs require specific execution sequences (e.g., authenticate → create org → provision device). This collection handles the sequence automatically.

**2. Manual Testing is Tedious**  
Testing APIs manually requires remembering URLs, parameters, and authentication tokens. This collection automates these tasks.

**3. Multi-Module Coordination**  
Testing end-to-end workflows (e.g., deploy container to device) requires coordinating multiple API calls. This collection chains requests together.

**4. Learning Curve**  
Understanding how to use WEDA APIs can be challenging. This collection provides working examples you can run immediately.

### What You Get

✅ **Pre-configured Requests** - All API calls ready to use  
✅ **Automatic Variable Management** - Authentication tokens and IDs are auto-saved between requests  
✅ **Sequential Workflows** - Requests automatically chain together for complex operations  
✅ **Built-in Validation** - Each request includes test scripts to verify success

---

## Pre-requisites

### Step 1: Install Postman
### Step 2: Get Collection Files

Download and extract the [WEDA API collection]() package

> **Note**: If you download the .zip file, make sure to extract it.

### Step 3: Import into Postman

1. Click **Import** button (top-left)
2. Choose the file or folder you downloaded
3. Click **Import**. You should see 7 collections imported in the left sidebar.

<br />
**Postman Overview**
- left side: 
  - **Collections**: 7 collections containing categorized API requests
  - **Environments**: Select `weda-core` environment for API requests
- main panel:
  - send request and request setting/response details
- right side:
  - **Variables**: shows environment variables (auto-populated from API responses)

### Step 4: Configure Your Environment

1. Click **Environments** tab (left sidebar)
2. Select your environment(`weda-core`).
3. Update these 4 required variables:

| Variable     | Your Value                                            |
| ------------ | :---------------------------------------------------- |
| `login`      | Your WEDA account email — **required**                |
| `password`   | Your WEDA account password — **required**             |
| `domain`     | Pre-filled with `https://tpe.cloud.advantech.com`; change only if your deployment differs |
| `ssoBaseUrl` | Pre-filled with `identity`; change only if your deployment differs |

> **Note**: If you don't have WEDA account, please go to [Register Free Trial](https://wise.advantech.com/en-tw/products/advantech.WEDA) to request one.

**You don't need to manually check these variables except for the 4 variables mentioned above** - they are automatically captured from API responses.

4. **Activate the environment** - Select it from the dropdown (top-right corner)

**Congratulations!** You're ready to use the WEDA API collection.

---

## How to Use

### Running a Single Request

1. **Select a collection** from the left sidebar (e.g., **2-Provisioning&Activation**)
2. **Click on a request** (e.g., **Provisioning Node**)
3. **Review the request** details in the main panel
4. **Click Send** button
5. **Check the response**:
   - Status code (should be 200, 201, or 202 for success)
   - Response body (JSON data returned by API)
   - Test Results tab (validation results)

despite the detail of each API, the most important thing when using WEDA Postman API collection is to use the API in sequential workflows. Please follow the squence of collections to run the APIs, and you can achieve the desired results.

### Running the AI Model Management workflow

The **7-AI-Model-Mgmt** collection uploads a model, deploys it to a device, verifies the deployment, and then cleans up. Before running it with Postman Collection Runner or Newman:

1. Configure the collection variables listed in its description, including `apibaseurl`, `baseUrl`, `tusd`, `accessToken`, `org_id`, and `deviceId`.
2. Provide your own model file and set the collection variables `fileName`, `fileSize` (exact size in bytes), and `fileHash` (the file's SHA-256 hex digest, 64 characters without a prefix). These values must match the file you upload.
3. In **Upload a file chunk**, select that same file under **Body → binary**. For Newman, make the file available under `--working-dir` and set the request body's file `src` to its relative path.
4. The collection generates a unique, v1.2-compatible `modelEdition` automatically. The `containerName` variable defaults to `container1`; change it if the target device uses a different container name.

**Important:** This workflow deploys the model to the target device, activates it by restarting the configured container, and later removes the model deployment during cleanup. Use a test device and confirm that restarting the container and removing this model are safe before running the collection.

---

## Troubleshooting

### Clear All Cookies

**Goal**: Before starting, it's recommended to clear all cookies in Postman to avoid authentication issues. And if you get any error with unknown reason, please try to clear cookies and run again.

---

## Additional Resources

### Postman

- [Postman Getting Started](https://learning.postman.com/docs/getting-started/introduction/)
- [Using Variables](https://learning.postman.com/docs/sending-requests/variables/)
