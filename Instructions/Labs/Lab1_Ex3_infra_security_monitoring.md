# Lab 1 - Exercise 3 - Infrastructure security and monitoring

As a cloud security administrator, you need to protect the infrastructure that supports your Azure AI workloads. In this exercise, you'll secure secrets with Azure Key Vault, isolate network traffic using managed virtual networks and private endpoints, and enable diagnostic logging to monitor AI service activity.

**Tasks**:

1. Secure Azure AI Foundry with Azure Key Vault
1. Isolate networks with managed virtual network and private link
1. Enable diagnostic logging in Azure AI Foundry

## Task 1 – Secure Azure AI Foundry with Azure Key Vault

In this task, you'll configure Azure Key Vault to store secrets used by your AI services, such as API keys and connection strings.

1. Open **Microsoft Edge**, then navigate to `https://portal.azure.com`.

1. Sign in with the username and password provided by your lab hosting provider.

1. In the search bar, search for and select **Key vaults**.

1. Select your existing key vault, or select **+ Create** to create a new one.

1. If creating a new key vault, enter the required details (subscription, resource group, name, region) and select **Review + create** > **Create**.

1. In your key vault, select **Secrets** from the left navigation.

1. Select **+ Generate/Import**.

1. Enter a **Name** for the secret, such as `ai-service-api-key`.

1. In the **Secret value** field, enter the API key for your AI service.

1. Select **Create**.

1. Navigate to your **Azure AI Foundry** resource.

1. In the left navigation, select **Settings**, then review the **Key vault** connection to confirm it references the correct key vault.

1. Verify the AI service can access secrets by reviewing the managed identity and access policies configured on the key vault.

## Task 2 – Isolate networks with managed virtual network and private link

In this task, you'll configure network isolation for your Azure AI Foundry workspace using a managed virtual network and private endpoints.

1. In the Azure portal, navigate to your **Azure AI Foundry** resource.

1. In the left navigation, select **Networking**.

1. Under **Managed virtual network**, select **Workspace managed outbound access**.

1. Review the managed virtual network settings. Select **Allow Internet Outbound** or **Allow Only Approved Outbound** based on your organizational requirements.

1. To add a private endpoint, select **+ Add user-defined outbound rules**.

1. Configure a private endpoint rule by specifying the **Service resource type**, **Resource**, and **Sub-resource** for the target Azure service.

1. Select **Save** to apply the network configuration.

1. Navigate to the **Private endpoint connections** section to verify the private endpoint status shows as **Approved**.

1. Test connectivity by accessing the AI Foundry workspace and confirming resources are accessible through the private network.

## Task 3 – Enable diagnostic logging in Azure AI Foundry

In this task, you'll configure diagnostic settings to capture logs and metrics from your Azure AI services for monitoring and auditing.

1. In the Azure portal, navigate to your **Azure AI Foundry** resource.

1. In the left navigation, under **Monitoring**, select **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. Enter a **Diagnostic setting name**, such as `ai-foundry-logs`.

1. Under **Logs**, select the log categories you want to capture (for example, **Audit**, **Request Response Logs**, **Trace Logs**).

1. Under **Metrics**, select **AllMetrics**.

1. Under **Destination details**, select **Send to Log Analytics workspace**.

1. Select the appropriate **Subscription** and **Log Analytics workspace**.

1. Select **Save**.

1. To verify logging is working, navigate to your **Log Analytics workspace**.

1. Select **Logs** in the left navigation.

1. Run a query to check for recent AI service log entries, such as:

    ```kusto
    AzureDiagnostics
    | where ResourceProvider == "MICROSOFT.COGNITIVESERVICES"
    | order by TimeGenerated desc
    | take 10
    ```

1. Review the query results to confirm diagnostic data is being collected.
