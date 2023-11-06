---

copyright:
  years:  2023
lastupdated: "2023-11-06"

keywords: change log for Projects, updates to Projects CLI, projects CLI

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Project CLI change log
{: #cli-change-log}

<!-- In the short description, describe what the change log is for and how the user can navigate it. -->
In this change log, you can learn about the latest changes, improvements, and updates for the Project CLI.

## Version 0.0.25
{: #cli-0024}

Version 0.0.25 of the CLI was released on 6 November 2023. 

In this release, the `create` and `update` JSON properties match the `get` JSON properties with separation between the server-controlled attributes and the user-supplied attributes. The commands are normalized so that they follow a regular pattern. Terminology was also aligned to use `validate`, `deploy`, and `undeploy`. 

Updated the following commands: 
- All commands that impact configurations now begin with `config` instead of `project`.
- The **`project create`**, **`project update`**, **`config-create`**, and **`config-update`** commands now use the `definition` construct to replace individual parameters like `name` and `description`.
- The **`project config-install`** command is replaced by the **`config-deploy`** command.
- The **`project config-uninstall`** command is replaced by the **`config-undeploy`** command.
- The **`project list-config-drafts`** command is replaced by the **`config-versions`** command.
- The **`project config-draft-get`** command is replaced by the **`config-version-get`** command.

Added the following commands: 
- The **`config-version-delete`** command deletes a version of a configuration. 
- The **`environment-create`** command creates an environment. 
- The **`environment-update`** command edits an environment. 
- The **`environment-delete`** command deletes an environment. 
- The **`environment`** command returns an environment. 
- The **`environments`** command returns all environments. 

<!-- Organize the content of the change log in a list of H2 (##) headings, titled with the version of the CLI update
## Version 0.3.2
{: #cli-032}

Version 0.3.2 of the CLI was released on 31 August 2021.

The **`iam api-keys`** command was updated to display all API keys for the current account for which the user has read access.

## Version 0.3.1
{: #cli-031}

Version 0.3.1 of the CLI was released on 4 July 2021.

- Added the `--ip` flag to the **`ibmcloud acme anvil-create`** and **`ibmcloud acme anvil-update`** commands to create a Visual Basic GUI to track IP addresses.
- Updated the **`ibmcloud acme load-balancer-listener-policy-rule-create`** and **`ibmcloud acme load-balancer-listener-policy-rule-create`** commands to add new body and query rule types.
- Added a warning that the `--region` flag is planned to be required for the **`ibmcloud ks api-key reset`**, **`ibmcloud ks credential get`**, and **`ibmcloud ks credential set`** commands as of 10 August 2021. The region is already required by the API. Currently in the CLI, the region defaults to the targeted region if the `--region` flag is not used.

## _CLI version_ - DD Month YYYY
{: #cli-version-id}

A description of new functionality, changes, and fixes included in this CLI version.-->
