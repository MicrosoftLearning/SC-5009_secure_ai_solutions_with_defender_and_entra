---
lab:
  title: Exercise - Configure AI project access and guardrails
  module: Secure AI workloads
  description: Configure project access, blocklists, and content filters in Microsoft Foundry.
  duration: 20 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Foundry
    - Content filters
    - Blocklists
    - Access control
---

# Lab 1 - Exercise 3 - Configure AI project access and guardrails

Your organization needs to control who can work within AI projects and enforce restrictions on what content AI deployments can process or generate. As the cloud security administrator, you'll assign project-level roles, create blocklists to block restricted terms, and configure content filters.

**Tasks**:

1. Manage access within Foundry projects
1. Create and manage blocklists
1. Configure and refine content filters

## Task 1 – Manage access within Foundry projects

Resource-level access controls who can reach the Foundry resource, but project-level access controls what they can do inside it. In this task, you'll assign a role at the project level, giving a specific user just enough access to work within a single project.

1. Open **Microsoft Edge**, then navigate to `https://ai.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In Microsoft Foundry, on the left sidebar, scroll down to the bottom to select the **Management center**.

1. In the Management center, under **Resource**, select **Users**.

   If your organization has assigned resource-level roles, you may see existing role assignments here, such as groups with the **Azure AI Developer** role.

1. In the Management center, under **Project** select **Users**.

1. On the **Manage users in this project** page, select **+ New user**.

1. In the **Add resource users** dialog, enter, then select `Accounting-1223`.

1. In the **Role** dropdown, select **Azure AI User**.

1. Select **Add**.

1. You should see the **Accounting-1223** user assigned to the **Azure AI User** role.

You've successfully assigned project-level access to a user in Microsoft Foundry.

## Task 2 – Create and manage blocklists

The compliance team has provided a list of terms that should never appear in AI interactions. In this task, you'll create a blocklist in Microsoft Foundry to prevent those terms from being processed or generated.

1. In the left sidebar, select your Foundry project to return to the project overview.

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

## Task 3 – Configure and refine content filters

With the blocklist in place, you now need to set up broader content filtering. Blocklists control specific terms, while content filters control categories of harmful content. In this task, you'll create a content filter configuration that controls severity thresholds for harmful categories and applies your blocklist.

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
