---

copyright:

  years: 2024

lastupdated: "2024-04-03"

keywords: stack, configure stack, deployable architecture stack, stacked deployable architecture

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Stacking deployable architectures by using the CLI
{: #config-stack}

You can stack deployable architectures together in a project to create a robust end-to-end solution architecture, without coding Terraform to connect the deployable architectures together. You can add references to inputs or outputs as you configure your deployable architectures to link them together in the stack. After you deploy the deployable architectures in your stack, you can add the stack to a private catalog to easily share it with others in your organization. 
{: shortdesc}

This is an experimental feature that is available for evaluation and testing purposes and might change without notice.
{: experimental}

## Before you begin
{: #stack-prereq}

Make sure that you have the following access. For more information about access and permissions, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

* The Editor role on the {{site.data.keyword.cloud_notm}} Projects service.
* The Editor and Manager role on the {{site.data.keyword.bplong}} service
* The Viewer role on the resource group for the project

Add the deployable architectures that you'd like to stack together to your project. For more information, see [Adding deployable architectures to a project](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui#add-deployment-project).

When you add deployable architectures to your project, provide meaningful names to help identify them. For example, if your stack contains an infrastructure deployable architecture that creates the base for an application, that infrastructure needs to be deployed first. Otherwise, the application isn't able to deploy onto that infrastructure. Name your infrastructure deployable architecture `1 - infrastructure` when you add it to your project. Name the application `2 - application` to indicate it needs to be deployed second.
{: tip}

## Stacking architectures together by using the CLI
{: #stack-architectures-cli}

After you add the deployable architectures to your project, stack them together by running the following `ibmcloud project config-create` command. In the `Definition` option, specify the `members` by providing a name and the configuration ID for the existing deployable architectures that you want to include in your stack:

```sh
ibmcloud project config-create --project-id PROJECT-ID [--definition DEFINITION]
```
{: codeblock}

For example, the following command creates a deployable architecture stack that is named `StackDev` in your project. The stack contains two deployable architectures, `custom-apache` and `test-slz` that were already added as configurations to the project:

```sh
ibmcloud project config-create \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--definition '{"name": "StackDev", "members": [{"name": "custom-apache", "config_id": "caff3a49-0bf4-40c4-b348-47e5da6e2274"}, {"name": "test-slz", "config_id": "fc7fa3d1-33db-4c40-9570-7604348ab3c4"} ]}' --output json
```

For more information about the command parameters, see [**`ibmcloud project config-create`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli#project-cli-config-create-command).

## Creating the stack definition by using the CLI
{: #create-stack-definition-cli}

The stack definition contains inputs and outputs at the stack level that can be referenced in the member deployable architectures within the stack. You can also include references between members of the stack, which links the member deployable architectures together: 

![A diagram of a deployable architecture stack. Three input values are defined at the stack level, a prefix, an ssh_key, and an ssh_private_key. The test-slz architecture within the stack references the prefix and ssh_key as two of its input values. While the custom-apache architecture within the stack references an output from test-slz as one of its inputs, along with the ssh_private_key from the stack level.](images/apache-stack.svg "A deployable architecture stack with references"){: caption="Figure 1. A deployable architecture stack with references" caption-side="bottom"}

Currently, members can't reference outputs from the stack level. 
{: note}

Run the following `ibmcloud project stack-definition-create` command to create the stack definition and provide the inputs: 

```sh
ibmcloud project stack-definition-create --project-id PROJECT-ID --id
```

Where `id` is the configuration ID of the `StackDev` deployable architecture stack that you just added to your project. 

For example, the following command adds the following three inputs at the stack level: 
* `prefix` input with `stackDemo` as the default value. The input is a required string that is not hidden from users. 
* `ssh_key` input with no default value. The input is a required string that is not hidden from users. 
* `ssh_private_key` with no default value. The input is a required string that is not hidden from users. 

The command also includes input names for the two members of the stack. These inputs will be populated with values as references:
* The `test-slz` deployable architecture contains a `prefix` input and an `ssh_key` input. 
* The `custom-apache` deployable architecture contains an `ssh_private_key` input and a `prerequisite_workspace_id` input. 

For more information about writing references, see [referencing values](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#reference-values).

```sh
ibmcloud project stack-definition-create \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id 4d69cee6-0fb2-4621-96c6-16d987f3d9d7 \
--stack-definition '{"inputs": [{"name": "prefix", "type": "string", "hidden": false, "required": true, "default": "stackDemo"}, {"name": "ssh_key", "type": "string", "hidden": false, "required": true}, {"name": "ssh_private_key", "type": "string", "hidden": false, "required": true, "default": "<<-EOF\nINSERT YOUR KEY HERE\nEOF"}], "members": [{"name": "test-slz", "inputs": [{"name": "prefix"}, {"name": "ssh_key"}]}, {"name": "custom-apache", "inputs": [{"name": "ssh_private_key"}, {"name": "prerequisite_workspace_id"}]} ]}' --output json
``` 

For more information about the command parameters, see [**`ibmcloud project stack-definition-create`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli&interface=cli#project-cli-stack-definition-create-command).

## Referencing inputs from the stack level within member deployable architectures by using the CLI
{: #update-members-cli}

Now that the inputs are added at the stack level, update the member deployable architectures in the stack to reference those inputs by running the `ibmcloud project config-update` command for each member of the stack: 

```sh
ibmcloud project config-update --project-id PROJECT-ID --id
```

For example, the following command updates the `test-slz` deployable architecture to reference the inputs that were added at the stack level: 

```sh
ibmcloud project config-update \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id fc7fa3d1-33db-4c40-9570-7604348ab3c4 \
--definition '{"inputs": {"prefix": "ref:../../inputs/prefix", "ssh_key": "ref:../../inputs/ssh_key"}}' --output json
```

Since the `custom-apache` architecture uses the `ssh_private_key` value from the stack definition, update the `custom-apache` deployable architecture to reference that value: 

```sh
ibmcloud project config-update \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id caff3a49-0bf4-40c4-b348-47e5da6e2274 \
--definition '{"inputs": {"ssh_private_key": "ref:../../inputs/ssh_private_key"
```

For more information about the command parameters, see [**`ibmcloud project config-update`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli&interface=cli#project-cli-config-update-command).

## Updating input values at the stack level by using the CLI
{: #update-stack-values-cli}

Now that the member deployable architectures are configured to reference the values you want, update the input values at the stack level by running `ibmcloud project config-update` for the `StackDev` deployable architecture stack. For example, the following command updates the `prefix` input value that is referenced by the `test-slz` deployable architecture within the stack. Values are also provided for the `ssh_key` and `ssh_private_key` inputs: 

```sh
ibmcloud project config-update  \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id 4d69cee6-0fb2-4621-96c6-16d987f3d9d7 \
--definition '{"inputs": {"prefix": "kb-stack-0327", "ssh_key": "<publicKey>", "ssh_private_key": "<privateKey>"}}' --output json
```

For more information about the command parameters, see [**`ibmcloud project config-update`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli&interface=cli#project-cli-config-update-command).

Now that the input value is configured at the stack level, [validate](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#how-to-config) and [deploy](/docs/secure-enterprise?topic=secure-enterprise-deploy-project&interface=ui) each member deployable architecture within the stack. 

For example, the following command validates the `test-slz` deployable architecture: 

```sh
ibmcloud project config-validate \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id fc7fa3d1-33db-4c40-9570-7604348ab3c4
```

While the following command approves the `test-slz` deployable architecture for deployment: 

```sh
ibmcloud project config-approve \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id fc7fa3d1-33db-4c40-9570-7604348ab3c4 \
--comment 'I approve'
```

And the following command deploys the `test-slz` deployable architecture: 

```sh
ibmcloud project config-deploy \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id fc7fa3d1-33db-4c40-9570-7604348ab3c4 
```

## Onboarding a deployable architecture stack to a private catalog by using the CLI 
{: #onboard-da-stack-to-catalog}

After each member deployable architecture in your stack is validated and deployed, you can onboard your entire stack to a private catalog for others to access. Run the following `ibmcloud project stack-definition-export` command: 

```sh
ibmcloud project stack-definition-export --project-id PROJECT ID
```

You can create a new product or add a version to an existing product. For example, the following command creates a new product in your private catalog named `My Apache Stack`: 

```sh
ibmcloud project stack-definition-export --project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 --id 4d69cee6-0fb2-4621-96c6-16d987f3d9d7 --settings '{"catalog_id": "702ff97a-e35a-45a4-a0c0-a04e2e052bc8", "label": "My Apache Stack"}' --output json
```

While the following command creates a new version of an existing product: 

```sh
ibmcloud project stack-definition-export \
--project-id 0e13c360-45c4-4b68-a53f-bb8f6ac04161 \
--id 4d69cee6-0fb2-4621-96c6-16d987f3d9d7 \
--settings '{"catalog_id": "702ff97a-e35a-45a4-a0c0-a04e2e052bc8", "product_id": "1bf57631-27a2-42cc-ac87-733cca67e8a5", "target_version": "1.0.1"}' --output json
```

For more information about the command parameters, see [**`ibmcloud project stack-definition-export`**](/docs/secure-enterprise?topic=secure-enterprise-projects-cli&interface=cli#project-cli-stack-definition-export-command).

Your stack is now a draft in the private catalog that is not yet published, but available to anyone who has Editor access to the private catalog. 

To finish onboarding your deployable architecture stack to your private catalog, [edit the catalog details](/docs/secure-enterprise?topic=secure-enterprise-onboard-da&interface=ui#edit-catalog-entry) and provide information like an architecture diagram and a category.
