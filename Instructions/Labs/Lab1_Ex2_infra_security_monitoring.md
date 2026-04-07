---
lab:
  title: Exercise - Secure and monitor AI workloads
  module: Secure AI workloads
  description: Secure Key Vault access, review network risks, and enable diagnostic logging.
  duration: 20 minutes
  level: 200
  islab: true
  primarytopics:
    - Azure Key Vault
    - Network isolation
    - Diagnostic logging
---

# Lab 1 - Exercise 2 - Secure and monitor AI workloads

Your organization's AI workloads depend on supporting services like Azure Key Vault for secrets management and network controls for traffic isolation. As the cloud security administrator, you need to secure these infrastructure components and enable monitoring to maintain visibility into AI service activity.

**Tasks**:

1. Connect Azure Key Vault to Microsoft Foundry
1. Identify network security risks for AI workloads
1. Enable diagnostic logging in Microsoft Foundry

## Task 1 – Connect Azure Key Vault to Microsoft Foundry

In this task, you'll grant the Foundry resource's managed identity least-privilege access to Azure Key Vault, then connect Key Vault as a resource in your Foundry project. You'll briefly switch to the Foundry portal to complete the connection.

1. Open **Microsoft Edge**, then navigate to `https://portal.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. Select the **Key vault** resource.

1. In Key Vault, go to **Access control (IAM)**, then select **Add** > **Add role assignment**.

1. On the Add role assignment page, in the **Role** tab, search for and select `Key Vault Secrets User`.

1. Select **Next**.

1. On the **Members** tab, select **Managed identity**.

1. Select **+ Select members**.

1. In the **Select managed identities** flyout, select the dropdown for **Managed identity**, then select **Foundry** from the dropdown.

1. Select the Foundry resource that appears, then select **Select**.

1. Select **Review + assign** to take you to the Review + assign tab.

1. Now that the managed identity has access to Key Vault, navigate to `https://ai.azure.com` to connect it to your Foundry project.

1. Select the available Foundry project.

1. Scroll to the bottom of the left sidebar, then select **Management center**.

1. In the left sidebar under **Resource** select **Connected resources**.

1. On the **Manage connected resources in this project** page, select **+ New connection**.

1. In the **Add a connection to external assets** dialog, search for then select `Key Vault`.

1. In the **Add an Azure Key Vault** dialog, under **Authentication**, ensure **Account managed by identity** is selected in the dropdown, then select **Add connection**.

1. Once connected, you will see a notification with a green check mark indicating the connection is successful.

1. Select **Close** to close the dialog, and you will see your Key Vault connection in your project.

## Task 2 – Identify network security risks for AI workloads

In this task, you'll identify security risks in the current networking configuration of your Key Vault and Foundry resource to understand where network isolation improvements are needed.

1. Navigate back to the Azure portal by going to `https://portal.azure.com`.

1. Select **Resource groups**, then select the **rg-foundry-lab** resource group.

1. Select the **Key vault** resource.

1. In the left sidebar, under **Settings**, select **Networking**.

1. On the **Firewalls and virtual networks** tab, note that the key vault is currently set to **Allow public access from all networks**. This means any authenticated identity on the internet can reach it.

1. Review the available options: **Allow public access from specific virtual networks and IP addresses** and **Disable public access**. In production, you would restrict access to only the virtual networks your AI workloads use.

1. Select the **Private endpoint connections** tab. Note that there are no private endpoints configured, meaning all traffic to Key Vault currently goes over the public internet.

    > **Note**: In a production environment, you would create a private endpoint for Key Vault so that Foundry communicates with it over Azure's private backbone instead of the public internet. Combined with disabling public access, this ensures only resources on your virtual network can reach the key vault.

1. Select the back arrow to return to the **rg-foundry-lab** resource group.

1. Select the **Foundry** resource.

1. In the left sidebar, under **Settings**, select **Networking**.

1. Review the network access options. Note the available configurations for controlling inbound and outbound access to the Foundry resource.

    > **Note**: In production, you would use a managed virtual network with **Allow Only Approved Outbound** to restrict which external services the Foundry resource can connect to. Combined with private endpoints on dependent resources like Key Vault and Storage, this keeps all AI workload traffic within controlled network boundaries.

1. Based on your review, identify a configuration that allows unrestricted public access or uncontrolled outbound connectivity, and determine which setting you would change to limit that exposure.

## Task 3 – Enable diagnostic logging in Microsoft Foundry

In this task, you'll configure diagnostic settings to capture logs and metrics from your Azure AI services for monitoring and auditing.

1. In the Azure portal, navigate to your **Microsoft Foundry** resource by selecting **Resource groups**, then select the **rg-foundry-lab** resource group.

1. Select the **Foundry** resource.

1. In the left sidebar, under **Monitoring**, select **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. In the **Diagnostic setting name** field, enter: `foundry-diag`.

1. Under **Logs**, select the checkbox for **Audit**.

1. Under **Destination details** select the checkbox for **Send to Log Analytics workspace**

1. Select the appropriate **Subscription** and **Log Analytics workspace**.

1. Select **Save**.

