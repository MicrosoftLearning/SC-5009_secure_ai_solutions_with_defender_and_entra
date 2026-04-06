---
lab:
  title: Exercise - Enable data security protections for AI workloads
  module: Secure AI workloads
  description: Enable Microsoft Defender for Cloud protections for AI services and configure data security settings for AI interactions.
  duration: 20 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Defender for Cloud
    - Microsoft Defender
    - AI workload security
---

# Lab 1 - Exercise 1 - Enable data security protections for AI workloads

Your organization is deploying AI solutions using Azure AI Foundry and needs to ensure these workloads are protected from day one. As the cloud security administrator, you've been asked to enable threat detection for AI services, enforce security policies, and restrict who can access AI workload resources.

**Tasks**:

1. Enable protections for AI workloads
1. Implement security policies for AI services
1. Control access to AI workloads using Microsoft Entra ID

## Task 1 – Enable protections for AI workloads

Before configuring access controls, you need to establish security posture management and threat detection for your AI services. In this task, you'll enable Defender CSPM to discover AI workloads and surface security recommendations, then enable the AI services plan to add runtime threat detection and data security for AI interactions.

1. Open **Microsoft Edge**, then navigate to `https://portal.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. Select **Microsoft Defender for Cloud** on the Microsoft Azure home page.

1. Expand **Management** then select **Environment settings**.

1. On the **Environment settings** page, select the subscription you want to configure.

1. On the **Defender plans** page, select **On** for **Defender CSPM**.

1. Select **Save** to enable the Defender CSPM plan.

1. On the same **Defender plans** page, select **On** for **AI services**.

1. Under **Monitoring coverage** select **Settings** for the AI Services plan.

1. Select **On** for **Enable data security for AI interactions**.

1. Select **Continue** to save your settings.

1. Select **Save** to enable the AI Service protection plan.

1. Verify both the **Defender CSPM** and **AI services** plans show as **On** on the Defender plans page.

You've successfully enabled posture management and threat protection for AI workloads in Microsoft Defender for Cloud.

## Task 2 – Implement security policies for AI services

With Defender plans enabled, you need to enforce security requirements on your AI resources using Azure Policy. In this task, you'll assign a built-in policy that restricts network access on Azure AI Services resources, ensuring they aren't exposed to the public internet without controls.

1. In the top left of the Azure page, select **Home** to get back to the home page.

1. From the home page, select **Subscriptions**, then select your Azure subscription.

1. In the left sidebar of your Azure subscription, expand **Settings**, then select **Policies**.

1. On the **Policies** page, expand **Authoring** > **Definitions**.

1. In the **Search** field, enter `Azure AI Services`, then select the **Azure AI Services resources should restrict network access** policy.

1. On the top left of the page, select **Assign policy**.

1. On the **Basics** tab, leave the defaults selected.

1. Select **Review + create**, then select **Create**.

1. You should receive a notification indicating your policy assignment succeeded.

    > **Note**: Policy assignments can take 5–15 minutes to take effect. Once active, any Azure AI Services resource that allows unrestricted network access will be flagged as non-compliant.

You've successfully assigned a security policy to enforce network restrictions on AI services.

## Task 3 – Control access to AI workloads using Microsoft Entra ID

With protection and policies in place, you need to control who can access AI workload resources. In this task, you'll use Azure RBAC to assign the Azure AI Developer role to a group at the resource level.

1. Navigate back to the home page of your Azure subscription.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. In the resource group, select the resource with the type **Foundry**.

1. Select **Access control (IAM)** from the left sidebar of your Foundry resource.

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
