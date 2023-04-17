---

copyright:
  years: 2022, 2023


lastupdated: "2023-04-17"


keywords: authorizing a project, add project to account, project secrets, project API key, authenticate, authentication for a project

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Using an API key with {{site.data.keyword.secrets-manager_short}} to authorize a project to deploy an architecture
{: #authorize-project}

When you configure your deployable architecture, you are required to select an authentication method. You can use an API key that is stored as a secret to authorize a project to deploy in an account.
{: shortdesc}

A secret is a piece of sensitive information, for example an API key, password, or any type of credential that you might use to access a confidential system. You can use a secret in {{site.data.keyword.secrets-manager_full}} as a way to manage API keys dynamically and store them securely in your own dedicated instance.

Though it is possible to add your API key directly into your configuration, it is not recommended, as the API key displays in your `project.json` file and is visible to anyone who exports it.
{: important}

## Before you begin
{: #gs-prereqs}

1. Make sure that you are assigned the required permissions to create the project tooling resources within the account in addition to permission to create projects:

* The Editor role on the Project service.
* The Editor and Manager role on the {{site.data.keyword.bplong}} service.
* The Viewer role on the resource group for the project.

For more information about access and permissions, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

1. [Create a {{site.data.keyword.secrets-manager_short}} service instance](/docs/secrets-manager?topic=secrets-manager-create-instance&interface=ui) in your {{site.data.keyword.cloud_notm}} account. To create a secret, you must have the Writer role or higher on the {{site.data.keyword.secrets-manager_short}} service.

2. After you create your secret instance, make sure that you select **Other secret type** to add an arbitrary secret. For information about creating an abitrary secret, see [Creating arbitrary secrets in the UI](/docs/secrets-manager?topic=secrets-manager-arbitrary-secrets&interface=ui). Your arbitrary secret must contain the API key. The API key must be created in the target account that you want to deploy to.

3. Complete the required steps to [create a project and add a deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-setup-project). You authorize the project to deploy with an API key or existing secret when you configure your deployable architecture.

## Using an existing secret
{: #deploy-exisiting-secret}

1. In the {{site.data.keyword.cloud_notm}} console, sign in to the account that you want to deploy the project to.
1. Go to **Menu** ![Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
1. Select the project that includes the deployable architecture configuration that you want to authorize.
1. From the **Configurations** tab, select the configuration.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit**
1. In the required input section, go to the Authentication method. Make sure that **Use an existing secret** is set to **Yes**.
1. Select **API key using {{site.data.keyword.secrets-manager_short}}**.
1. Click **Select from {{site.data.keyword.secrets-manager_short}}**.
1. Choose the service instance, secret group, and secret.
1. Click **Save**.

## Adding an API key
{: #create-new-secret}

During the configuration process, you might decide to add the API key directly. This option is not recommended because the API key displays in your `project.json` file and is visible to anyone who exports it.

1. In the {{site.data.keyword.cloud_notm}} console, sign in to the account that you want to deploy to.
1. Go to **Manage** > **Access (IAM)** > **API keys**.
1. Click **Create an {{site.data.keyword.Bluemix_notm}} API key**.
1. Enter a name and description for your API key. Include the appropriate privileges.
1. Click **Create**.
1. Then, click **Show** to display the API key. Or, click **Copy** to copy and save it for later, or click **Download**.

For security reasons, the API key is only available to be copied or downloaded at the time of creation. If the API key is lost, you must create a new API key.
{: tip}

1. Go to **Menu** ![Menu icon](../icons/icon_hamburger.svg "Menu") **Projects**.
1. Select the project that includes the deployable architecture configuration you want to authorize.
1. From the **Configurations** tab, select the configuration.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit**.
1. In the required input section,make sure that the **Use an existing secret** option is set to **No**.
1. Add the API key that you copied or downloaded.
