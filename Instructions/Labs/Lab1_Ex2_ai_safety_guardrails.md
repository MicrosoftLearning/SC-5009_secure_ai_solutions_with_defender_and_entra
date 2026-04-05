# Lab 1 - Exercise 2 - AI safety and guardrails

As a cloud security administrator, you need to configure content safety controls to prevent AI services from processing or generating harmful content. In this exercise, you'll create and manage blocklists in Azure AI Content Safety, then configure and refine content filters to enforce organizational policies.

**Tasks**:

1. Create and manage blocklists
1. Configure and refine content filters

## Task 1 – Create and manage blocklists

In this task, you'll create a custom blocklist in Azure AI Content Safety to block specific terms and phrases from AI interactions.

1. Open **Microsoft Edge**, then navigate to `https://portal.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the search bar, search for and select **Azure AI Content Safety**.

1. Select your Content Safety resource.

1. In the left navigation, select **Blocklists**.

1. Select **+ Create blocklist**.

1. Enter a **Name** for the blocklist, such as `restricted-terms`.

1. Optionally, add a **Description** for the blocklist.

1. Select **Create**.

1. Select the newly created blocklist to open it.

1. Select **+ Add term**.

1. Enter a term or phrase you want to block, then select **Add**.

1. Repeat the previous step to add additional terms as needed.

1. Review the blocklist to confirm your terms have been added.

## Task 2 – Configure and refine content filters

In this task, you'll configure content filtering settings for your AI deployment, adjusting severity thresholds and applying your custom blocklist to enforce content safety policies.

1. In the Azure portal, navigate to your **Azure AI Foundry** resource.

1. In the left navigation, select **Content filters**.

1. Select **+ Create content filter**.

1. Enter a **Name** for the content filter configuration, such as `organization-content-policy`.

1. Under **Input filter**, review the category filters (Hate, Sexual, Violence, Self-harm) and adjust the severity thresholds based on your organizational policy.

1. Under **Output filter**, review and adjust the category filters for generated content.

1. Under **Blocklists**, select **+ Add blocklist**.

1. Select the `restricted-terms` blocklist you created in Task 1.

1. Select **Create** to save the content filter configuration.

1. Apply the content filter to a model deployment by navigating to **Deployments**, selecting a deployment, and associating the content filter.

1. Test the deployment by sending a prompt that includes a blocked term, and verify the request is filtered.
