---
lab:
  title: Exercise - Configure permissions for the AI agent
  module: Secure AI agent identities
  description: Configure API permissions and assign Azure RBAC roles to the AI agent's service principal.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - API permissions
    - Azure RBAC
    - Service principals
    - Azure AI Foundry
    - Azure Key Vault
---

# Lab 2 - Exercise 2 - Configure permissions for the AI agent

Your organization's AI agent uses an application identity named **Contoso-AI-Agent**, registered in Microsoft Entra ID. The agent needs to access Azure AI services, read secrets from Key Vault, and query user data from Microsoft Graph — but a registered identity has no permissions by default. As the identity administrator, you'll configure both API permissions and Azure RBAC roles to grant the agent only the access it needs. Unlike granting access to users or groups, you're now granting access to an application identity that runs independently — without a user signing in.

> **Note**: Application identities use two types of permissions. **API permissions** control access to data through APIs like Microsoft Graph. **Azure RBAC roles** control access to Azure resources like Foundry and Key Vault. Most AI agents need both.

**Tasks**:

1. Add API permissions for the AI agent
1. Grant the AI agent access to the Foundry resource
1. Grant the AI agent access to Key Vault

## Task 1 – Add API permissions for the AI agent

The AI agent needs to read user profile data from Microsoft Graph to personalize responses. In this task, you'll add an application-level API permission to the agent's app registration, allowing it to query user data without an interactive sign-in.

1. Open **Microsoft Edge**, then navigate to `https://entra.microsoft.com/`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the left sidebar, under **Entra ID**, select **App registrations**.

1. Select **Contoso-AI-Agent**.

1. In the left sidebar, under **Manage**, select **API permissions**.

1. Select **+ Add a permission**.

1. On the **Request API permissions** flyout, select **Microsoft Graph**.

1. Select **Application permissions**.

1. In the search field, enter `User.Read.All`, then check the **User.Read.All** permission.

1. Select **Add permissions**.

1. Back on the **API permissions** page, review the permissions list. You should see **User.Read.All** listed under **Microsoft Graph** with a status of **Not granted**.

    > **Note**: This permission requires admin consent before the agent can use it. In a production environment, a Global Administrator or Privileged Role Administrator would review and grant consent. The "Not granted" status means the permission is configured but not yet active — this is an important security checkpoint that prevents applications from accessing data without explicit approval.

You've successfully configured an API permission for the AI agent. At this point, the agent has a configured permission to access data through Microsoft Graph, but it still cannot access Azure resources until RBAC roles are assigned.

## Task 2 – Grant the AI agent access to the Foundry resource

The AI agent needs to call Azure AI services hosted in your Foundry resource. In this task, you'll assign the Cognitive Services User role to the agent's service principal, allowing it to make inference calls without granting management access.

1. Open a new tab and navigate to `https://portal.azure.com`.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. In the resource group, select the resource with the type **Foundry**.

1. Select **Access control (IAM)** from the left panel.

1. Select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Cognitive Services User`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for `Contoso-AI-Agent`, then select the application, then select **Select**.

1. Select **Next**, then on the **Review + assign** tab, select **Review + assign**.

1. You should see a notification indicating you successfully added the role assignment.

You've successfully granted the AI agent identity access to Azure AI services on the Foundry resource.

## Task 3 – Grant the AI agent access to Key Vault

The AI agent retrieves configuration secrets from Azure Key Vault at runtime. In this task, you'll assign the Key Vault Secrets User role to the agent's service principal, giving it read-only access to secrets without the ability to modify them.

1. Navigate back to the **rg-foundry-lab** resource group.

1. Select the **Key vault** resource.

1. Select **Access control (IAM)**, then select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Key Vault Secrets User`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for `Contoso-AI-Agent`, then select the application, then select **Select**.

1. Select **Next**, then on the **Review + assign** tab, select **Review + assign**.

1. You should see a notification indicating you successfully added the role assignment.

You've successfully granted the AI agent identity read access to secrets in Azure Key Vault.
