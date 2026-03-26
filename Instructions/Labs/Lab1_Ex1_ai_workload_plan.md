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

# Lab 1 - Exercise - Enable data security protections for AI workloads

As a cloud security administrator, you're preparing to secure Azure AI workloads. Before applying access controls or reviewing activity, you need to enable security protections for AI services at the subscription level. This includes turning on Defender for Cloud plans and enabling data security controls for AI interactions.

**Tasks**:

1. Enable protections for AI workloads

## Task 1 – Enable protections for AI workloads

In this task, you'll enable Microsoft Defender for Cloud protections for AI services and turn on data security controls for AI interactions at the subscription level.

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


## Exercise – Control access to AI workloads using Microsoft Entra ID

1. In Microsoft Azure, navigate to your Azure Foundry resource.

1. Select **Access control (IAM)**.

1. Select **+ Add** > **Add role assignment**.

1. On the **Add role assignment** page, under the **Job function roles** tab, search for and select `Azure AI Developer`.

1. Select **Next**.

1. On the **Members** tab, select the option for **User, group, or service principal**, then select **+ Select members**.

1. In the **Select members** flyout, search for and select `Azure AI Developer`, then select **Select**.

1. On the **Add role assignment** page, select **Next**.

1. On the **Review + assign** tab, select **Review + assign**.

1. On the **Access control (IAM)** page, select the **Role assignments** tab to review the updated access.