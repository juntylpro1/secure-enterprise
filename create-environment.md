---

copyright:

  years: 2023

lastupdated: "2023-12-06"

keywords: environment, add environment, deployment environment

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Creating an environment
{: #create-env}

Within your project, create an environment to group related configurations together and share values across them for easier deployments. The properties that you add to an environment are automatically added to configurations that are using that environment. Within the configuration, you can override any values that are provided by the environment. For more information, see the [benefits to using environments](/docs/secure-enterprise?topic=secure-enterprise-best-practices-projects#best-practice-env).
{: shortdesc}

When you edit a configuration, you can select an environment for the configuration to use in the **Define details** section. 
{: tip}

## Before you begin
{: #prereq-env}

You must have the Editor role or greater on the {{site.data.keyword.cloud}} Projects service to create and edit environments. For more information about access and permissions, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

## Creating an environment by using the console
{: #create-env-ui}

To create an environment from your project, complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **[Projects](/projects/)** and select a project. 
1. From the Manage tab, select **Environments**. 
1. Click **Create**. 
1. Provide a name for your environment, then click **Add** to add properties. 

There are three categories of properties that you can add to an environment: authentication, compliance, and input. You can add these properties manually, or add multiple properties at once from a configuration in your project. 

### Adding properties manually 
{: #add-prop-manually}

If you add properties manually, consider adding the authentication method first. The authentication method for your target account is required to authorize a deployment to that target account. The authentication method is also used if you want to pull in a {{site.data.keyword.compliance_short}} attachment from your target account. You can add only one authentication property to an environment, and you can only add a compliance property to an environment if you have a {{site.data.keyword.compliance_short}} attachment in your target account that you want to use. You can't add a compliance property that uses the [default controls from the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#cra-validate-failure), as those default controls vary from architecture to architecture.

You must provide an authentication property in your environment first with valid authentication details if you want to add a compliance property and specify an attachment from {{site.data.keyword.compliance_short}}.
{: important}

Authentication and compliance information is used in all configurations, so if you add an authentication property or a compliance property with a {{site.data.keyword.compliance_short}} attachment to your environment, it is automatically added to any configuration that's using the environment.

Input values can also be added as properties to your environment. When you add an input to an environment, the name of your input in the environment must match the name of the input in the configurations that are using the environment. If the names do not match, the value from the environment is not used in the configuration. For example, if you add an input to your environment and name it `resource_group`, but a configuration that is using that environment has an input that is named `resourcegroup` the value from the environment is not used in that configuration. 

Multiple architectures can use the same environment, but not all architectures have the same input names for similar values. You can add multiple inputs to your environment with the same value, but different names. For example, you can add two input properties and name one `resource_group` and the other `resourcegroup`. Keep the values the same for both properties. Any configuration that's using the environment and has a `resource_group` input name or a `resourcegroup` input name will use the same value from the environment. 

To add a property manually, complete the following steps: 

1. After you create your environment, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") for the environment.
1. Click **Add** > **Add manually...**
1. Select which category of property you want to add. 

   Consider adding an authentication property first with valid authentication details for your target account.
   {: remember}

1. Provide the details for the property and click **Add**. 
1. Click **Save**. 

### Adding properties from a configuration
{: #add-from-config}

Save time and reduce errors by adding multiple properties to your environment from a configuration. By doing so, you help ensure that the properties are accurate in your environment, as the input names and values are pulled directly from the configuration that you select. After you add the properties from a configuration, you can edit them in the environment without affecting your configuration. Future edits to your configuration do not impact the properties in your environment. 

To add multiple properties from a configuration, complete the following steps: 

1. After you create your environment, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") for the environment. 
1. Click **Add** > **Add from a configuration…**
1. Select the configuration that you want to use to add properties to your environment. 
1. Select the items from the configuration that you want to add to your environment, and click **Add**. 

<!-- 1. Optionally, select **Edit this configuration to use the environment** if you want the configuration to use this environment. If selected, your configuration must be revalidated.  -->

<!-- You can create a project by going to the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") and selecting  or from a deployable architecture in the [catalog](/catalog/). Projects can also be created by using the [Project API](https://{DomainName}/apidocs/projects).

## Adding users to a project by using the console
{: #add-users-project}
{: ui}

Project access is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). You add users to a project by granting the Reader role or higher on the project instance. For more information on assigning access to projects, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

## Adding deployable architecture to a project by using the console
{: #add-deployment-project}
{: ui}

Deployable architectures that you add to a project are represented as configurations in the project UI. After you add a deployable architecture to a project, you can edit your configuration before you deploy it. There are a couple of ways to add a deployable architecture to your project.

To add a deployable architecture to your project from the project dashboard, complete the following steps:

1. From the project dashboard, select the Configurations tab.
1. Click **Create**.
1. Select a deployable architecture from the catalog.
1. Click **Review deployment options**.
1. Click **Add to project**. 

You can also add a deployable architecture to a project directly from the catalog:

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](/catalog).
1. Select the deployable architecture.
1. Click **Review deployment options**. 
1. Click **Add to project**.
1. You can create a new project or add to an existing project.
1. Enter the required details for the deployable architecture.
1. Click **Add**.

Check out the steps on how to [configure and deploy a deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project) when you're ready to deploy resources from a deployable architecture from a project.



## Exporting the project JSON by using the console
{: #json-export}
{: ui}

As a user that’s working with projects, you can export the project JSON to manually manage the project in your own public or private repository. For example, you might want to push updates to the JSON by calling the project API using CLI commands or by using your own CICD tools. You might also export the JSON as a way to backup the project information outside of the {{site.data.keyword.cloud_notm}} Projects service.

To export the project JSON, complete the following steps:
1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
1. From the project dashbaord, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Export JSON**
1. From the modal, click **Export**.

For more information about the project JSON, see [Project JSON](/docs/secure-enterprise?topic=secure-enterprise-json-project).



## Creating a project by using the CLI
{: #create-project-cli}
{: cli}

To create a project by using the CLI, run the following `ibmcloud project create` command:

```sh
ibmcloud project create --resource-group RESOURCE-GROUP --location LOCATION --name NAME [--description DESCRIPTION] [--destroy-on-delete DESTROY-ON-DELETE]
```
{: codeblock}

For example, the following command creates a project that is named `My new project` with the `The purpose of my new project.` description:

```sh
ibmcloud project create --resource-group Default --location us-south --name My new project --description The purpose of my new project.
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project create`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli#project-cli-create-command).

## Adding deployable architecture to a project by using the CLI
{: #add-deployment-project-cli}
{: cli}

To add a deployable architecture to your project by using the CLI, run the following `ibmcloud project config-create` command:

```sh
ibmcloud project config-create --project-id PROJECT-ID --name NAME --locator-id LOCATOR-ID [--id ID] [--labels LABELS] [--description DESCRIPTION] [--authorizations AUTHORIZATIONS] [--compliance-profile COMPLIANCE-PROFILE] [--input INPUT] [--setting SETTING]
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project config-create`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli#project-cli-config-create-command).

## Setting the JSON output format by using the CLI
{: #json-format-cli}
{: cli}

By using the following `--output json` option on the command line, you can set the output of a command to JSON: 

```sh
--output json
```
{: codeblock}

## Creating a project by using the API
{: #create-project-api}
{: api}

Projects API is a beta release that is currently available for evaluation and testing purposes.
{: beta}

You can programmatically create a project by calling the [Projects API](/apidocs/projects#create-project){: external} as shown in the following sample request. The example creates a project with the name `My new project`:

```bash
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \ 
  --data '{"name": "My new project", "description": "A microservice to deploy on top of ACME infrastructure", "configs": [{"labels": [], "output": [{"name": "id"},{"name": "crn"}], "input": [{"name": "ibmcloud_api_key", "type": "password", "required": false, "default": "__NOT_SET__", "value": "1234567"},{"name": "image_id", "type": "string", "required": false, "default": "r134-ab47c72d-b11c-417b-a442-9f1ca6a6f5ed"},{"name": "machine_type", "type": "string", "required": false, "default": "cx2-32x64"},{"name": "name", "type": "string", "required": true, "default": "solution"}], "name": "my config", "type": "schematics_blueprint", "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.0997e7ee-d387-497f-aba5-aafa80fa0f74-global", "description": "vpc solution"}}' \
  "{base_url}/v1/projects?resource_group=Default&location=us-south"
```
{: curl}
{: codeblock}

## Adding deployable architecture to a project by using the API
{: #add-deployment-project-api}
{: api}

Projects API is a beta release that is currently available for evaluation and testing purposes.
{: beta}

You can programmatically add a deployable architecture to an existing project by calling the [Projects API](/apidocs/projects#create-config){: external} and customizing the configuration as shown in the following sample request. The example adds a deployable architecture with the name `My example deployable architecture` to a project called `My existing project`:

```bash
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
   --header "Accept: application/json" \ 
   --header "Content-Type: application/json" \
   --data '{"name": "env-stage", "description": "Stage environment configuration.
", "labels": ["env:stage", "governance:test", "build:0"], "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global", "input": [{"name": "account_id", "type": "string", "value": "$configs[].name["account-stage"].input.account_id"}, {"name": "resource_group", "type": "string", "value": "stage"}, {"name": "access_tags", "type": "array", "value": ["env:stage"]}, {"name": "logdna_name", "type": "string", "value": "name of the LogDNA stage service instance"}, {"name": "sysdig_name","type": "string", "value": "name of the SysDig stage service instance"}], "setting": [{"name": "IBMCLOUD_TOOLCHAIN_ENDPOINT", "value": "https://api.us-south.devops.dev.cloud.ibm.com"}]}' \  
"{base_url}/v1/projects/1rge0328-0df9-4c88-8cd7-5602447qf3c7/configs"
```
{: curl}
{: codeblock}
 -->
