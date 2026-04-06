---
lab:
  title: Exercise - AI safety and guardrails
  module: Secure AI workloads
  description: Create blocklists and configure content filters in Microsoft Foundry to control what AI deployments can accept and produce.
  duration: 15 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Foundry
    - Content filters
    - Blocklists
---

# Lab 1 - Exercise 2 - AI safety and guardrails

Your organization's compliance team has flagged that AI services must not process or generate content containing confidential project codenames, internal product terms, or restricted phrases. As the cloud security administrator, you need to create blocklists to enforce these restrictions and configure content filters to control what your AI deployments can accept and produce.

**Tasks**:

1. Create and manage blocklists
1. Configure and refine content filters

## Task 1 – Create and manage blocklists

The compliance team has provided a list of terms that should never appear in AI interactions. In this task, you'll create a blocklist in Microsoft Foundry to prevent those terms from being processed or generated.

1. Open **Microsoft Edge**, then navigate to `https://ai.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. Select the available Foundry project.

1. In the left sidebar, under **Protect and govern**, select **Guardrails + controls**.

1. On the **Guardrails + controls** page, select the **Blocklists** tab.

1. Select **+ Create blocklist**.

1. On the **Create a blocklist** page, enter:

   - **Name**: `ConfidentialProjectTerms`
   - **Description**: `Blocks internal codenames and confidential product terms.`

1. Select **Create blocklist**.

1. Select the newly created blocklist to open it.

1. Select **+ Add new term**.

1. Ensure **Exact match** is selected, then enter `ProjectNova`, then select **Add term**.

1. Continue the process to enter these **Exact match** terms:

   - `Starlight`
   - `Orion-x`

1. Select **+ Add new term**, then select **Regex**.

1. Enter `Contoso\w+`, then select **Add term**.

    > **Note**: This regex pattern matches any term starting with "Contoso" followed by one or more characters, like "ContosoVault" or "ContosoSecure". Using a regex pattern lets you block variations without adding each one individually.

1. Review the blocklist to confirm your terms have been added.

You've successfully created a blocklist to prevent restricted terms from being used in AI interactions.

## Task 2 – Configure and refine content filters

With the blocklist in place, you now need to set up broader content filtering. In this task, you'll create a content filter configuration that controls severity thresholds for harmful categories and applies your blocklist to a model deployment.

1. In the Microsoft Foundry portal, select the back arrow next to **ConfidentialProjectTerms** to go back to the **Guardrails + Controls** page.

1. Select the **Content filters** tab, then select **+ Create content filter**.

1. On the **Add basic information** page, in the **Name** field, enter `ContosoAIContentPolicy`.

1. Select **Next**.

1. On the **Set input filter** page, set the severity thresholds for each category:

   - **Violence**: Medium
   - **Hate**: Medium
   - **Sexual**: Medium
   - **Self-harm**: Medium

1. In the **Blocklist** section of the **Set input filter** page, toggle the feature to on.

1. Under **Select built-in or customized blocklist**, select `Profanity` and `ConfidentialProjectTerms`.

1. Select **Next**.

1. On the **Set output filter** page, set the severity thresholds for each category:

   - **Violence**: Medium
   - **Hate**: Medium
   - **Sexual**: Medium
   - **Self-harm**: Medium

1. In the **Blocklist** section of the **Set output filter** page, toggle the feature to on.

1. Under **Select built-in or customized blocklist**, select  `Profanity` and `ConfidentialProjectTerms`.

1. Select **Next**.

1. On the **Apply filter to deployments (optional)** page, select **Next**.

1. On the **Review your content filter configurations** page, review your content filter, then select **Create filter**.

You've successfully configured content filters with your compliance blocklist.
