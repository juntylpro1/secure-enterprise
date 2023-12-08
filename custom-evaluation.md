---

copyright:

  years: 2023

lastupdated: "2023-12-07"

keywords: deployable architecture, custom, share, enterprise, evaluate

subcollection: secure-enterprise

content-type: tutorial
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Evaluating an {{site.data.keyword.cloud_notm}} deployable architecture
{: #evaluate-deployable architecture}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

In this tutorial, you walk through how to evaluate {{site.data.keyword.cloud}} pre-built deployable architectures. By completing this tutorial, you learn how to find deployable architectures in the {{site.data.keyword.cloud_notm}} catalog, diagrams, features and descriptions, security and compliance information, and multiple ways to deploy.
{: shortdesc}

Imagine you are a product manager for the fictitious company _Example Corp_. Your enterprise needs a deployable architecture to provide secure and customizable compute resources for running your applications and services. Particularly, you want something that creates secure and compliant Virtual Server Instances on a Virtual Private Cloud (VPC) network. You decide to search the {{site.data.keyword.cloud_notm}} to find something that matches your business needs.

This is a fictitious scenario to help you learn and understand how to share a deployable architecture. As you complete the tutorial, adapt each step to match your organization's needs.

## Finding a deployable architecture
{: #find-deployable-architecture}
{: step}

To begin the evaluation, you decide to search for terms to help you narrow down your selection. Since you are interested in Virtual Server Instances, you decide to use that as your search term.

1. In the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com){: external} console, click **Catalog**.
1. Search for **Virtual Server Instance**.
1. Select **Deployable architectures** from the list of **Type** filters to limit the results to deployable architectures.

You review the names, providers, and short descriptions of the search results and decide to further research **VSI on VPC landing Zone**.

## Evaluating overview information
{: #evaluate-overview}
{: step}

You can review more detailed information on the architecture's catalog page.

1. Select **VSI on VPC landing zone** from the list of search results.
1. Use the **Overview** section to gain a more detailed insight into the purpose and use of **VSI on VPC landing zone**.
1. Review the **Features and capabilities** section to learn about product-level features that highlight the processes, abilities, and results of the deployable architecture. These features apply to the deployable architecture as a whole and do not change, regardless of version or architecture variation. **VSI on VPC landing zone**:
    - Creates virtual servers for workloads
    - Configures subnets
    - Associates security groups
    - Provisions SSH keys

1. Review the related links section to explore **VSI on VPC landing zone**'s deployment guide and readme file to become familiar with how to use the deployable architecture.
1. Click **Get help** for direct access to {{site.data.keyword.cloud_notm}} Support Center.

## Viewing more details
{: #evaluate-details}
{: step}

You use catalog entry additional information to create support cases, use the CLI, and plan deployment. To view more details, complete the following steps:

1. Click **View details**.
1. Review the type, provider, category, and update date of the deployable architecture.
1. Make sure that the version and variation are correct.
1. Use the estimated deployment time for planning purposes and to understand how long deployment is expected to take.
1. Take note of the programmatic name, product ID, version locator, and catalog ID. These values can be used in support cases, CLI, and input values.
1. Use the content source URL to download the source code of the deployable architecture and scan for vulnerabilities. For more information, see [Scanning software for vulnerabilities](/docs/account?topic=account-scans).
1. Close the panel.

## Comparing architecture versions and variations
{: #evaluate-results}
{: step}

You can choose from many versions and compare two variations of the **VSI on VPC landing zone** deployable architecture. The cost varies between each version and variation based on the resources that are required.

1. In the **Architecture** section, select the most recent version.
1. In the **Variation** section, select **See more** to compare the variation options in a list view. You can compare prices, capabilities, and results.
1. Select the **Standard** variation and scroll to the **Architecture overview** section. You can review the variation's architecture diagram and read the diagram description to understand how the variation works and what it produces.
1. Select **Permissions** and review the table to understand the required platform and service roles that are required to successfully deploy **VSI on VPC landing zone**. For more information about reviewing assigned access, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources&interface=ui#review-your-access-console).
1. Select **Security & compliance** to see a list of security profiles and controls that **VSI on VPC landing zone** meets. Profiles and controls that appear in the table were scanned and validated when the deployable architecture was onboarded to the catalog. You can review the security and compliance information to make sure that the architecture meets your enterprise's security requirements.
1. Select **Help** to review the product-specific support information, including the available support channels.
1. Review the **Summary** panel to understand the cost breakdown of your chosen variation.
    You can expand each resource to review the specific items that are running up cost.
    {: tip}

1. Repeat the steps for other versions and variations to understand the differences and decide on the option that best meets your use case.

After you review the variations, you decide that the **Standard** variation of **VSI on VPC landing zone** best meets your enterprise's business needs, but you need to modify the deployable architecture. You are now ready to learn how to [customize **VSI on VPC landing zone**](/docs/secure-enterprise?topic=secure-enterprise-customize-from-catalog).
