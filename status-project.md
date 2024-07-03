---

copyright:
  years: 2023
lastupdated: "2024-07-03"

keywords: project status, manage status, needs attention, partial deployment, deploy project, validate project, validate configuration, deploy configuration

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring the status of a configuration
{: #monitor-status-projects}

In a project, a configuration has one status: either draft or deployed. However, configurations go through many changes that you can track throughout the configuration's lifecycle. You can find more information about the detailed status of a configuration by opening the configuration within your project.

## Understanding configuration status
{: #understand-config-status}

The following table shows an example lifecycle of a configuration from creation through deployment.

| Configuration action | Status in the project | Detailed configuration status | Next steps |
| -------------- | -------------- | -------------- | -------------- |
| Create a configuration | Draft | N/A | Edit, save, and validate the changes |
| Validate the configuration | Draft | Validation failed | Edit, save, and validate the changes |
| Validate the configuration | Draft | Validation successful | Approve |
| Approve | Draft | Approved | Deploy |
| Deploy | Draft | Changes failed to deploy | Edit and deploy again |
| Deploy | Deployed | Changes deployed | No other actions are necessary, but you can still edit the configuration, validate it, and deploy any changes. |
{: caption="Table 1. Status of a configuration in a project compared to the detailed status within the configuration and next steps." caption-side="bottom"}

When you deploy a draft configuration, the status of the configuration changes to deployed within your project. After a configuration is deployed, you can still edit the configuration and deploy changes. If you do so, the status of the configuration remains deployed within your project.

## Understanding resource status
{: #understand-resource-status}

You can track resources that were created by a deployment from the Resources tab in your configuration. From there, you can endeploy resources or view more information about the status of your resources. For more information, see [Undeploying resources](/docs/secure-enterprise?topic=secure-enterprise-remove-resources&interface=ui).

If your changes failed to deploy, some or all of the resources weren't created by {{site.data.keyword.bplong}}. The Resources tab in your configuration does not include the resources that weren't created successfully.
