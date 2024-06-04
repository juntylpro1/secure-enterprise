---

copyright:
   years: 2024
lastupdated: "2024-05-13"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Publishing a module to the IBM Cloud module registry
{: #publish-module-registry}

The [Module registry](https://cloud.ibm.com/catalog?catalog=2) is a collection of modules with one or more runnable examples where users can copy usage code to get started, but they are not deployable from the registry. This registry is offered on {{site.data.keyword.cloud_notm}}, but is separate from the {{site.data.keyword.cloud_notm}} catalog. It is especially useful for enterprises that have air-gapped environments without access to github.com so that they can access the modules directly from {{site.data.keyword.cloud_notm}}.
{: shortdesc}

After you've completed the IBM Cloud onboarding process, you can publish your module to the registry if you meet the following criteria:

* The module is sourced in the [terraform-ibm-modules](https://github.com/terraform-ibm-modules){: external} GitHub organization following the [Contributing to the IBM Cloud Terraform module projects](https://terraform-ibm-modules.github.io/documentation/#/contribute-module){: external} guidelines.
* Your module must have the `Graduated` or `Stable` [status badge](https://terraform-ibm-modules.github.io/documentation/#/badge-status){: external}.
* You have a personal access token from GitHub that can be used to verify your access to the GitHub source in `terraform-ibm-modules`. The token must have the following access:
   * `public_repo`
   * `read:org`
   * `user:email`
* You must be in the `github-collaborators` team in the terraform-ibm-modules GitHub organization.

If you meet all of the requirements, then you're ready to publish:

1. Go to **Manage** > **Catalogs**, select your private catalog, select your module, and then click **Actions**.
1. Click **Publish**.
1. Select **Publish to module registry**.
1. Enter your personal access token to verify your access to the module source.
1. Click **Publish**.

Now your module is available to all users in the [Module registry](https://cloud.ibm.com/catalog?catalog=2).
