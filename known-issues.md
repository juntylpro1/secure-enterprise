---

copyright:

  years: 2022, 2024

lastupdated: "2024-02-26"

keywords: known issues, known limitations

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Known issues and limitations
{: #known-issues}

Known issues and limitations include configuration management, user access to projects, and identity and access management (IAM) limits.
{: shortdesc}

## Authorization
{: #auth-known-issue}

To work in a project, users must have access to the {{site.data.keyword.cloud_notm}} Projects service, the resource group for the project, and {{site.data.keyword.bplong}}. For more information about access, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

Authorizing projects to deploy to a target account is managed by passing an API key into the deployable architecture. [Projects can be directly authorized by using a trusted profile](/docs/secure-enterprise?topic=secure-enterprise-tp-project), but trusted profiles are not currently supported by all services. [API keys will continue to be supported](/docs/secure-enterprise?topic=secure-enterprise-authorize-project), but a trusted profile is the preferred method for authorizing deployment to target accounts.

## Configuration management
{: #configuration-known-issue}

Configurations can be added, deleted, and renamed. Moving a configuration between projects must be done manually by editing `project.json` documents on both projects. If there are multiple configurations in a project, they can be organized only by naming conventions.

## Cost estimate
{: #cost-estimate-known-issue}

Cost estimation is available for deployable architectures in the {{site.data.keyword.cloud_notm}} catalog. Depending on the deployable architecture, a starting cost is estimated based on the available data. This estimated amount is subject to change as the architecture is customized within a project, and it does not include all resources, usage, licenses, fees, discounts, or taxes. For more information, see [Estimating architecture costs in a project](/docs/secure-enterprise?topic=secure-enterprise-cost-estimate-project).

## API, SDK, and Terraform
{: #api-sdk-tf-known-issue}

The projects API, SDK, and Terraform functionalities are beta for this release. Beta products are made solely available for evaluation and testing purposes. There are no warranties, SLAs, or support provided and beta products are not intended for production use.


{{../account/known-issues.md#iam_limits}}

{{../account/known-issues.md#cbr-limits}}

{{../account/known-issues.md#policy-version-limit}}
