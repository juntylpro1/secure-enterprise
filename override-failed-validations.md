---

copyright:

  years: 2023, 2024

lastupdated: "2024-06-04"

keywords: project, validation, failures, failed validation, failed, override, approve, administrator

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Approving failed validations
{: #approve-failed-validation}

As an administrator on the {{site.data.keyword.cloud}} Projects service, if the validation pipeline didn't complete or succeed, you can override the failure and approve it.
{: shortdesc}

Before you override a failed validation, ensure that the pipeline failed due to a Code Risk Analyzer scan and not because of a validation or plan failure. If you override a failure because of a validation or plan failure, approving isn't recommended because the configuration won't deploy successfully.
{: important}

## When to approve a failed validation
{: #override-when}

There might be a couple scenarios where you'd want to override a failed validation. If a major customer-impacting event requires you to make updates quickly, you might want to deploy your changes even at the risk of introducing compliance errors, which can be fixed later.

Sometimes, compliance errors are introduced that aren't applicable to your configuration or business needs. For example, if your {{site.data.keyword.cos_short}} bucket resiliency is not set to cross region, the corresponding compliance goal will fail. However, this compliance issue might not impact your business if you don't need maximum availability and want to deploy your configuration to only one region.

To approve a failed validation, complete the following steps:

1. From the projects list, select a project.
1. Go to the **Configurations** tab, select a deployable architecture configuration, and click **Edit**.
1. Select **View details** from the menu.
1. Review the issues that caused the validation to fail.
1. If you want to approve the changes, select **Override and approve**.
1. Add a comment that explains why you're approving the changes.
1. Click **Override and approve**.
