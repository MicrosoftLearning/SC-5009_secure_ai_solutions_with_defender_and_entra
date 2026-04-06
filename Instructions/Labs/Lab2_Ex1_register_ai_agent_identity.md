---
lab:
  title: Exercise - Register an application identity for an AI agent
  module: Secure AI agent identities
  description: Register an application in Microsoft Entra ID and configure authentication credentials for an AI agent that accesses Azure AI services.
  duration: 10 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Entra ID
    - App registrations
    - Service principals
---

# Lab 2 - Exercise 1 - Register an application identity for an AI agent

Your organization is building an AI agent that needs to access Azure AI services and Key Vault programmatically. Unlike interactive users who sign in with their credentials, this agent needs its own application identity to authenticate securely. As the identity administrator, you'll register the application in Microsoft Entra ID and configure its authentication credentials.

**Tasks**:

1. Register an application in Microsoft Entra ID
1. Configure authentication and identify the service principal

## Task 1 – Register an application in Microsoft Entra ID

AI agents that access Azure services independently need a registered identity in Microsoft Entra ID. In this task, you'll create an app registration that represents the agent, establishing the identity that will be used for authentication and authorization.

1. Open **Microsoft Edge**, then navigate to `https://entra.microsoft.com/`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the left sidebar, under **Entra ID**, select **App registrations**.

1. Select **+ New registration**.

1. On the **Register an application** page, enter:

   - **Name**: `Contoso-AI-Agent`
   - **Supported account types**: Leave the default **Single tenant only** option selected.

1. Leave **Redirect URI** blank.

    > **Note**: This agent authenticates using client credentials, not interactive sign-in, so it doesn't need a redirect URI. Redirect URIs are used for applications that require users to sign in through a browser.

1. Select **Register**.

You've successfully registered an application identity for the AI agent in Microsoft Entra ID.

## Task 2 – Configure authentication and identify the service principal

The app registration defines the application, but the agent needs a credential to prove its identity. In this task, you'll create a client secret for authentication, then locate the corresponding service principal — the identity object that gets assigned roles and permissions.

1. On the **Contoso-AI-Agent** app registration page, in the left sidebar under **Manage**, select **Certificates & secrets**.

1. Select the **Client secrets** tab, then select **+ New client secret**.

1. In the **Add a client secret** flyout, enter:

   - **Description**: `AI agent authentication`
   - **Expires**: **180 days (6 months)**

1. Select **Add**.

1. Copy the **Value** of the newly created secret.

    > **Important**: This secret value is only displayed once. In a production environment, you would store this value securely in Azure Key Vault rather than copying it manually.

1. In the left panel under Entra ID, select **Enterprise applications**.

1. In the search field, enter `Contoso-AI-Agent`, then select the application.

1. On the **Contoso-AI-Agent** enterprise application page, confirm the application is listed.

    > **Note**: The app registration defines what the application is. The enterprise application is the service principal — the identity object in your tenant that gets assigned roles and permissions. When you grant access to Azure resources, you assign roles to this service principal.

You've successfully configured authentication credentials and identified the service principal for the AI agent.
