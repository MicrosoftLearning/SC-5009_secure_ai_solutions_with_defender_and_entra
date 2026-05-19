---
lab:
  title: Exercise - Configure permissions for AI workloads
  module: Secure access for AI workloads
  description: Configure API permissions and assign Azure RBAC roles to an AI workload application identity.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - API permissions
    - Azure RBAC
    - Service principals
    - Microsoft Foundry
    - Azure Key Vault
---

# Lab 2 - Exercise 2 - Configure permissions for AI workloads

Your organization's AI workloads use an application identity named **Contoso-AI-App**, registered in Microsoft Entra ID. These workloads need to access Azure AI services, read secrets from Key Vault, and query data from Microsoft Graph. By default, a registered application identity has no permissions. As the identity administrator, you'll configure API permissions and Azure RBAC roles to grant only the access required. This process applies to application identities that run without user interaction.

> **Note**: Application identities use two types of permissions. **API permissions** control access to data through APIs like Microsoft Graph. **Azure RBAC roles** control access to Azure resources such as Foundry and Key Vault. Most AI workloads require both

**Tasks**:

1. Add API permissions for the application
1. Grant the application access to the Foundry resource
1. Grant the application access to Key Vault

## Task 1 – Add API permissions for the application

The application needs access to Microsoft Graph to retrieve user profile data. In this task, you'll add an application-level API permission to allow access without user sign-in.

1. Open **Microsoft Edge**, then navigate to `https://entra.microsoft.com/`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the left sidebar, under **Entra ID**, select **App registrations**.

1. Select **Contoso-AI-App**.

1. In the left sidebar, under **Manage**, select **API permissions**.

1. Select **+ Add a permission**.

1. On the **Request API permissions** flyout, select **Microsoft Graph**.

1. Select **Application permissions**.

1. In the search field, enter `User.Read.All`, then check the **User.Read.All** permission.

1. Select **Add permissions**.

1. Back on the **API permissions** page, review the permissions list. You should see **User.Read.All** listed under **Microsoft Graph** with a status of **Not granted**.

    > **Note**: This permission requires admin consent before it can be used. In a production environment, a Global Administrator or Privileged Role Administrator grants consent. The "Not granted" status means the permission is configured but not yet active. This acts as a security checkpoint to prevent access without approval.

You've successfully configured an API permission. At this point, the application can request access to Microsoft Graph, but it cannot access Azure resources until RBAC roles are assigned.

## Task 2 – Grant the application access to the Foundry resource

The application needs access to Azure AI services hosted in your Foundry resource. In this task, you'll assign the Cognitive Services User role to the application's service principal. This allows inference access without granting management permissions.

1. Open a new tab and navigate to `https://portal.azure.com`.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. In the resource group, select the resource with the type **Foundry**.

1. Select **Access control (IAM)** from the left panel.

1. Select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Cognitive Services User`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for `Contoso-AI-App`, then select the application, then select **Select**.

1. Select **Next**, then on the **Review + assign** tab, select **Review + assign**.

1. You should see a notification indicating you successfully added the role assignment.

You've successfully granted the application access to Azure AI services on the Foundry resource.

## Task 3 – Grant the application access to Key Vault

The application retrieves configuration secrets from Azure Key Vault. In this task, you'll assign the Key Vault Secrets User role to the application's service principal, providing read-only access to secrets.

1. Navigate back to the **rg-foundry-lab** resource group.

1. Select the **Key vault** resource.

1. Select **Access control (IAM)**, then select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Key Vault Secrets User`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for `Contoso-AI-App`, then select the application, then select **Select**.

1. Select **Next**, then on the **Review + assign** tab, select **Review + assign**.

1. You should see a notification indicating you successfully added the role assignment.

You've successfully granted the application read access to secrets in Azure Key Vault.
