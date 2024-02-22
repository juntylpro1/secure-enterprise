---

copyright:
   years: 2023, 2024
lastupdated: "2024-02-22"

keywords: deployable architecture, custom, private catalog, catalog manifest

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Onboarding a customized deployable architecture to your private catalog
{: #onboard-custom}

After you customize a [deployable architecture](#x10293733){: term} in the {{site.data.keyword.cloud}} catalog to fit your business needs, you can share it with other users in your enterprise by onboarding it to a private catalog.

## Before you begin
{: #onboard-custom-before}

If you used a customization bundle from an {{site.data.keyword.cloud_notm}} deployable architecture, you can [review and use the automation options](/docs/secure-enterprise?topic=secure-enterprise-customize-from-catalog#included-pipelines) available for using GitHub Actions or an {{site.data.keyword.cloud_notm}} Toolchain to onboard to a private catalog and manage the lifecycle of your product.
{: tip}

1. Customize your deployable architecture, which includes a manifest `ibm_catalog.json` file in a customization bundle. The JSON file is used to automatically import product and version information instead of manually entering it in the console. For more information, see [Customizing an {{site.data.keyword.cloud_notm}} deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-customize-from-catalog).
1. Create a release of your repository. For more information, see [Creating a release](/docs/sell?topic=sell-source-repo-setup#create-release).
1. Make sure that you install the {{site.data.keyword.cloud_notm}} CLI and Catalogs management CLI plug-in. For more information, see [Catalogs management CLI plug-in](/docs/cli?topic=cli-manage-catalogs-plugin).
1. Verify that you're assigned the correct access. You need the following {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) roles:

      * Administrator on all account management services and all IAM services
      * Editor on the Catalog management service
      * Manager service access role for {{site.data.keyword.bplong}}
      * Other roles that are required for specific resources in your customized deployable architecture

## Importing a version by using the console
{: #custom-import-ui}
{: ui}

1. Go to **Manage** > **Catalogs** > **Private catalogs** in the {{site.data.keyword.cloud_notm}} console.
1. Select the private catalog where you want to add your product, and click **Add**. If you do not have any private catalogs, click **Create** to add one.
1. Select **Deployable architecture** as the type of the product that you're adding.
1. Choose **Terraform** as your delivery method.
1. Select the type of repository. If the source for your deployable architecture is located in a private repository, you need to authenticate with a personal access token.
1. Enter the source URL. This source URL ends in `tar.gz` and must point to the release snapshot for the version that you're importing.
1. If you created multiple variations of the customized deployable architecture, select the variation you'd like to import first. Variations are used to provide different options within your single catalog tile. For example, a single deployable architecture might have proof of concept and production workload variations as options for users to choose from when deploying.
1. Enter the software version in the format of major version, minor version, and revision, for example, `1.0.0`. Typically, this version matches the version number of your release snapshot.

   If there are multiple variations for a single deployable architecture, ensure that you're using the same version for all variations. This way all variations appear as options on the tile in the catalog.
   {: important}

1. Select a category. The following two categories are commonly used for deployable architectures: Converged infrastructure and Enterprise applications. If you included a category in your catalog manifest file, it is automatically imported.
1. Click **Add product**.
1. If your deployable architecture has multiple variations, click **Add version** to import your next variation. The delivery method, repository type, source URL, and software version must match the information in your catalog manifest JSON. Each variation must be added as a separate version of your deployable architecture. When you are done adding all of the variations, continue to the next step.

## Importing a version by using the CLI
{: #custom-import-cli}
{: cli}

First, install the {{site.data.keyword.cloud_notm}} CLI. For more information, go to [Get started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

Complete the following steps to import your deployable architecture to a private catalog. When a `ibm_catalog.json` catalog manifest file is present, certain metadata is automatically imported to the private catalog when you import a product.

1. Run the [ibmcloud catalog create](/docs/cli?topic=cli-manage-catalogs-plugin#create-catalog) command to create a private catalog. Private catalogs provide a way for you to manage access to products for users in your account. If you already have a private catalog that is created, you can skip this step.

    ```bash
    ibmcloud catalog create --name CATALOG [--catalog-description "DESCRIPTION"]
    ```
    {: codeblock}

1. Run the [ibmcloud catalog offering create](/docs/cli?topic=cli-manage-catalogs-plugin#create-offering) command to add the deployable architecture to your private catalog.

    ```bash
    ibmcloud catalog offering create [--catalog CATALOG-NAME] [--zipurl URL]
    ```
    {: codeblock}

    If you want to import from a private repository, you can use a personal access token by adding `[--token TOKEN]` to your command.
    {: important}

1. Run the [ibmcloud catalog offering add-category](/docs/cli?topic=cli-manage-catalogs-plugin#add-category-offering) command to add a category to your product. If no category is selected, the **Developer tools** category is added by default for new products.

    If you included a category in a catalog manifest file, you can skip this step.
    {: note}

    ```bash
    ibmcloud catalog offering add-category --catalog CATALOG_NAME [--offering OFFERING] [--category CATEGORY]
    ```
    {: codeblock}

1. Run the [`ibmcloud catalog offering import-version`](/docs/cli?topic=cli-manage-catalogs-plugin#import-offering-version) command for each variation of your deployable architecture:

    ```sh
    ibmcloud catalog offering import-version -c <CATALOGID> -o <OFFERINGID> --zipurl <TGZ> --flavor <FLAVOR_LABEL>
    ```
    {: codeblock}

## Configuring a version
{: #custom-config-version}

Review the version details and configure the input variables.

### Reviewing the version details by using the console
{: #custom-review-version-ui}
{: ui}

1. Select your deployable architecture from the Version list.
1. From the Configure version tab, you can review your version details.
1. Optional: If you have multiple variations for a deployable architecture, click the **Edit** icon for the variation. Ensure that the display name and display order that is used for ordering the drop-down list are what you want from your customer's perspective. For example, it might be helpful to order variations small to large or from least expensive to most expensive. Click **Save** when you're done.
1. When you are ready to continue, click **Next**.

### Reviewing the version details by using the CLI
{: #custom-review-version-cli}
{: cli}

You can review your version's details by using the console. To view the steps, see [Reviewing the version details by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-review-version-ui).

### Configuring the input variables by using the console
{: #custom-cfgdeploy-ui}
{: ui}

After you review the version details, you can set the Terraform runtime version, configure deployment details, and update the output value descriptions.

#### Configuring the Terraform runtime version
{: #custom-config-runtime}

If your product requires a specific Terraform runtime version, you can override the default runtime version.

If you included `TF_VERSION` in your input variables within your source repository, you can skip this step.
{: important}

1. From the Configure the deployment details section, select **Override the default Terraform runtime version**.
1. Enter the Terraform runtime version that you want to use.

#### Configuring the input variables
{: #custom-config-input-variables}

Input variables are parameters that users specify when they install your product. You can review and modify the input variables that were imported from your catalog manifest or add new input variables to your deployable architecture. When you configure your input variables, you can update the requirements, visibility, and format of the input variables.

1. To add new input variables, click **Add input variables**.
1. Select the parameters that you want to include, or select **Parameters** to select all options, and click **Add**.
1. From the input variables table, select a parameter, and click **Edit**.
1. Select the applicable options to require or hide the value. You can choose a value type, default value, and description for each input variable to customize how the value appears to users. Unless they are hidden, input variables display for your users, and can be configured during the deployment process. Make sure that your input variable descriptions are clear and concise for your users.

   Required
   :   Users are required to specify the parameter during installation.

   Hidden
   :   The parameter is included in the configuration but is not shown to users and is not configurable.

   To help you and your users stay more secure, make sure that passwords that are stored as hidden values have limited authority. While these values are never stored, they are available during the installation process in a customer account context. Therefore, to avoid a security impact if the value is leaked, make sure that these passwords have read-only access to specific resources, such as a specific image in an image registry.
   {: important}

1. Click **Save** > **Next**.

#### Updating output values
{: #custom-output-values}

You can update the descriptions of any output values that you included. The output values are shown to users when they deploy your product.

If you didn't include output values, you can't update the descriptions.
{: note}

1. From the Configure the deployment details section, go to the Output values section, and find the value that you want to update.
1. Enter a value description that helps the user understand its purpose.
1. Click **Next**.

### Configuring the input variables by using the CLI
{: #custom-onboard-cfgdeploy-cli}
{: cli}

After you review the version details, you're ready to configure the input variables by updating your offering.

1. Run the [`ibmcloud catalog offering get`](/docs/cli?topic=cli-manage-catalogs-plugin#get-offering) command:

   ```sh
   ibmcloud catalog offering get -c <CATALOGID> -o <OFFERINGID> --output json > offering.json
   ```
   {: codeblock}

1. In the `offering.json` file, add your input variables to the `configuration` array within a version and save the file.
1. Run the [`ibmcloud catalog offering update`](/docs/cli?topic=cli-manage-catalogs-plugin#update-offering) command to update your product:

   ```sh
   ibmcloud catalog offering update -c <CATALOGID> -o <OFFERINGID> --updated-offering offering.json
   ```
   {: codeblock}

### Configuring scripts
{: #custom-pre-post-scripts}

You can have a pre-script or post-script run for your deployable architectures before or after validating, deploying, and undeploying. Scripts are configured to a specific version of your deployable architecture, and must be run and validated through projects. For more information about projects, see [Creating a project](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui).

There are several benefits for using scripts for your deployable architecture. Scripts can be used for custom validation, for example, if you want to ensure that the `tag` parameter is always a valid cost center ID. The pre-validation script could make a call out to a service to check that the cost center ID was valid. You can track deployments and add resources to an inventory system by providing a post-deployment script that can call out to a service to track which resources were just deployed. Another scenario could be data migration. A pre-deployment script can backup data and then after the deployable architecture deletes the old data store and creates the new one, the post-deployement script can restore it to the new data store. Or you can use scripts to install or configure software.

Scripts are pulled from your deployable architecture's repository. Scripts need to be written in Ansible and saved in a YAML file. For the deployment to recognize the scripts automatically, create a scripts file in the root of your repo and they need to be saved in this order `action/stage/type.yaml`. For example, if you have a script that you want to run before your project validation, the file would be saved as `validate/pre/ansible.yaml`. If they are saved in a different directory, you need to use the catalog manifest so that the catalog can find them. For more information about the catalog manifest, see [Specifying product metadata for onboarding a product to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-manifest).

All scripts must be capable of running more than once without failing. For example, a pre-deployment or post-deployment script should operate correctly, even if it is run several times. Post-deployment scripts might add resources to a catalog management database and should be sure not to add duplicate resources if run more than once.

The following is an example of a pre-script that is used to display a message after the deployable architecture is validated. Pre-scripts get passed to all of the inputs from the deployable architecture, including the credentials used to authorize deployment.

```python
- name: Validate pre playbook
  hosts: localhost
  vars:
    ibmcloud_api_key: "{{ lookup(`ansible.builtin.env`, `ibmcloud_api_key`)}}"
    cos_instance_name: "{{ lookup(`ansible.builtin.env`, `cos_instance_name`)}}"
    workspace_id: "{{ lookup(`ansible.builtin.env`, `workspace_id`)}}"
  tasks:
  - name: Print message
    ansible.builtin.debug:
      msg: "The workspace id is {{ workspace_id }}"
    when: workspace_id is defined and workspace_id != ""
  - name: Print message
    ansible.builtin.debug:
      msg: "The cos instance name is {{ cos_instance_name }}"
    when: cos_instance_name is defined
  - name: Print result
    ansible.builtin.debug:
      msg: "Received api key"
    when: ibmcloud_api_key is defined
```

The following is an example of a post-script. Post-scripts get passed the outputs of the deployable architecture.

```python
- name: Deploy post playbook
  hosts: localhost
  vars:
    ibmcloud_api_key: "{{ lookup(`ansible.builtin.env`, `ibmcloud_api_key`)}}"
    git_repo_url: "{{ lookup(`ansible.builtin.env`, `git_repo_url`)}}"
  tasks:
   - name: Print result
     ansible.builtin.debug:
       msg: "Received api key"
     when: ibmcloud_api_key is defined
   - name: Print result
     ansible.builtin.debug:
       msg: "The result is: {{ git_repo_url }}"
     when: git_repo_url is defined and git_repo_url != ""
```

To add scripts to your deployable architecture's version, use the following steps.

1. Create a scripts file in the root of your repo and save your scripts as separate YAML files. The file structure for your script file needs to be `root/action/state/type`.yaml. For example, `script/validate/pre/ansible.yaml`.
1. From the Configure the deployment details section, click **Add scripts**.
1. Select the scripts that you would like to add, and click **Add**.

### Defining IAM access by using the console
{: #custom-solution-access-ui}
{: ui}

Let users know the service and platform access roles that are needed to install your product. The IAM access that you add is required for users to install your product. If you included IAM access information in your catalog manifest file, the information was imported during onboarding. If not, you can add new access. For more information, see [Service access roles](/docs/account?topic=account-userroles#service_access_roles).

#### Adding new IAM access
{: #custom-solution-new-access}

1. From the Define IAM access section, click **Add**.
1. Select the service that is required to use your product.
1. Select the service access role that is required. The service access role allows access for using the service and performing service API calls.
1. Select the platform access role that is required. The platform access role enables actions to be performed on platform resources, such as creating an instance, connecting instances to apps, and assigning user access.
1. Click **Add** > **Next**.

### Defining IAM access by using the CLI
{: #custom-solution-access-cli}
{: cli}

If you included a catalog manifest file in your repository, the IAM access was automatically imported into the private catalog. If not, you can add new access by using the console. To view the steps, see [Defining IAM access by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-solution-access-ui).

## Adding deployable architecture details by using the console
{: #custom-solution-arch-ui}
{: ui}

Each variation of a deployable architecture must have at least one architecture diagram. Architecture diagrams must be provided in `.svg` format and outline the system and relationships, constraints, and boundaries between the components of the deployable architecture.

If your catalog manifest contains architecture diagram information, it was automatically imported during onboarding. If not, complete the following steps to add an architecture diagram:

1. Click **Add architecture diagram**.
2. Click **Add**.
3. Enter the URL to your SVG diagram.
4. Add a short caption that describes what architecture is being depicted.
5. Add a longer description that explains in more detail what this architecture helps to achieve and what types of relationships between components are represented.
6. Optional: Click **Add** if you want to provide more diagrams.
7. Click **Update**.
8. Review what you added, and click **Next**.

### Adding highlights
{: #custom-solution-highlight-ui}

You can add details that highlight the processes, abilities, and results of the version, or if applicable, the architecture variation. If you have multiple architecture variations, each variation should use the same highlight and then a unique description of how it does or doesn't meet each. Customers can use the highlights to evaluate the differences between variations. For example, you might want to list number of VPCs, network connectivity type, high availability capability, or other important factors that might be used to differentiate each variation.

If you included feature and highlight information in your catalog manifest file, it was automatically imported during onboarding. If not, complete the following steps to add highlights:

1. Click **Add highlights**.
1. Click **Add**.
1. Enter the name of the highlight that you want to feature. For example, `Number of VPCs`.
1. Enter a description. For example, if you chose `Number of VPCs` as the name of the highlight and, you can enter `2` as the description.
1. Click **Update** > **Next**.

### Adding prerequisites
{: #custom-solution-dependencies}

You can choose to list your deployable architecture as a full stack product or as an extension with prerequisites. If your product is an extenstion, you must list prerequisite products that users are required to deploy before this deployable architecture. These prerequisite products are listed on the deployable architecture's catalog page.

If you included a dependency section in your catalog manifest file, prerequisite information was automatically imported during onboarding. If not, complete the following steps:

1. From the Add prerequisites section, choose whether your product is a full stack or an extension. If your architecture is a full stack product, no further action is required.
1. If your product is an extension, click **Add**.
1. Enter or select the product that you want to add as a prerequisite.
1. Enter the required version or range of versions by using SemVer formatting. For example, `^1.0.0`.
1. Select any required variations. If no specific variations are selected, all variations are listed as prerequisites.
1. Click **Add** > **Next**.

## Adding deployable architecture details by using the CLI
{: #custom-arch-cli}
{: cli}

If you included a catalog manifest file in your repository, deployable architecture details are automatically imported into the private catalog. If not, you can add an architecture diagram to your deployable architecture by using the console. To view the steps, see [Adding deployable architecture details by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-solution-arch-ui).

## Adding the license requirements by using the console
{: #custom-cfg-license-ui}
{: ui}

If users are required to accept any license agreements beyond the {{site.data.keyword.cloud_notm}} Services Agreement, provide the URL to each agreement.

If you included a catalog manifest file in your repository, license requirement details were automatically imported into the private catalog. If not, complete the following steps:

1. From the Add license agreements section, click **Add license**.
1. Enter the name and URL of the license, and click **Add license**.
1. After entering all additional license agreements, click **Next**.

## Adding the license requirements by using the CLI
{: #custom-cfg-license-cli}
{: cli}

If you included a catalog manifest file in your repository, license requirement details were automatically imported into the private catalog. If not, add license requirements to your deployable architecture by using the console. To view the steps, see [Adding license requirements by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-cfg-license-ui).

## Reviewing your readme file by using the console
{: #custom-readme-ui}
{: ui}

When users access your deployable architecture from the catalog, they can view the readme file on your product's catalog details page.

1. From the Edit readme file section, review your readme file.
2. If changes are required, update your readme file from your source repository.

If you reload the version at any time, any changes that you made to your readme file in the console will be overwritten with the content from your source repository.
{: note}

## Reviewing your readme file by using the CLI
{: #custom-readme-cli}
{: cli}

Review your readme file by using the console. To view the steps, see [Reviewing your readme file by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-readme-ui).

## Validating a test deployment by using the console
{: #custom-validate-ui}
{: ui}

The validation process tests your Terraform template by running it from the {{site.data.keyword.bpshort}} service that you configure. A successful validation ensures that users can ceate your deployable architecture with your default input variables. You must validate your deployable architecture before you can share it.

If you are validating a module, make sure that all required resources are available. If you are validating a deployable architecture that references modules from the catalog, make sure that the modules were onboarded to the catalog.

1. From the Validate version page, enter the name of your {{site.data.keyword.bpshort}} service, select a resource group, select a {{site.data.keyword.bpshort}} region, and click **Next**.

   In the **Tags** field, you can enter a name of a specific tag to attach to your template. This tag is put on the {{site.data.keyword.bplong_notm}} workspace. Tags provide a way to organize, track usage costs, and manage access to the resources in your account.
   {: tip}

1. From the input variables section, review your parameter values, and click **Next**.
1. In the Validation version section, select **I have read and agree to the following license agreements**.
1. Click **Validate**.

   To monitor the progress of the validation process, click **View logs**.
   {: tip}

## Validating a test deployment by using the CLI
{: #custom-validate-cli}
{: cli}

To validate a version of your deployable architecture into an existing product, run the [`ibmcloud catalog offering version validate`](/docs/cli?topic=cli-manage-catalogs-plugin#validate-offering) command:

```sh
ibmcloud catalog offering version validate --vl <VERSION_LOCATOR>
```
{: codeblock}

## Reviewing cost by using the CLI
{: #custom-cost-cli}
{: cli}

Review the cost of your deployable architecture by using the console. To view the steps, see [Reviewing or defining cost by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-cost-ui).

## Reviewing or defining cost by using the console
{: #custom-cost-ui}
{: ui}

You can review the estimated starting cost of your product. If you included the resource metadata in your source repository, the information is parsed during validation and pulled into a starting cost per hour (USD) summary table. The table is displayed in the catalog for customers to compare across variations of a deployable architecture or to get a general idea of what a base configuration of your deployable architecture might cost.

The summary table lists the resources that your product uses and their estimated costs. Starting cost is an estimate based on available data. It does not include all resources, usage, license, fees, discounts, or taxes.
{: note}

## Managing compliance
{: #custom-tf-controls}

You can add controls to your deployable architecture to prove that it meets security and compliance requirements.

Before you can add controls to your product, you must choose a predefined profile or add your controls to a custom {{site.data.keyword.compliance_full}} profile. Then, scan the resources in your account that match those the deployable architecture creates to verify.
{: important}

Only controls that are supported by the {{site.data.keyword.compliance_short}} and validated by {{site.data.keyword.compliance_short}} scans appear in the catalog.

### Adding compliance controls by using the console
{: #custom-tf-add-controls-ui}
{: ui}

You must include compliance information in your catalog manifest JSON file to add profiles and controls to your product. For more information, see [Specifying product metadata for onboarding a product to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-manifest).

### Adding compliance controls by using the CLI
{: #custom-tf-add-controls-cli}
{: cli}

You must include compliance information in your catalog manifest JSON file to add profiles and controls to your product. To see the steps, see [Adding compliance controls by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-tf-add-controls-ui).

### Applying {{site.data.keyword.compliance_short}} scans by using the console
{: #custom-tf-scc-scan-ui}
{: ui}

Add the scans that you previously ran in the {{site.data.keyword.compliance_short}}. {{site.data.keyword.compliance_short}} scans determine adherence to regulatory controls. For more information, see [Scheduling a scan](/docs/security-compliance?topic=security-compliance-scan-resources&interface=ui).

1. Select the profile that you used for the evaluation.
1. Select the {{site.data.keyword.compliance_short}} scan.
1. Click **Apply scan**.
1. Click **Next**.

If your version does not pass all of the goals for a particular control, you can create a custom Security and Compliance profile.

### Applying {{site.data.keyword.compliance_short}} scans by using the CLI
{: #custom-tf-scc-scan-cli}
{: cli}

Add the scans that you previously ran in the {{site.data.keyword.compliance_short}}. {{site.data.keyword.compliance_short}} determine adherence to regulatory controls. For more information, see [Scheduling a scan](/docs/security-compliance?topic=security-compliance-scan-resources&interface=ui).

To add the {{site.data.keyword.compliance_short}} scan, run the [`ibmcloud catalog offering version scc`](/docs/cli?topic=cli-manage-catalogs-plugin#version-scc) command:

```sh
ibmcloud catalog offering version scc --vl <VERSION_LOCATOR> --profile <PROFILE_ID> --scan <SCAN_ID>
```
{: codeblock}

## Reviewing requirements by using the console
{: #custom-tf-review-reqs-ui}
{: ui}

Make sure that you completed all of the required steps so that you can share the deployable architecture with others in your enterprise.

## Reviewing requirements by using the CLI
{: #custom-tf-review-reqs-cli}
{: cli}

You can make sure that you completed all of the required steps. To view the steps, see [Reviewing requirements by using the console](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=ui#custom-tf-review-reqs-ui).
