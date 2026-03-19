# ServiceNow Tenant & Copilot Connector Setup Guide

> **Referenced from**: [Phase 1 — Step 1-1 in Step-by-Step Deployment Guide](./3.Step-by-Step-Guide.md#step-1-1-create-servicenow-tenant--configure-copilot-connector)  
> **Purpose**: Set up a free ServiceNow Developer Instance and configure the
> ServiceNow Knowledge Copilot Connector in M365 Admin Center  
> **Target Users**: CSA / Vendor / PM  
> **Last Updated**: March 2026

---

## Overview

This guide walks through two main tasks:

1. **Create a free ServiceNow Developer Instance** — required as the external
   knowledge source for the HROnboardingAutoAgent
2. **Install and configure the ServiceNow Knowledge Copilot Connector** — indexes
   ServiceNow knowledge base articles into M365 so they can be used as agent knowledge

> ⚠️ **Before You Start**  
> - The ServiceNow Copilot Connector is currently in **public preview**  
> - This capability is **enabled by default** in all Microsoft 365 Copilot licensed tenants  
> - Admins can disable this on a user/group basis via **Integrated Apps** in M365 Admin Center  
> - Reference: [Manage Plugins for Copilot in Integrated Apps](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-plugins-for-copilot-in-integrated-apps)

---

## Prerequisites

| Requirement | Details |
|---|---|
| Email address | Required to sign up for a ServiceNow Developer account (Microsoft corp email recommended) |
| M365 Admin access | Required to install and configure the Copilot Connector |
| Microsoft 365 Copilot license | Required for the tenant where the connector will be installed |

---

## Part 1: Create a Free ServiceNow Developer Instance

### Step 1-1-1. Sign Up for a ServiceNow Developer Account

1. Open your browser and go to https://developer.servicenow.com

   > 📸 **[Screenshot required]** — ServiceNow Developer Program home page with the "Sign In" button in the top right corner

2. Click **"Sign In"** in the top right corner
3. Click **"Get a ServiceNow ID"**

   > 📸 **[Screenshot required]** — Sign in page showing the "Get a ServiceNow ID" link

4. Fill out the registration form with the following details:
   - First Name
   - Last Name
   - Email *(Microsoft corp email is recommended)*
   - Country
   - Password
   - Check the reCAPTCHA box
   - Accept the Terms of Use
5. Click **Submit**

   > 📸 **[Screenshot required]** — ServiceNow ID registration form filled out

---

### Step 1-1-2. Verify Your Email

1. Check your inbox for a verification email from `signon@service-now.com`
2. Click **"Verify Email"** in the email

   > 📸 **[Screenshot required]** — Verification email from ServiceNow with the "Verify Email" button

3. After verification, log in to your ServiceNow account
4. On first login, enter the **one-time verification code** sent to your email

   > 📸 **[Screenshot required]** — One-time verification code email from ServiceNow

   > 💡 **Note**: MFA setup will appear on the next screen. For simplicity, click **"Skip"** to proceed without MFA.

---

### Step 1-1-3. Complete Initial Setup

1. On the next screen, click **"Developer Program"**

   > 📸 **[Screenshot required]** — Post-login screen with "Developer Program" option

2. In the **"Getting Started"** dialog, click **"No"** (I need a guided experience)

   > 📸 **[Screenshot required]** — "Getting Started" dialog with "No" option selected

3. In the next window, select your preferred options, check the **Terms of Use** checkbox, and click **"Finish Setup"**

   > 📸 **[Screenshot required]** — Setup preferences screen with Terms of Use checkbox

---

### Step 1-1-4. Request a ServiceNow Instance

1. You should now be in your **ServiceNow Developer Dashboard**
2. Click **"Request Instance"** in the top right corner

   > 📸 **[Screenshot required]** — ServiceNow Developer Dashboard with "Request Instance" button in the top right

   > 💡 This process typically takes less than a minute.

3. Once the instance is ready, a pop-up will appear with your instance details:
   - **Instance URL**: `https://dev[XXXXXX].service-now.com`
   - **Username**: `aes.creator`
   - **Current password**: *(auto-generated)*

   > 📸 **[Screenshot required]** — "Your instance is ready!" pop-up showing Instance URL, Username, and Password

   > ⚠️ **Important**: Click **"Return to the Developer Site"** when this pop-up appears. Do NOT click "Open Instance" yet.

4. Click your **profile icon** in the top right corner

   > 📸 **[Screenshot required]** — Developer site with profile icon in the top right

---

### Step 1-1-5. Switch to Admin Role

1. Click **"Change User Role"** from the profile dropdown

   > 📸 **[Screenshot required]** — Profile dropdown menu showing "Change User Role" option

2. In the **"Change User Role"** dialog, select **"Admin"**

   > 📸 **[Screenshot required]** — Change User Role dialog with "Admin" option selected

   > ⚠️ **Important**: Admin access is required to configure the ServiceNow instance for the Copilot Connector.

3. Click **"Change User Role"** to confirm
4. Click **"Done"** once the change is confirmed

   > 📸 **[Screenshot required]** — "Your change user role request is completed successfully" confirmation screen

5. Click **"Cancel"** to exit the dialog

---

### Step 1-1-6. Retrieve Admin Credentials

1. In your **"My Instance"** details window, click **"Manage instance password"**

   > 📸 **[Screenshot required]** — My Instance panel showing "Manage instance password" option

2. Note down the following credentials — you will need them in Part 2:
   - **Instance URL**: `https://dev[XXXXXX].service-now.com`
   - **Username**: `admin`
   - **Password**: *(shown in the manage password screen)*

   > ⚠️ **Important Notes on Instance Availability**:  
   > - ServiceNow instances will **hibernate** after a period of inactivity  
   > - Attempts to access the instance via Graph or Power Platform connectors will **fail** when the instance is hibernating  
   > - Always validate the instance is **awake** before starting your demo  
   > - If an instance is **dormant for more than 10 days**, it will be reclaimed by ServiceNow — logging in via the Copilot connector alone is **not sufficient** to keep it active

---

## Part 2: Configure Admin Access in ServiceNow Instance

### Step 1-1-7. Log In to Your ServiceNow Instance as Admin

1. Open your browser and go to your **Instance URL** from Step 1-1-6  
   `https://dev[XXXXXX].service-now.com`
2. Log in with:
   - **Username**: `admin`
   - **Password**: *(from Step 1-1-6)*

   > 📸 **[Screenshot required]** — ServiceNow instance login page with admin credentials entered

---

### Step 1-1-8. Verify Knowledge Bases are Available

1. Click the **"All"** tab in the top navigation
2. Type **"knowledge bases"** in the search field
3. Select **"Knowledge Bases"** under **Knowledge > Administration**

   > 📸 **[Screenshot required]** — ServiceNow search showing "Knowledge Bases" under Knowledge > Administration

4. Confirm the following four default Knowledge Bases are listed:

   | Knowledge Base | Description |
   |---|---|
   | KCS Knowledge Base (demo data) | KCS Demo KB |
   | Known Error | Default knowledge base for Known Errors |
   | IT | The ACME North America IT Service Desk Knowledge Base |
   | Knowledge | Knowledge Base for general Knowledge users |

   > 📸 **[Screenshot required]** — Knowledge Bases list showing all four default knowledge bases

   > 💡 These four knowledge bases will be imported and indexed into M365 using the ServiceNow Copilot Connector.

---

## Part 3: Install the ServiceNow Knowledge Copilot Connector

> ⚠️ **You will need your ServiceNow admin credentials from Step 1-1-6 for this part.**

### Step 1-1-9. Add a New Connection in M365 Admin Center

1. Log in to **M365 Admin Center** → https://admin.microsoft.com
2. Navigate to **Settings** → **Search & Intelligence** → **Data sources**
3. Click **"+ Add Connection"**

   > 📸 **[Screenshot required]** — M365 Admin Center, Search & Intelligence > Data sources page with "Add Connection" button

4. In the connector list, select **"ServiceNow Knowledge"**
5. Click **"Next"**

   > 📸 **[Screenshot required]** — Connector selection page with "ServiceNow Knowledge" selected

---

### Step 1-1-10. Configure the Connection Settings

1. Click **"Custom setup"** in the upper right of the screen

   > 📸 **[Screenshot required]** — Connection setup page with "Custom setup" button in the upper right

2. Fill in the following fields in the **Setup** tab:

   | Field | Value |
   |---|---|
   | Display name | `ServiceNow` *(or a unique name, e.g., `ServiceNowKB5`)* |
   | ServiceNow URL | `https://dev[XXXXXX].service-now.com` *(your instance URL from Step 1-1-6)* |
   | Authentication type | `Basic` |
   | Username | `admin` |
   | Password | *(your admin password from Step 1-1-6)* |

   > ⚠️ **Security Note**: `Basic` authentication is used for **demo/dev purposes only**.  
   > For **customer deployments**, always use **ServiceNow OAuth** or **Azure AD OIDC**.

   > 📸 **[Screenshot required]** — Setup tab with all connection fields filled in

---

### Step 1-1-11. Authenticate the Connection

1. Wait for the **"Sign in"** button to appear under the authentication section

   > 💡 **Known Issue**: There is a current UI bug where the "Sign in" button may not appear immediately. Wait a moment and it will show up.

2. Click **"Sign in"** and wait for authentication to complete

   > 📸 **[Screenshot required]** — Authentication section showing the "Sign in" button

3. After successful authentication, confirm that **green check marks** appear next to the username and password fields

   > 📸 **[Screenshot required]** — Authentication section showing green check marks next to username and password

---

### Step 1-1-12. Configure User Access Permissions

1. Click the **"Users"** tab at the top of the setup panel

   > 📸 **[Screenshot required]** — Custom setup tabs showing Setup, Users, Content, and Sync tabs

2. Under **"Access Permissions"**, select **"Everyone"**

   > 📸 **[Screenshot required]** — Users tab with "Everyone" selected under Access Permissions

   > ⚠️ **Security Note**: **"Everyone"** is selected for demo/dev convenience only.  
   > For **customer deployments**, always select **"Only people with access to this data source"**  
   > to preserve the access controls configured in ServiceNow.

---

### Step 1-1-13. Create the Connection

1. Go back to the **"Setup"** tab
2. Scroll to the bottom and check the **Notice** checkbox to accept
3. Wait for the **"Create"** button to become enabled

   > 💡 This may take up to a minute. If the button remains disabled, try clicking to the **Users** tab and back to trigger the button activation.

4. Click **"Create"**

   > 📸 **[Screenshot required]** — Setup tab with Notice checkbox checked and the "Create" button enabled

5. The button will display **"Creating connection"** while the process runs

---

### Step 1-1-14. Add a Connector Description

1. Once the connection is created, a success screen will appear:  
   **"Created connection — ServiceNow (ServiceNowKB[X])"**

   > 📸 **[Screenshot required]** — Success screen showing "Created connection" with the connector name

2. Click **"Auto suggestion"** to have Copilot generate a description automatically

   > 📸 **[Screenshot required]** — Next steps screen with the "Auto suggestion" button

   > 💡 **If "Auto suggestion" does not work** (known bug), you can add the description later:  
   > - Wait until the connection status shows **"Ready"**  
   > - Click the connection in the list → Click **"Edit description"**  
   > - Paste the following sample description:

   ```
   I want to use this connection to provide solutions, best practices,
   troubleshooting guides, and other relevant content. It serves as a
   valuable resource for users, IT professionals, and support teams within
   organizations. The data source contains articles, documents, and FAQs
   related to various topics, including software applications, hardware,
   processes, and policies.
   ```

3. Click **"Done"**

   > ⚠️ **Important**: The **first sync can take up to 2 hours** to complete.  
   > Wait for the sync to finish before proceeding to the next step.

   > 📸 **[Screenshot required]** — Data sources page showing the new ServiceNow connector with "Preparing to sync" status

---

## Part 4: Verify the Connection

### Step 1-1-15. Verify Indexed Content via Microsoft Search

1. Navigate to https://microsoft365.com and log in as a user in your tenant
2. In the search box at the top, type **`KB0*`** and press **Enter**

   > 📸 **[Screenshot required]** — Microsoft 365 search results showing KB articles from ServiceNow

3. Click **"All Sources"** filter → Select your ServiceNow connector (e.g., `ServiceNow-KB`)
4. Confirm that KB articles from ServiceNow are listed in the results

   > 📸 **[Screenshot required]** — Search results filtered by ServiceNow-KB showing knowledge articles

---

### Step 1-1-16. Verify via M365 Copilot Prompts (Optional)

Use the following prompts in **M365 Copilot (Teams)** to verify the connector is working:

> 💡 Before testing, disable **"Web content"** in the Copilot plugin settings to ensure responses come only from the ServiceNow connector.

| Scenario | Prompt |
|---|---|
| Test basic retrieval | `List the articles regarding Outlook 2010. Place the results in a table with the article title in one column and a brief summary in the other.` |
| Test thematic analysis | `What are the main themes in the ServiceNow IT knowledge base regarding Windows?` |
| Test content drafting | `Draft an email to inform employees about necessary precautions to prevent phishing attacks and remind them of their data protection responsibilities. Include a brief summary of each KB article.` |

---

## Summary Checklist

| Step | Task | Status |
|---|---|---|
| 1-1-1 | ServiceNow Developer account created | ☐ |
| 1-1-2 | Email verified and account activated | ☐ |
| 1-1-3 | Initial setup completed | ☐ |
| 1-1-4 | ServiceNow Dev instance requested and ready | ☐ |
| 1-1-5 | User role changed to Admin | ☐ |
| 1-1-6 | Admin credentials noted | ☐ |
| 1-1-7 | Logged in to ServiceNow instance as Admin | ☐ |
| 1-1-8 | Four default Knowledge Bases confirmed | ☐ |
| 1-1-9 | New connection added in M365 Admin Center | ☐ |
| 1-1-10 | Connection settings configured | ☐ |
| 1-1-11 | Authentication completed (green check marks visible) | ☐ |
| 1-1-12 | User access permissions set to "Everyone" | ☐ |
| 1-1-13 | Connection created successfully | ☐ |
| 1-1-14 | Connector description added | ☐ |
| 1-1-15 | Indexed content verified via Microsoft Search | ☐ |
| 1-1-16 | M365 Copilot prompts tested (optional) | ☐ |

---

## Troubleshooting

| Issue | Solution |
|---|---|
| "Sign in" button not appearing | Wait a moment — this is a known UI bug. The button will appear shortly. |
| "Create" button remains disabled | Click to the Users tab and back to trigger button activation. |
| "Auto suggestion" does nothing | Add description manually after connection reaches "Ready" state. |
| Connector returns errors when querying | Verify the ServiceNow instance is not hibernating — log in directly first. |
| Instance reclaimed by ServiceNow | Re-request a new instance and reconfigure the connector. |
| Items indexed count is 0 after sync | Wait up to 2 hours for first sync. Run a full crawl if still 0 after that. |

For additional troubleshooting, refer to:  
[Troubleshooting the ServiceNow Knowledge Microsoft Copilot connector — Microsoft Learn](https://learn.microsoft.com/en-us/microsoftsearch/troubleshoot-servicenow-knowledge-connector)

---

## Related Resources

- Step-by-Step Deployment Guide → [`3.Step-by-Step-Guide.md`](./3.Step-by-Step-Guide.md)
- Phase 1 — Add HR Documents to ServiceNow KB → [`3.Step-by-Step-Guide.md#step-1-2`](./3.Step-by-Step-Guide.md#step-1-2-add-hr-documents-to-servicenow-knowledge-base)
- https://developer.servicenow.com
- https://admin.microsoft.com
- https://learn.microsoft.com/en-us/microsoftsearch/troubleshoot-servicenow-knowledge-connector
