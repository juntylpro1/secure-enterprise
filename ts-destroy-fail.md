---

copyright:
  years: 2023
lastupdated: "2023-04-17"

keywords: troubleshoot projects, destroy resources, destroy resources failed, needs attention failure, resource failure, needs attention, failure, destroy, resources

subcollection: secure-enterprise

content-type: troubleshoot
---

{{site.data.keyword.attribute-definition-list}}

# Why were my resources not destroyed?
{: #ts-destroy-failed}
{: troubleshoot}

You tried to destroy resources, but it failed.
{: shortdesc}

The project displays a **Needs attention** alert and a message displays on the **Activity** tab that states that the resources were not destroyed.
{: tsSymptoms}

Go to the needs attention widget on the **Overview** tab and select **Destroy resources failed** to view the {{site.data.keyword.bpshort}} logs, which provide more information about the failure.
{: tsCauses}

* Permissions for the API Key or trusted profile were changed: For more information about the required access for trusted profiles, see [Using trusted profiles to authorize projects](/docs/secure-enterprise?topic=secure-enterprise-tp-project).
* A service was down when you tried to destroy resources: Check the [Status page](/status){: external} for the service, and try to destroy resources again when the service is back up.
* The deployable architecture that your configuration is based on contains bugs that caused a failure when you tried to destroy resources.
* Though not recommended, some resources might need to be destroyed one by one in the {{site.data.keyword.bpshort}} resource list. For more information, see [Destroying resources created by projects](/docs/secure-enterprise?topic=secure-enterprise-best-practices-projects#project-resources-destroy).
{: tsResolve}
