---
lab:
  title: Exercise - Enable data security protections for AI workloads
  module: Secure AI workloads
  description: Enable Microsoft Defender for Cloud protections for AI services and configure data security settings for AI interactions.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Defender for Cloud
    - Microsoft Defender
    - AI workload security
---

# Lab 1 - Exercise 1 - Enable data security protections for AI workloads

Your organization is deploying AI solutions using Azure AI Foundry and needs to ensure these workloads are protected from day one. As the cloud security administrator, you've been asked to enable threat detection for AI services, restrict who can access Foundry resources, and enforce least-privilege access at the project level so that only the right people can work with sensitive AI models and data.

**Tasks**:

1. Enable protections for AI workloads
1. Control access to AI workloads using Microsoft Entra ID
1. Manage access within Foundry projects

## Task 1 – Enable protections for AI workloads

Before configuring access controls, you need to make sure threats to your AI services are being detected. In this task, you'll enable Microsoft Defender for Cloud protections and data security controls for AI interactions at the subscription level.

1. Open **Microsoft Edge**, then navigate to `https://portal.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. Select **Microsoft Defender for Cloud** on the Microsoft Azure home page.

1. Expand **Management** then select **Environment settings**.

1. On the **Environment settings** page, select the subscription you want to configure.

1. On the **Defender plans** page, select **On** for **AI services**.

1. Under **Monitoring coverage** select **Settings** for the AI Services plan.

1. Select **On** for **Enable data security for AI interactions**.

1. Select **Continue** to save your settings.

1. Select **Save** to enable the AI Service protection plan.

1. Verify the AI services plan shows as **On** on the Defender plans page.

You've successfully enabled protection for AI workloads in Microsoft Defender for Cloud.

## Task 2 – Control access to AI workloads using Microsoft Entra ID

With threat detection in place, you need to control who can access the Foundry resource. In this task, you'll use Azure RBAC to assign the Azure AI Developer role to a group at the resource level.

1. Navigate back to the home page of your Azure subscription.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. In the resource group, select the resource with the type **Foundry**.

1. Select **Access control (IAM)** from the left panel of your Foundry resource.

1. Select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Azure AI Developer`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for and select `Accounting Contributors`, then select **Select**.

1. On the **Add role assignment** page, select **Next**.

1. On the **Review + assign** tab, select **Review + assign**.

1. On the **Access control (IAM)** page, select the **Role assignments** tab.

1. You should see a notification indicating you successfully added the role assignment.

You've successfully assigned the Azure AI Developer role to a group on your Foundry resource using Microsoft Entra ID.

## Task 3 – Manage access within Foundry projects

You've granted access at the resource level, but not everyone needs access to everything. In this task, you'll use the Foundry portal to assign a role at the project level, giving a specific user just enough access to work within a single project.

1. In **Microsoft Edge**, navigate to `https://ai.azure.com`.

1. In Microsoft Foundry, on the left sidebar, scroll down to the bottom to select the **Management center**.

1. In the Management center, under **Resource**, select **Users**.

  You should see the **Accounting Contributors** group with the **Azure AI Developer** role you added in a previous task.

1. In the Management center, under **Project** select **Users**.

1. On the **Manage users in this project** page, select **+ New user**.

1. In the **Add resource users** dialogue, enter, then select `Accounting-1223`.

1. In the **Role** dropdown, select **Azure AI User**.

1. Select **Add**.

1. You should see the **Accounting-1223** user assigned to the **Azure AI User** role.

You've successfully assigned project-level access to a user in Microsoft Foundry.
