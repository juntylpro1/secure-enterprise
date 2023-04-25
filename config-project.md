---

copyright:

  years: 2022, 2023

lastupdated: "2023-04-25"

keywords: manage project, rename project, move project, deploy project, merge request, merge changes

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Configuring and deploying a deployable architecture
{: #config-project}

After you add a deployable architecture to your project, you can edit the input values to configure the architecture for deployment.
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

1. From the **Security** panel, select the authentication method that you want to use to deploy your architecture.

    Add an API key by using {{site.data.keyword.secrets-manager_full}}. This authorizes the project to deploy to a target account and is required to deploy your configuration. For more information, see [Using an API key with Secrets Manager to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    {: note}

1. During validation, a Code Risk Analyzer scan is run on your architecture. Select the controls that you want to use during validation. You can use the **Architecture default** controls, or the **Select from {{site.data.keyword.compliance_short}}** option if you have an attachment set up in your target account. {: #cra-validate-failure}

    If you select **Architecture default**:
    * The scan uses the default controls that the owner of the deployable architecture added when they onboarded it.
    * Controls that the architecture owner added that are also included in the [supported set of {{site.data.keyword.compliance_short}} rules](/docs/code-risk-analyzer-cli-plugin?topic=code-risk-analyzer-cli-plugin-cra-cli-plugin#terraform-scc-goals) are checked.
    * Any extra controls that the architecture owner added that are not included in the list of supported rules are not checked when you validate your configuration.
    * If the owner of the deployable architecture didn't add compliance controls to their product, the full set of {{site.data.keyword.compliance_short}} rules is used.

    To view the list of added controls, go the [{{site.data.keyword.cloud_notm}} catalog](/catalog){: external} and select the deployable architecture that you're configuring. The Security & compliance tab lists all of the controls that were added to the deployable architecture.
    {: tip}

    If you select **Select from {{site.data.keyword.compliance_short}}**, you must have an instance of the service and an attachment through {{site.data.keyword.compliance_short}} in the target account that you want to deploy to. For help creating an attachment, see [Evaluating resource configuration with {{site.data.keyword.compliance_long}}](/docs/secure-enterprise?topic=secure-enterprise-security-compliance-scanning).

1. From the **Required** panel, enter values for the required fields for the deployable architecture configuration.
1. Optional: You can add values by going to the **Optional** panel.
1. Click **Save**.
1. Click **Validate**. The modal that is displayed provides more details about your in-progress validation.

   If the validation fails, you can [troubleshoot the failure](/docs/secure-enterprise?topic=secure-enterprise-ts-na-failures#na-checks-fail). Or, an administrator on the projects service can review the results through the {{site.data.keyword.bpshort}} service and [override the failure and approve](/docs/secure-enterprise?topic=secure-enterprise-approve-failed-validation) the configuration to deploy anyway. However, ensure that the pipeline failed due to the Code Risk Analyzer scan and not because of a validation or plan failure. It is not recommended to override a failure that is flagged due to a validation or plan failure as the configuration will not deploy successfully. For more information about security and compliance in projects, see [Achieving continuous compliance as an enterprise](/docs/secure-enterprise?topic=secure-enterprise-continuous-compliance).

During the configuration and deployment process, monitor your [needs attention items](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects). The widget reflects any issue that occurs in your configurations.
{: remember}

## Approving changes
{: #approve-changes}

After you validate your configuration, the changes must be approved by an editor or administrator on the projects service. Complete the following steps to approve changes:

1. From the projects list, select a project.
1. Check that there aren't any outstanding needs attention items on the **Overview** tab in your project. Needs attention items can block your ability to deploy.
1. Go to the **Configurations** tab, and select a deployable architecture configuration.
1. Click **Edit**.
1. Click **View last validation**.
1. Add a comment providing more details about the approval, and click **Approve**.

If your validation failed due to the Code Risk Analyzer scan, an administrator on the projects service can [override the failure and approve](/docs/secure-enterprise?topic=secure-enterprise-approve-failed-validation) the configuration to deploy anyway.
{: remember}

## Deploying your architecture
{: #deploy-config}

After your configuration updates are validated and approved, you can deploy your architecture to your target account. You can deploy to any account that has authorized your project for deployments. For more information, see [Using an API key with Secrets Manager to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).

1. From the **Configurations** tab in your project, click the name of your deployable architecture configuration > **Edit**.
1. Review the input values and make any necessary changes.
1. Click **Deploy**. This action includes preparing your resources to deploy, which can take a few minutes. You are notified when the deployment is successful.
1. Review the outputs from the deployable architecture.

If any additional changes are needed, or if a new version of the deployable architecture is available, you must deploy your architecture again. You must also deploy your architecture again [if there is any drift detected](/docs/schematics?topic=schematics-drift-note&interface=ui#drift-ui) in your {{site.data.keyword.bpshort}} workspace.

## Viewing resources
{: #resources-project}

View your resources that are tied to the deployable architecture configuration by completing the following steps:

1. From the projects list, select a project.
2. Go to the **Configurations** tab, and select a deployable architecture configuration.
4. From the **Resources** tab, you can view the full list of deployed resources. For additional information, click **View in {{site.data.keyword.bpshort}}**.

## Reviewing output values
{: #project-output-values}

Output values populate after the architecture is deployed, and they provide important information about your created resources. After the deployment is successful, you can go to the **Output** tab to view the outputs.
