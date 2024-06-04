---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-09"

keywords: onboard, catalog management, private catalog, catalog manifest, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Providing product information
{: #catalog-details}

After you've onboarded your deployable architecture, you can specify product information by making selection in the console, or by manually building a file. The product-level information that you provide is shown in the catalog when your users attempt to work with your product. The information can help them to understand the function of the individual components that are associated with it.

When you onboard a deployable architecture to a catalog, you must provide preset configurations that will dictate the basic configuration that a user will get when they provision your architecture from the catalog.

Prefer to edit these configurations locally? [Build a catalog manifest from a template instead](/docs/secure-enterprise?topic=secure-enterprise-catalog-manifest-values).
{: tip}


## Before you begin
{: #before-catalog-details}

Before you can start working with the manifest file, you must have the following prerequisites.

* The required access to work with private catalogs and deployable architectures:
   * Administrator on all account management services and all IAM services
   * Editor on the Catalog management service
   * Manager service access role for {{site.data.keyword.bplong}}
   * Other roles that are required for specific resources in your customized deployable architecture
* Make sure that you install the {{site.data.keyword.cloud_notm}} CLI and Catalogs management CLI plug-in. For more information, see [Catalogs management CLI plug-in](/docs/cli?topic=cli-manage-catalogs-plugin).
* A deployable architecture that you have previously [onboarded to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-share-arch-catalog).

   Don't have a deployable architecture ready to use? [Use the sample deployable architecture to test the flow](https://github.com/IBM/catalog-create-sample-da){: external}.
   {: tip}


## Configuring your version
{: #custom-cfgdeploy-ui}
{: ui}

After you review the version details, you can set the Terraform runtime version, configure deployment details, and update the input and output values.

### Step 1: Review available version information
{: #review-info}

1. Go to the **Manage > Catalogs > Private catalogs** page of the console.
1. Select the private catalog that you want to add a product to. The catalog details page opens.
1. Select your the product that you want to provide additional details for.
1. On the **Versions** tab, select the version that you want to provide details for.
1. On the **Configure versions tab** review the version details. Then, click **Next**.

### Step 2: Configure deployment details through the UI
{: #configure-deployment-details}

1. Configure the Terraform runtime version.

   You can choose to override the default version by clicking the **Override the default Terraform runtime version** box and then inputting a valid runtime version.

1. Configure your input variables. These are the variables that a user will need to specify when working with your deployable architecture. Click **Add input variables** and provide the requested information.
1. Configure your output variables. Terraform output values show information about your configuration and can be used to help users when they're working with multiple Terraform configurations.
1. Add scripts to your version.

   1. Create a scripts file in the root of your repository and save your scripts as separate YAML files. The file structure for your script file must be `root/action/state/type.yaml`. For example, `script/validate/pre/ansible.yaml`.
   1. Click **Add scripts**.
   1. Select the scripts that you would like to add, and click **Add**.
   1. When you've finished adding scripts, click **Next**.

#### Understanding pre and post scripts
{: #understand-scripts}

You can have a pre-script or post-script run for your deployable architectures before or after validating, deploying, and undeploying. Scripts are configured to a specific version of your deployable architecture, and must be run and validated through projects. For more information about projects, see [Creating a project](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui).

There are several benefits for using scripts for your deployable architecture. Scripts can be used for custom validation, for example, if you want to ensure that the `tag` parameter is always a valid cost center ID. The pre-validation script could make a call out to a service to check that the cost center ID was valid. You can track deployments and add resources to an inventory system by providing a post-deployment script that can call out to a service to track which resources were just deployed. Another scenario could be data migration. A pre-deployment script can backup data and then after the deployable architecture deletes the old data store and creates the new one, the post-deployement script can restore it to the new data store. Or you can use scripts to install or configure software.

Scripts are pulled from your deployable architecture's repository. Scripts need to be written in Ansible and saved in a YAML file. For the deployment to recognize the scripts automatically, create a scripts file in the root of your repo and they need to be saved in this order `action/stage/type.yaml`. For example, if you have a script that you want to run before your project validation, the file would be saved as `validate/pre/ansible.yaml`. If they are saved in a different directory, you need to use the catalog manifest so that the catalog can find them. For more information about the catalog manifest, see [Specifying product metadata for onboarding a product to a private catalog](/docs/secure-enterprise?topic=secure-enterprise-manifest-values).

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
{: codeblock}

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
{: codeblock}

### Step 3: Define IAM access
{: #define-iam-access}
{: ui}

Let users know the service and platform access roles that are needed to install your product. The IAM access that you add is required for users to install your product. If you included IAM access information in your catalog manifest file, the information was imported during onboarding. If not, you can add new access. For more information, see [Service access roles](/docs/account?topic=account-userroles#service_access_roles).

To add new roles, you can use the following steps.

1. From the **Define IAM access** section, click **Add**.
1. Select the service that is required to use your product.
1. Select the service access role that is required. The service access role allows access for using the service and performing service API calls.
1. Select the platform access role that is required. The platform access role enables actions to be performed on platform resources, such as creating an instance, connecting instances to apps, and assigning user access.
1. Click **Add** > **Next**. You are taken into the next section on adding deployable architecture details.

## Adding deployable architecture details
{: #add-da-details}

Each variation of a deployable architecture must have at least one architecture diagram. Architecture diagrams must be provided in `.svg` format and outline the system and relationships, constraints, and boundaries between the components of the deployable architecture.


### Step 1: Adding architecture diagrams
{: #add-arch-diagram}

Each variation of a deployable architecture must have at least one architecture diagram. Architecture diagrams must be provided in `.svg` format and outline the system and relationships, constraints, and boundaries between the components of the deployable architecture.

1. Click **Add architecture diagram**.
2. Click **Add**.
3. Enter the URL to your SVG diagram.
4. Add a short caption that describes what architecture is being depicted.
5. Add a longer description that explains in more detail what this architecture helps to achieve and what types of relationships between components are represented.
6. Optional: Click **Add** if you want to provide more diagrams.
7. Click **Update**.
8. Review what you added, and click **Next**.


### Step 2: Add prerequisites
{: #add-prerequisites}

You can choose to list your deployable architecture as a full-stack product or as an extension with dependencies. If your product is an extension, you must list prerequisite products that users are required to deploy before this deployable architecture. Prerequisite products are listed on the deployable architecture's catalog page.

1. From the **Add prerequisites** section, choose whether your product is a full stack or an extension. If your architecture is a full-stack product, no further action is required.
1. If your product is an extension, click **Add**.
1. Enter or select the product that you want to add as a prerequisite.
1. Enter the required version or range of versions by using SemVer formatting. For example, `^1.0.0`.
1. Select any required variations. If no specific variations are selected, all variations are listed as prerequisites.
1. Click **Add** > **Next**.


### Step 3: Add highlights
{: #add-highlights}

You can add details that highlight the processes, abilities, and results of the version, or if applicable, the architecture variation. Highlights appear on the catalog page and change based on the version that is selected or provide a comparison view for users who are comparing architecture variation options for a single product. If you have multiple architecture variations, each variation should use the same highlight and then a unique description of how it does or doesn't meet each. Highlights help customers to evaluate the differences between variations. For example, you might want to list the number of VPCs, network connectivity type, high availability capability, or other important factors that might be used to differentiate each variation.

1. Click **Add highlights**.
1. Click **Add**.
1. Enter the name of the highlight that you want to feature. For example, `Number of VPCs`.
1. Enter a description. For example, if you chose `Number of VPCs` as the name of the highlight and, you can enter `2` as the description.
1. Click **Update** > **Next**.


## Adding license agreements
{: #add-license-agreements}

If users are required to accept any license agreements beyond the {{site.data.keyword.cloud_notm}} Services Agreement, provide the URL to each agreement.

1. From the Add license agreements section, click **Add license**.
1. Enter the name and URL of the license, and click **Add license**.
1. After entering all additional license agreements, click **Next**.


## Editing your readme file
{: #edit-readme}

When a user attempts to work with your deployable architecture from the catalog, they can view the readme file on your product's catalog details page.

1. From the **Edit readme** section, review your current file.
1. Click **Edit** to make any needed changes. When you are finished editing, click **Save**.
1. Click **Next**.

If you reload the version at any time, any changes that you made to your readme file in the console will be overwritten with the content from your source repository.
{: important}


## Validating your version
{: #validate-version}

The validation process tests your Terraform template by running it from the {{site.data.keyword.bpshort}} service that you configure. A successful validation ensures that users can create your deployable architecture with your default input variables. You must validate your deployable architecture before you can share it.

Depending on the resources created during validation, you might incur some costs. After completing the onboarding process, you can delete any resources that are not needed. For more information, see [Deleting resources](/docs/account?topic=account-delete-resource&interface=ui).
{: important}

If you are validating a module, make sure that all the required resources are available. If you are validating a deployable architecture that references modules from the catalog, make sure that the modules were onboarded to the catalog.

1. From the **Validate version** page, enter the name of your {{site.data.keyword.bpshort}} service, select a resource group, select a {{site.data.keyword.bpshort}} region, and click **Next**.

   In the **Tags** field, you can enter a name of a specific tag to attach to your template. This tag is put on the {{site.data.keyword.bplong_notm}} workspace. Tags provide a way to organize, track usage costs, and manage access to the resources in your account.
   {: tip}

1. From the input variables section, review your parameter values, and click **Next**.
1. In the Validation version section, select **I have read and agree to the following license agreements**.
1. Click **Validate**.

   To monitor the progress of the validation process, click **View logs**.
   {: tip}


## Reviewing or defining cost
{: #review-cost}

You can review the estimated starting cost of your product. If you included the resource metadata in your source repository, the information is parsed during validation and pulled into a starting cost per hour (USD) summary table. The table is displayed in the catalog for customers to compare across variations of a deployable architecture or to get a general idea of what a base configuration of your deployable architecture might cost.

The summary table lists the resources that your product uses and their estimated costs. Starting cost is an estimate based on available data. It does not include all resources, usage, license, fees, discounts, or taxes.
{: note}

## Managing compliance
{: #manage-compliance}


You can add profiles and controls to your deployable architecture to prove that it meets security and compliance requirements. You must use {{site.data.keyword.compliance_short}} to scan the resources created during validation.

Only profiles and controls that are supported by the {{site.data.keyword.compliance_short}} and validated by {{site.data.keyword.compliance_short}} scans appear in the catalog.


### Step 1: Add claims
{: #add-claims}

Add the profiles that contain the controls that your deployable architecture can meet.

1. In the **Manage compliance** section of your product, select **Add claims**.
1. Select the profile that you want to add.
1. Choose to add the entire profile or a subset of controls.
1. If you choose an entire profile, continue to the next step. If you choose to add a subset of controls, select the controls that you want to add.
1. Click **Add**.

### Step 2: Run a scan through Security and Compliance Center
{: #run-scan}

When you claim profiles and controls, you must evaluate the resources that were created during validation to ensure compliance. To run a scan, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) **> Security and Compliance** to access {{site.data.keyword.compliance_short}}.
2. In the navigation, click **Profile**.
3. Click the **Overflow** menu in the row of the profile that you want to evaluate and select **Run scan**.
3. Click **Run scan**.

After your scan completes, you can return to your private catalog to continue the onboarding process.

### Step 3: Add your scan results
{: #add-scan-results}

Add the scans that you previously ran in the {{site.data.keyword.compliance_short}}. {{site.data.keyword.compliance_short}} scans determine adherence to regulatory controls. For more information, see [Running an evaluation for {{site.data.keyword.cloud}}](/docs/security-compliance?topic=security-compliance-scan-resources).

1. Click **Add scan**.
1. Select the profile that you used for the evaluation.
1. Select the {{site.data.keyword.compliance_short}} scan.
1. Click **Apply scan**.
1. Click **Next**.


## Reviewing requirements
{: #review-reqs}

Review the selections that you made through and confirm that you are ready to share. If all of the changes that you've made look accepatable to you and have gone through any required reviews at your organization. Click **Ready to share**.


## Downloading the manifest
{: #downloading-manifest}

When you're ready to share your deployable architecture with others in your organization, you must specify product information so that it is catagorized correctly in the catalog. To do so, you use a file called `ibm_catalog.json`, also known as a manifest, to detail the information about your architecture that you want to ensure is prefilled when members of your organization attempt to work with your architecture. You can choose to manually build the manifest file, or you can take advantage of the functionality in the console that will generate it on your behalf.

To download a manifest through the UI, you can use the following steps.
{: ui}

1. Go to the **Manage > Catalogs > Private catalogs** page of the console.
2. Select the architecture that was previously onboarded. A details page opens.
3. On the **Versions** tab, select the version that you want to generate a manifest for.
4. From the **Actions** drop-down menu, select **Download manifest**.
5. Add the file into the root folder of your source code repository as `ibm_catalog.json`.
{: ui}

To download the manifest through the CLI, you can use the following command for the `catalogs-management` CLI plugin.
{: cli}

```
ibmcloud catalog offering download-manifest --catalog "<your catalog name>" --offering "catalog-ibm-catalog-doc-0.0.1" --version 0.0.1 --path
```
{: codeblock}
{: cli}

Whenever you make changes to your products configuration, generate and download a new manifest. Be sure to add it to your source code repository as described in the previous section.
{: note}
