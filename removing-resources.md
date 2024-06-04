---

copyright:

  years: 2023

lastupdated: "2023-07-06"

keywords: manage project, destroy resources, remove resources, resource, resources, delete resources, Terraform resources, Terraform workspace

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Removing deployed resources
{: #remove-resources}

Deploying an architecture creates resources that can incur costs in the target account that you deployed to. Destroying the resources that were created removes them from that target account, and can help reduce costs for your business.
{: shortdesc}

Destroying the resources that were deployed by a configuration returns the configuration to draft status. You can deploy the architecture configuration again, if you need to.
{: note}

## Removing deployed resources from a project by using the console
{: #delete-resource-without-project}
{: ui}

You can destroy deployed resources without deleting the project or configuration that deployed those resources. Doing so can be useful if you no longer need the resources in the target account that you deployed to, but want to keep the project or configuration to use again for future deployments. Complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
1. Select the project that contains the configuration that deployed the resources that you want to remove.
1. On the **Configurations** tab, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Destroy resources** for the configuration.
1. Enter the name of the configuration into the required field.

    Make sure that you want to destroy the resources, as this action can't be undone. While you can re-create the resources based on the current configuration, any cached data or persisted data is destroyed.
    {: important}

1. Click **Destroy**.

## Deleting a project and all of its deployed resources by using the console
{: #delete-and-remove-resources}
{: ui}

By default, when you delete a project or a configuration, any resources that were deployed are destroyed automatically. Confirm that this setting is enabled by opening your project and going to **Manage** > **Settings** before you delete your project or configuration. If this setting is disabled, when you delete your project or configuration, the resources remain deployed, but you lose the ability to manage them easily with your project. Deployed resources continue accruing costs in your target account.
{: important}

If you no longer need a project and want to remove any architectures that were deployed by configurations in your project, delete the project and destroy any Terraform resources that were created. Complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete project** for the project that you want to delete.
1. Enter the project name into the required field.

    Make sure that you want to delete the project, as this action can't be undone.
    {: important}

1. Click **Delete**.

## Deleting a configuration and all of its deployed resources by using the console
{: #delete-and-remove-config}
{: ui}

By default, when you delete a project or a configuration, any resources that were deployed are destroyed automatically. Confirm that this setting is enabled by opening your project and going to **Manage** > **Settings** before you delete your project or configuration. If this setting is disabled, when you delete your project or configuration, the resources remain deployed, but you lose the ability to manage them easily with your project. Deployed resources continue accruing costs in your target account.
{: important}

If you no longer need a configuration and want to remove any architectures that were deployed by it, delete the configuration and destroy any resources that were created. Complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
1. Select the project that contains the configuration that you want to delete.
1. On the **Configurations** tab, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete** for the configuration that you want to delete.
1. Enter the name of the configuration into the required field.

    Make sure that you want to delete the configuration, as this action can't be undone.
    {: important}

1. Click **Delete**.

 

## Removing deployed resources from a project by using the CLI
{: #delete-resource-without-project-cli}
{: cli}

To delete deployed resources by using the CLI without deleting the project or configuration that deployed those resources, run the following `ibmcloud project config-uninstall` command:

```sh
ibmcloud project config-uninstall --project-id PROJECT-ID --id ID
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project config-uninstall`**](/docs/cli?topic=cli-projects-cli#project-cli-config-undeploy-command).

## Deleting a project and all of its deployed resources by using the CLI
{: #delete-and-remove-resources-cli}
{: cli}

To delete a project by using the CLI and destroy any resources that were created, run the following `ibmcloud project delete` command:

```sh
ibmcloud project delete --id ID [--destroy DESTROY]
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project delete`**](/docs/cli?topic=cli-projects-cli#project-cli-delete-command).

## Deleting a configuration and all of its deployed resources by using the CLI
{: #delete-and-remove-config-cli}
{: cli}

To delete a configuration by using the CLI and destroy any resources that were created, run the following `ibmcloud project config-delete` command:

```sh
ibmcloud project config-delete --project-id PROJECT-ID --id ID [--draft-only DRAFT-ONLY] [--destroy DESTROY]
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project config-delete`**](/docs/cli?topic=cli-projects-cli#project-cli-config-delete-command).

## Removing deployed resources from a project by using the API
{: #delete-resource-without-project-api}
{: api}

Projects API is a beta release that is currently available for evaluation and testing purposes.
{: beta}

You can programmatically destroy configuration resources from a project by calling the [Projects API](/apidocs/projects#undeploy-config){: external} as shown in the following sample request. The example deletes resources deployed by a configuration with the ID `0df9-5602447qf3c7-8cd7-1rge0328-4c88` from a project with the ID `1rge0328-0df9-4c88-8cd7-5602447qf3c7`: 

```bash
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  --data '' \
  "{base_url}/v1/projects/1rge0328-0df9-4c88-8cd7-5602447qf3c7/configs/0df9-5602447qf3c7-8cd7-1rge0328-4c88/uninstall"
```
{: curl}
{: codeblock}

## Deleting a configuration and all of its deployed resources by using the API
{: #delete-and-remove-config-api}
{: api}

Projects API is a beta release that is currently available for evaluation and testing purposes.
{: beta}

You can programmatically delete a configuration in a project and all of its deployed resources by calling the [Projects API](/apidocs/projects#delete-config){: external} as shown in the following sample request. The example deletes a configuration with the ID `0df9-5602447qf3c7-8cd7-1rge0328-4c88` from a project with the ID `1rge0328-0df9-4c88-8cd7-5602447qf3c7`:

```bash
curl -X DELETE --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \  
  --header "Content-Type: application/json" \  
  "{base_url}/v1/projects/1rge0328-0df9-4c88-8cd7-5602447qf3c7/configs/0df9-5602447qf3c7-8cd7-1rge0328-4c88?draft_only=false"
```
{: curl}
{: codeblock}
