---
lab:
  title: Exercise - Verify and audit AI agent access
  module: Secure AI agent identities
  description: Review the AI agent's enterprise application configuration, verify API permissions, audit role assignments, and rotate credentials.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - Enterprise applications
    - API permissions
    - Activity logs
    - Credential management
    - Identity monitoring
---

# Lab 2 - Exercise 3 - Verify and audit AI agent access

Your organization's AI agent identity has been configured with API permissions and Azure RBAC roles. Before the agent goes into production, you need to verify its configuration is correct, confirm that access changes are being recorded, and ensure credentials can be rotated safely. As the identity administrator, you'll review the enterprise application's permissions, audit role assignment activity, and practice credential rotation.

**Tasks**:

1. Review the agent's API permissions and consent status
1. Review the enterprise application properties
1. Review Azure activity logs for role assignments
1. Rotate the AI agent's client secret

## Task 1 – Review the agent's API permissions and consent status

When an application identity is configured with API permissions, those permissions appear on the enterprise application's permissions blade. In this task, you'll verify that the AI agent's permissions are configured correctly and review the consent status.

1. Open **Microsoft Edge**, then navigate to `https://entra.microsoft.com/`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the left sidebar, under **Entra ID**, expand **Applications**, then select **Enterprise applications**.

1. In the search field, enter `Contoso-AI-Agent`, then select the application.

1. In the left sidebar, expand **Security**, then select **Permissions**.

1. On the **Permissions** page, review the permissions listed. You should see **User.Read.All** under **Microsoft Graph** with a consent status of **Not granted**.

    > **Note**: The "Not granted" status means this permission is configured but not yet active. In a production environment, a Global Administrator would review and grant admin consent before the agent can use this permission. This consent workflow is a critical security checkpoint — it prevents applications from accessing data without explicit approval.

1. Note the distinction between the permissions listed here and the RBAC roles assigned in the Azure portal. API permissions (shown here) control access to data through APIs. RBAC roles (assigned on individual Azure resources) control access to Azure infrastructure.

You've successfully verified the AI agent's API permission configuration and consent status.

## Task 2 – Review the enterprise application properties

The enterprise application's properties control how the service principal behaves in your tenant. In this task, you'll review key settings that affect the agent's sign-in behavior and access controls.

1. In the left sidebar, expand **Manage**, then select **Properties**.

1. On the **Properties** page, review the following settings:

   - **Enabled for users to sign-in**: Yes
   - **Assignment required**: No

    > **Note**: When **Assignment required** is set to **No**, any user or service in the tenant can obtain tokens for this application. In a production environment, setting this to **Yes** restricts token issuance to only explicitly assigned users or groups — an important control for limiting which identities can act as or through the agent.

1. Consider whether this configuration would allow unrestricted token issuance for the AI agent, and when you would change **Assignment required** to **Yes**.

You've successfully reviewed the enterprise application properties for the AI agent.

## Task 3 – Review Azure activity logs for role assignments

Azure activity logs capture management operations on Azure resources, including role assignments. In this task, you'll verify that the RBAC role assignments granted to the AI agent's service principal were recorded.

1. Open a new tab and navigate to `https://portal.azure.com`.

1. In the search bar at the top of the Azure portal, enter `Activity log`, then select **Activity log** from the results.

1. On the **Activity log** page, set the **Timespan** filter to **Last 1 hour**.

1. In the **Operation** filter, search for and select `Create role assignment`, then select **Apply**.

1. Review the log entries. You should see entries for role assignment operations on the Foundry resource and Key Vault.

1. Select one of the **Create role assignment** entries to view its details.

1. Review the **Summary** tab, noting the resource, operation, and status.

    > **Note**: Use API permissions to understand what data an identity can access, and activity logs to understand what actions it has taken. Together, these provide full visibility into an application identity's access and behavior.

You've successfully verified that role assignments to the AI agent identity are recorded in Azure activity logs.

## Task 4 – Rotate the AI agent's client secret

Client secrets expire and can be compromised. When either happens, you need to rotate credentials without disrupting the agent's operations. In this task, you'll create a new client secret, verify both secrets are active during the overlap period, then delete the old secret — following the recommended rotation workflow.

1. Navigate back to `https://entra.microsoft.com/`.

1. In the left sidebar, under **Entra ID**, expand **Applications**, then select **App registrations**.

1. Select **Contoso-AI-Agent**.

1. In the left sidebar, under **Manage**, select **Certificates & secrets**.

1. On the **Client secrets** tab, confirm you see the existing secret (**AI agent authentication**).

1. Select **+ New client secret**.

1. In the **Add a client secret** flyout, enter:

   - **Description**: `Rotated agent credential`
   - **Expires**: **180 days (6 months)**

1. Select **Add**.

1. Verify that both secrets are now listed — the original and the newly created one.

    > **Note**: During a production rotation, this overlap period is critical. The new credential must be distributed to all consumers (the agent's hosting environment, Key Vault, deployment pipelines) before the old one is removed. Deleting the old secret prematurely will break authentication.

1. On the original **AI agent authentication** secret, select the delete icon, then confirm the deletion.

1. Verify that only the **Rotated agent credential** secret remains.

You've successfully rotated the AI agent's client secret following the recommended workflow: create new, verify overlap, remove old.
