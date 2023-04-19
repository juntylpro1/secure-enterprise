---

copyright:
  years: 2023
lastupdated: "2023-04-18"

subcollection: secure-enterprise

keywords: 

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using deployable architectures
{: #responsibilities-deployable-architectures}

Learn about the management responsibilities and terms and conditions that you have when you use deployable architectures. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for using {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use a deployable architecture. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops-da}

Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Monitor the status of a deployable architecture | {{site.data.keyword.IBM_notm}} provides the ability for customers to monitor the lifecycle of the deployable architecture.  | Use the [needs attention widget](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects) or [enable Event Notifications](/docs/secure-enterprise?topic=secure-enterprise-event-notifications-events) to monitor events that specifically impact the lifecycle of your deployable architecture.  |
|Monitor the status of a product spun up by your deployable architecture | IBM provides the ability for customers to monitor the lifecycle of the instances. | Use the resource list, service instance pages, or the [Status](https://cloud.ibm.com/status){: external} page to monitor events that specifically impact your service instance. |
{: row-headers}
{: caption="Table 1. Responsibilites for incident and operations" caption-side="bottom"}
{: summary="The first column describes the task that a customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Change management
{: #change-management-da}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

|Task  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Creation of the IBM Cloud deployable architectures | {{site.data.keyword.IBM_notm}} provides the base pattern as a deployable architecture for instantiation through Terraform.  | N/A  |
|IBM Cloud Terraform Provider | {{site.data.keyword.IBM_notm}} publishes Terraform provider of all Terraform enabled services on IBM Cloud.  | N/A  |
|Third-party Terraform Providers used within templates | N/A  | Customer is responsible for any use of third-party Terraform code that is used with the deployable architecture.  |
|Running default configuration (out of the box)| {{site.data.keyword.IBM_notm}} provides the ability for customers to create and deploy configurations of deployable architectures by using projects, Terraform-as-a-service, or the projects CLI.  | Use projects to [configure and deploy a deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project).  |
|Running templates locally by using Terraform directly | N/A  | Customer can run the deployable architecture on their local system.  |
|Customize modules or deployable architectures with pre-supported modules | {{site.data.keyword.IBM_notm}} provides and supports base Terraform modules for services on IBM Cloud, and provides preset JSON configuration overrides for templates. | Customer can use these base Terraform modules to extend their base deployable architecture pattern.  |
|Workload Managment (Application Migration and Backup/Restore) | N/A | Customer responsibility to manage and migrate application workloads. |
|Updates, fixes, and new features| {{site.data.keyword.IBM_notm}} provides regular updates and bug fixes, as well as new features following a continuous delivery model in a manner transparent to the customer.  | N/A |
|Issues found in IBM-provided versions of Terraform modules | {{site.data.keyword.IBM_notm}} provides a way for customers to open issues. If the issue is with a deployable architecture, open a case. If the issue is with a module, open an issue in the module [GitHub repo](https://github.com/terraform-ibm-modules){: external}. | Customer provides information to reproduce any problem. |
|Issues with IBM Container images | {{site.data.keyword.IBM_notm}} provides a way for customers to open issues. | Customer provides information to reproduce any problem. |
|Issues with third party and open source Container Images | N/A | Customer resolves with third-party vendor or open source community. |
|Issues with {{site.data.keyword.cloud_notm}}-provided stock operating system images | N/A | Customer must get a compatible stock image from the vendor. |
|Issues with the services the Terraform creates from a deployable architecture | {{site.data.keyword.cloud_notm}} will resolve issues with the services. | N/A |
| {{site.data.keyword.cloud_notm}} resource outages or issues that occur during automated template execution by using {{site.data.keyword.cloud_notm}} Terraform Provider | IBM reports outages for any cloud resources on the [Status](https://cloud.ibm.com/status){: external} page. | Customers can redeploy after issue is resolved.|
| {{site.data.keyword.cloud_notm}} catalog and private catalog support | {{site.data.keyword.IBM_notm}} provides a way for you to discover available deployable architectures in our public catalog and save your versions to a private catalog. | N/A |
| Provide ability for drift detection | {{site.data.keyword.IBM_notm}} notifies you if your instantiated resources differ from the base pattern. | Customer decides when to remediate any configurations detected in drift detection. |
|Pulling deployable architecture changes into a project| {{site.data.keyword.IBM_notm}} provides the ability for customers to update the version of a deployable architecture in a project, if a new version becomes available. | Customers are [notified when a new deployable architecture version is available](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects#na-version-update) so they can update their project. \n \n Customers can save their existing project data through an API, CLI, or by [exporting the project.json](/docs/secure-enterprise?topic=secure-enterprise-setup-project#json-export) from the UI that can be used as backup or as rollover plan if there is an issue.  \n \n Customers can then test the deployable architecture changes by deploying in a development or test environment before going to production.  This can all be done within the same project.  |
|Deleting a deployable architecture| {{site.data.keyword.IBM_notm}} provides the ability for customers to delete a deployable architecture.  | Customers can [delete a deployable architecture]() whenever they need to. |
{: row-headers}
{: caption="Table 2. Responsibilites for change management" caption-side="bottom"}
{: summary="The first column describes the task that a customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Identity and access management
{: #iam-responsibilities-da}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Accessing deployed deployable architectures | {{site.data.keyword.IBM_notm}} provides the ability to control user access to resources provisioned through projects.  | Use Identity and Access Management (IAM) to [assign users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project). |
|Authorize a project to deploy a deployable architecture configuration| {{site.data.keyword.IBM_notm}} provides the ability to authorize a project to deploy a deployable architecture configuration.  | Choose an authentication method to authorize a project to deploy in an account. It’s recommended to use a trusted profile, but you can use an API key or an existing secret to [authorize a project to deploy](/docs/secure-enterprise?topic=secure-enterprise-authorize-project) in an account.  |
{: row-headers}
{: caption="Table 3. Responsibilites for identity and access management" caption-side="bottom"}
{: summary="The first column describes the task that a customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Security and regulation compliance
{: #security-compliance-da}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

|  Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Apply patches and security updates to operating system in customer instances | IBM notifies you of updates. | Customer must apply all updates. |
| Install software and OS patches into customer-managed virtual machines | N/A | Customer must apply all patches. |
| Meet security and compliance objectives| Provide a secure deployable architecture that complies with declared standards. For more information about data security, see [How do I know that my data is safe?](/docs/overview/terms-of-use?topic=overview-security).  | Secure your workloads and data. Integrate tools into your toolchains that satisfy your security and compliance requirements. To learn more about securing your cloud apps, see [Security to safeguard and monitor your cloud apps](https://www.ibm.com/cloud/architecture/architecture/practices/securing-cloud-native-apps-risks-mitigation/){: external}.  |
{: row-headers}
{: caption="Table 4. Responsibilites for security and regulation compliance" caption-side="bottom"}
{: summary="The first column describes the task that a customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Disaster recovery
{: #disaster-recovery-da}

Disaster recovery includes tasks such as providing dependencies on disaster recovery sites, provision disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Meet disaster recovery objectives| {{site.data.keyword.IBM_notm}} follows best practices for disaster recovery. All {{site.data.keyword.IBM_notm}} applications automatically recover and restart after any disaster event. For more information about disaster recovery, see the [{{site.data.keyword.IBM_notm}} Disaster Recovery Plan](/docs/overview?topic=overview-zero-downtime#disaster-recovery).  | Customer can help meet disaster recovery objectives by deploying their project in a development or test environment before deploying to production. \n \n There are no other actions that the customer needs to take to prepare for an event of a catastrophic failure in a region.   |
| Meet high availability objectives| {{site.data.keyword.cloud_notm}} is available globally and load balanced from a single URL. It is highly available and continues to run even if your resources are unavailable. For more information about high availability, see the [{{site.data.keyword.IBM_notm}} service level objectives](/docs/overview?topic=overview-slo) and the [sample application architecture](/docs/overview?topic=overview-bcdr-app-recovery). | N/A |
{: row-headers}
{: caption="Table 5. Responsibilites for disaster recovery" caption-side="bottom"}
{: summary="The first column describes the task that a customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}
