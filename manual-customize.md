---

copyright:

  years: 2023, 2024

lastupdated: "2024-04-23"

keywords: customize, deployable architecture, bundle, manifest

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Customizing an {{site.data.keyword.cloud_notm}} deployable architecture
{: #customize-from-catalog}

You can take advantage of a {{site.data.keyword.IBM}}-curated customization bundle to extend and customize an {{site.data.keyword.cloud}} [deployable architecture](#x10293733){: term}. Each deployable architecture provides its own customization bundle. With the bundle, you can edit the deployable architecture on your local computer, use your own pipelines to test, and extend your own products to fit your enterprise's needs. To customize an architecture, you must have familiarity with Terraform.
{: shortdesc}

The customization bundle also includes an `automation` directory that includes starter scripts to help you manage the lifecycle of your customized deployable architecture from onboarding and validation to publishing it to a private catalog on {{site.data.keyword.cloud_notm}}. Currently, two pipeline methods are included in this directory: GitHub actions or a Toolchain from {{site.data.keyword.cloud_notm}}.

The following guidance provides an overview of the customization bundle and some examples of customization that you can do. It is not all inclusive and you can make any changes that you need. After you modify the architecture, you can add it to a private catalog and use {{site.data.keyword.IBM_notm}}'s tools to check for vulnerabilities, ensure security and compliance, and share the architecture with your enterprise. For a more in-depth customization walkthrough, see [Using a customization bundle to customize a deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-basic-custom).


Depending on your level of customization, {{site.data.keyword.cloud_notm}} might not support the deployable architecture. The components of the architecture that are supplied in the customization bundle are supported by {{site.data.keyword.cloud_notm}}, but any customized code that's used to extend is not.
{: important}

## Before you begin
{: #customize-begin}

1. Create a repository to store the customized deployable architecture, for example, a GitHub repository. For more information, see [Creating a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository){: external}.
1. Make sure that you have an editor of your choice to modify the deployable architecture, for example, Visual Studio Code. For more information, see [Visual Studio Code](https://code.visualstudio.com/){: external}.
1. Make sure that you have tools of your choice to test your deployable architecture and ensure that it works. For example, you can use Terraform runtime, which supplies the Terraform command line.

## Finding a customizable deployable architecture
{: #customize-find}

{{site.data.keyword.cloud_notm}} provides multiple deployable architectures that you can use as-is or you can customize. To find an architecture, complete the following steps:

1. In the [{{site.data.keyword.cloud_notm}} catalog](/catalog#reference_architecture){: external}, select a deployable architecture.
1. Download the customization bundle by selecting **Review deployment options** > **Customize locally** > **Start customizing**.

## Customizing the deployable architecture
{: #customize-bundle}

When you download the customization bundle, you receive a set of files that are designed to help you get started with customization.

### `ibm_catalog.json`
{: #customize-JSON}

The `ibm_catalog.json` file is a manifest JSON file that is used to automatically import version information into a private catalog. With a catalog manifest file, you can avoid manually entering version metadata through the console. To view how to set up an `ibm_catalog.json` file and the values that you can include, see [Specifying product metadata for onboarding a product to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-manifest-values).

### `main.tf`
{: #customize-main}

The `main.tf` file is where configuration information about each deployable architecture that you want to use is stored. Depending on the deployable architecture, you can use this file to specify specific regions, API keys, and source code locations. You can also use this file to add other modules and update the architecture's Terraform parameters.

#### Example of `main.tf` with specifications
{: #customize-main-example}

The following example shows Secure infrastructure on VPC for regulated industries using a specific region, `us-south`:

```bash
module "landing-zone" {
  source           = "https://cm.globalcatalog.cloud.ibm.com/api/v1-beta/offering/source//examples/power-sap?archive=tgz&catalogID=7df1e4ca-d54c-4fd0-82ce-3d13247308cd&flavor=power&kind=terraform&name=slz-vpc-with-vsis&version=0.0.22"
  ibmcloud_api_key = var.ibmcloud_api_key
  ssh_public_key   = var.ssh_public_key
  region           = "us-south"
  prefix           = "slz"
}
```
{: codeblock}

### `outputs.tf`
{: #customize-outputs}

The `outputs.tf` file contains available output values that you can include in your deployable architecture. The values are commented out, but you can include the values by removing the `#` symbol from the value. Also, you can add more output variables to the file. To include certain values, complete the following steps.

1. Open the `outputs.tf` file.
2. Remove the `#`s from any output value that you want to include.

#### Example of `outputs.tf`
{: #customie-outputs-example}

The following example includes the `vsi_names` value and excludes the `transit_gateway_name` value:


```bash
output "vsi_names" {
  value       = var.vsi_names
  description = "A list of the vsis names provisioned within the VPCs"
}
```
{: codeblock}

```text
#output "transit_gateway_name" {
#  value       = var.transit_gateway_name
#  description = "The name of the transit gateway"
#}
```
{: codeblock}

### `provider.tf`
{: #customize-provider}

The `provider.tf` file contains required information about which provider, API key, and region that users are required to use.

This information is pulled in from the `variables.tf` file. If you need to make changes, update the [`variables.tf`](#customize-variables) file.
{: important}

#### Example of a `provider.tf` file
{: #customize-provider-example}

The following example lists {{site.data.keyword.IBM_notm}} as the provider:

```bash
provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
  region           = var.region
}
```
{: codeblock}

### `README.md`
{: #customize-README}

The readme file contains background and usage information about the deployable architecture. You can customize the readme file to help members of your enterprise use the deployable architecture.

### `variables.tf`
{: #customize-variables}

The `variables.tf` file includes the required variables for the deployable architecture. You can add any additional variables that you need.

### `version.tf`
{: #customize-version}

The `version.tf` file stores information about the Terraform version and provider version that is needed to run the deployable architecture. If you are running the deployable architecture as-is, no updates are necessary. Your configuration might require you to update this file. If you need to specify a particular Terraform or provider version, complete the following steps:

1. Open the `versions.tf` file.
1. Update `required_version` to the Terrafrom version that users need to use.
1. Update `version` to the provider version that users need to use.

## Testing your customized deployable architecture
{: #customize-test}

Before you onboard your customized deployable architecture to a private catalog, test your customization and ensure that the architecture runs as intended. To test your architecture with the Terraform command line, complete the following steps:

1. After you customize the architecture, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Creating a release
{: #customize-release}

If your tests were successful, you can prepare to onboard your architecture to a private catalog by making sure that your files are in the repository and creating a release. For more information, see [Creating a release](/docs/sell?topic=sell-source-repo-setup#create-release).

## Leveraging automation to share to a private catalog
{: #included-pipelines}

The customization bundle has an `automation` directory that includes a couple of options for starter pipelines. These pipelines can be used to automate the lifecycle of your customized products that you share by using a private catalog on {{site.data.keyword.cloud_notm}}. This includes managing the onboarding, validation, and sharing of the deployable architecture version to a private catalog. `README` files are included for each pipeline option that provide details on how to leverage it. For more information about each one, see [GitHub Actions](https://github.com/features/actions){: external} and [Creating a toolchain](https://cloud.ibm.com/devops/setup/deploy?repository=https%3A%2F%2Fus-east.git.cloud.ibm.com%2Fopen-toolchain%2Fiac-compliance-ci-toolchain&env_id=ibm:yp:us-east){: external}.


### Using the console to onboard to a private catalog
{: #customize-onboard-private-catalog}

If you'd like to use the console to onboard your deployable architecture, see [onboarding your customized deployable architecture to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-onboard-da) for step-by-step guidance.

## Next steps
{: #customize-next}

The scripts that are provided in the customization bundle help you to automate the onboarding process to a private catalog for sharing your product with other users. However, if you'd like to use the console or CLI to onboard your deployable architecture, see [onboarding your customized deployable architecture to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-onboard-da) for step-by-step guidance. By using private catalogs, members of your enterprise are required to use approved architectures that they can deploy by using [projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).

