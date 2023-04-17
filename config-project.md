---

copyright:

  years: 2022, 2023

lastupdated: "2023-04-17"

keywords: manage project, rename project, move project, deploy project, merge request, merge changes

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Configuring and deploying a deployable architecture
{: #config-project}

After you add a deployable architecture to your project, you can edit the input values to create a configuration that is used to deploy the architecture.
{: shortdesc}

Configurations can be generic, but many projects use a configuration, or a group of configurations, to deploy resources to different environments. For example, a group of configurations can be used to deploy resources to development, test, and production environments and set up common services outside of the environments. When you deploy your configuration, {{site.data.keyword.bplong}} uses Terraform to apply the underlying plan. 

Before you can deploy your project, the inputs, plan, compliance, and estimated cost for the deployable architecture must be validated. Any changes that are made to the configuration are validated to ensure that there aren't any issues or failures.
{: note}

## Setting input values
{: #project-input-values}

Input values are used to configure a deployable architecture to match your specific needs. The required inputs vary based on the deployable architecture that you choose. They are a set of common inputs that are used to provide shared input values across any number of configurations.

The input's attribute allows variables to be imported from any number of outputs of different configurations, even from other projects. By doing so, the dev environment of an app project can easily be linked to the dev environment of an infrastructure project. Or common input values can easily be shared across environments and projects.

## Configuring the architecture
{: #how-to-config}

To create a customized configuration, complete the following steps:

1. From the **Select inputs** panel, enter values for the required fields for the deployable architecture configuration.

    You must select an authentication method for the project to deploy your configuration. You can use a trusted profile, add an API key by using {{site.data.keyword.secrets-manager_full}}, or add your API key to the `ibmcloud_api_key` field in your configuration. This authorizes the project to deploy to an account and is required to deploy your configuration. For more information, see [Authorizing a project to deploy to an account](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    {: note}

1. Optional: You can add values by going to the **Optional** panel.
1. Click **Save**.
1. Click **Validate**. The modal that is displayed provides more details about your in-progress validation.

   When you validate your configuration, {{site.data.keyword.cloud_notm}} projects run a Code Risk Analyzer scan that includes a [specific set of {{site.data.keyword.compliance_short}} goals](/docs/code-risk-analyzer-cli-plugin?topic=code-risk-analyzer-cli-plugin-cra-cli-plugin#terraform-scc-goals). Controls that the owner of the deployable architecture added that are also supported by {{site.data.keyword.cloud_notm}} projects are checked. Any extra controls that are not included in the list of supported {{site.data.keyword.compliance_short}} goals are not checked when you validate your configuration. If the owner of the deployable architecture didn't add compliance controls to their product, the full set of {{site.data.keyword.compliance_short}} goals is used. {: #cra-validate-failure}

   To view the list of added controls, go the [{{site.data.keyword.cloud_notm}} catalog](/catalog){: external} and select the deployable architecture that you're configuring. The Security & compliance tab lists all of the controls that were added to the deployable architecture.
   {: tip}

   If the validation fails, you can [troubleshoot the failure](/docs/secure-enterprise?topic=secure-enterprise-ts-na-failures#na-checks-fail). Or, an administrator can review the results through the {{site.data.keyword.bpshort}} service and [override the failure and approve](/docs/secure-enterprise?topic=secure-enterprise-approve-failed-validation) the configuration to deploy anyway. However, ensure that the pipeline failed due to the Code Risk Analyzer scan and not because of a validation or plan failure. It is not recommended to override a failure that is flagged due to a validation or plan failure as the configuration will not deploy successfully. For more information about security and compliance in projects, see [Achieving continuous compliance as an enterprise](/docs/secure-enterprise?topic=secure-enterprise-continuous-compliance).

During the configuration and deployment process, monitor your [needs attention items](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects). The widget reflects any issue that occurs in your configurations.
{: remember}

## Deploying your configuration
{: #deploy-config}

After you validate your configuration, you can deploy it to your target account.

1. Review the input values and make any necessary changes.
1. Check that there aren't any outstanding needs attention items. Needs attention items can block your ability to deploy.
1. Click **Deploy**. This action includes preparing your resources to deploy, which can take a few minutes. You are notified when the deployment is successful.
1. Review the outputs from the deployable architecture.

If any additional changes to the configuration are needed, or if a new version of the deployable architecture is available, you must deploy your configuration again. You must also deploy your configuration again [if there is any drift detected](/docs/schematics?topic=schematics-drift-note&interface=ui#drift-ui) in your {{site.data.keyword.bpshort}} workspace.

## Viewing resources
{: #resources-project}

View your resources that are tied to the deployable architecture configuration by completing the following steps:

1. From the projects list, select a project.
2. Go to the **Configurations** tab, and select a deployable architecture configuration.
4. From the **Resources** tab, you can view the full list of deployed resources. For additional information, click **View in {{site.data.keyword.bpshort}}**.

## Reviewing output values
{: #project-output-values}

Output values populate after the configuration is deployed. They provide important information about your created resources. After the deployment is successful, you can go to the **Output** tab to view the outputs for your configuration.
