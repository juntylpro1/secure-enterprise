---

copyright:

  years: 2022, 2023

lastupdated: "2023-05-16"

keywords: known issues, known limitations

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Known issues and limitations for projects
{: #known-issues}

Known issues and limitations include configuration management and user access to projects.
{: shortdesc}

## Authorization
{: #auth-known-issue}

Authorizing users to work in a project is complex as it requires users to be authorized to work with projects, toolchains, {{site.data.keyword.bplong}}, and other tools in IAM. For more information about access, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

Authorizing projects to deploy to a target account is managed by passing an API key into the deployable architecture. Projects can be directly authorized by using a trusted profile, but trusted profiles are not currently supported by all services. API keys will continue to be supported, but a trusted profile is the preferred method for authorizing deployment to target accounts. For more information, see [Authorizing projects to deploy](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).

## Configuration management
{: #configuration-known-issue}

Configurations can be added, deleted, and renamed. Moving a configuration between projects must be done manually by editing `project.json` documents on both projects. If there are multiple configurations in a project, they can be organized only by naming conventions.

## Cost estimate
{: #cost-estimate-known-issue}

Cost estimation is available for deployable architectures in the {{site.data.keyword.cloud_notm}} catalog. Depending on the deployable architecture, a starting cost is estimated based on the available data. This estimated amount is subject to change as the architecture is customized within a project, and it does not include all resources, usage, licenses, fees, discounts, or taxes. In the future, aggregate costs across projects that can be grouped by various criteria will be available. For more information, see [Estimating architecture costs in a project](/docs/secure-enterprise?topic=secure-enterprise-cost-estimate-project).

## API, SDK, and Terraform
{: #api-sdk-tf-known-issue}

The projects API, SDK, and Terraform functionalities are beta for this release. Beta products are made solely available for evaluation and testing purposes. There are no warranties, SLAs, or support provided and beta products are not intended for production use.

## Resource tagging
{: #project-tagging-known-issue}

Resources that are created by deploying from a project are automatically given service tags. These tags are only visible by using the command-line interface (CLI) or API and are not currently available in usage reports. You can use the [`ibmcloud resource search`](/docs/secure-enterprise?topic=secure-enterprise-projects-cli&interface=cli#ibmcloud-resource-tag-search) command to retrieve the resources created by configurations in a project based on the service tag.
