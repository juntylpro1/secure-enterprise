---

copyright:

  years: 2022, 2023

lastupdated: "2023-07-06"

keywords: manage project, rename project, move project, deploy project

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a project
{: #delete-project}

When you delete a project, destroy any resources that were deployed by configurations within the project to avoid additional costs.
{: shortdesc}

By default, when you delete a project, any resources that were deployed are destroyed automatically. Confirm that this setting is enabled by opening your project and going to **Manage** > **Settings**. If this setting is disabled and you delete your project, the resources remain deployed, but you lose the ability to manage them easily with your project. Deployed resources continue accruing costs in your target account.
{: important}

## Deleting a project by using the console
{: #delete-project-ui}
{: ui}

To delete a project, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete project** for the project that you want to delete.
3. Enter the project name into the required field.
    Make sure that you want to delete a project because after you delete a project, the action can't be undone.
    {: important}

4. Click **Delete**.

## Deleting a project by using the CLI
{: #delete-project-cli}
{: cli}

To delete a project by using the CLI, run the following `ibmcloud project delete` command:

```sh
ibmcloud project delete --id ID [--destroy DESTROY]
```
{: codeblock}

For more information about the command parameters, see [**`ibmcloud project delete`**](/docs/cli?topic=cli-projects-cli#project-cli-delete-command).

## Deleting a project by using the API
{: #delete-project-api}
{: api}

Projects API is a beta release that is currently available for evaluation and testing purposes.
{: beta}

You can programmatically delete a project by calling the [Projects API](/apidocs/projects#delete-project){: external} as shown in the following sample request. The example deletes a project with the ID `1rge0328-0df9-4c88-8cd7-5602447qf3c7`:

```bash
curl -X DELETE --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json"  \
  --header "Content-Type: application/json"  \
  "{base_url}/v1/projects/1rge0328-0df9-4c88-8cd7-5602447qf3c7"
```
{: curl}
{: codeblock}
