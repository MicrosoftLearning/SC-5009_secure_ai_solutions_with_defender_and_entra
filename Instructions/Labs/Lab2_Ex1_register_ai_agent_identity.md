---
lab:
  title: Exercise - Register an application identity for AI workloads
  module: Secure access for AI workloads
  description: Register an application identity in Microsoft Entra ID to allow AI workloads to securely access Azure services.
  duration: 10 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Entra ID
    - App registrations
    - Service principals
---

# Lab 2 - Exercise 1 - Register an application identity for AI workloads

Your organization is deploying AI workloads that interact with Azure AI services and supporting resources such as Key Vault. These workloads run without user interaction, so they require their own application identity for secure authentication. As the identity administrator, you'll register an application in Microsoft Entra ID and configure credentials that enable the workload to authenticate securely.

**Tasks**:

1. Register an application in Microsoft Entra ID
1. Configure authentication and identify the service principal

## Task 1 – Register an application in Microsoft Entra ID

AI workloads that access Azure services without user interaction need their own application identity in Microsoft Entra ID. In this task, you'll create an app registration that represents the workload and enables it to authenticate and access resources securely.

1. Open **Microsoft Edge**, then navigate to `https://entra.microsoft.com/`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the left sidebar, under **Entra ID**, select **App registrations**.

1. Select **+ New registration**.

1. On the **Register an application** page, enter:

   - **Name**: `Contoso-AI-App`
   - **Supported account types**: Leave the default **Single tenant only** option selected.

1. Leave **Redirect URI** blank.

    > **Note**: This application uses client credentials for authentication rather than interactive sign-in, so it doesn’t require a redirect URI. Redirect URIs are used for applications that involve user sign-in through a browser.

1. Select **Register**.

You've successfully registered an application identity for the AI workload in Microsoft Entra ID.

## Task 2 – Configure authentication and identify the service principal

The app registration defines the application, but it needs credentials to authenticate. In this task, you'll create a client secret, then locate the corresponding service principal — the identity object that gets assigned roles and permissions.

1. On the **Contoso-AI-App** app registration page, in the left sidebar under **Manage**, select **Certificates & secrets**.

1. Select the **Client secrets** tab, then select **+ New client secret**.

1. In the **Add a client secret** flyout, enter:

   - **Description**: `AI workload authentication`
   - **Expires**: **180 days (6 months)**

1. Select **Add**.

1. Copy the **Value** of the newly created secret.

    > **Important**: This secret value is only displayed once. In a production environment, you would store this value securely in Azure Key Vault rather than copying it manually.

1. In the left panel under Entra ID, select **Enterprise applications**.

1. In the search field, enter `Contoso-AI-App`, then select the application.

1. On the **Contoso-AI-App** enterprise application page, confirm the application is listed.

    > **Note**: The app registration defines the application. The enterprise application is the service principal. This is the identity in your tenant that gets assigned roles and permissions. When you grant access to Azure resources, you assign roles to this service principal.

You've successfully configured authentication credentials and identified the service principal for the AI workload.
