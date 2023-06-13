---

copyright:

  years: 2022, 2023

lastupdated: "2023-06-13"

keywords: project access, iam projects, assigning project access, assign access, access project

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Assigning users access to projects
{: #access-project}

Projects are controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). As an administrator on a project, you can grant users access to view and edit projects, approve changes, and deploy or destroy configuration resources.
{: shortdesc}

## Actions and roles for the {{site.data.keyword.cloud_notm}} Projects service
{: #service-access-projects}

The following list includes the actions that users can take when they are assigned a specific role on the {{site.data.keyword.cloud_notm}} Projects service. Review the following information to make sure that you are assigning the correct level of access to your users.

| Role | Definition |Project Permissions |
|-------------|---------------------|---------------------|
| Viewer | Viewers can perform read-only actions within a project. | View a project (including the project.json) \n \n Find a project by using Global Search |
| Operator | Operators can perform the same actions as viewers, with more permissions beyond the viewer role, including planning project deployments | All viewer project permissions \n \n Validate a configuration \n \n Edit a configuration |
| Editor | Editors can perform the same actions as operators, with more permissions beyond the operator role, including creating projects and deploying resources. | All viewer and operator project permissions \n \n Create a project \n \n Edit a project \n \n Edit project settings \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Approve configuration changes \n \n Deploy configuration changes \n \n Destroy resources  |
| Administrator | Administrators can perform the same actions as editors, with more permissions beyond the editor role, including updating project statuses and planning new or changed project deployments. | All viewer, operator, and editor project permissions \n \n Force approve changes that failed validation |
{: caption="Table 1. Access roles for projects" caption-side="top"}

In addition, you must be assigned the following access on the project tooling resources within the account:

* The Editor and Manager role on the {{site.data.keyword.bplong}} service
* The Viewer role on the resource group for the project

An administrator on the {{site.data.keyword.cloud_notm}} Projects service must grant access between the Projects service and the {{site.data.keyword.bpshort}} service in the account that contains the project. This access is granted automatically the first time that an administrator creates a project.
{: important}

## Assigning access in the console
{: #console-project-service}

To assign access to the {{site.data.keyword.cloud_notm}} Projects service, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and then select **Access groups**.
1. Select the access group that you want to assign access to, then go to **Access** > **Assign access**.
1. For the service, select **{{site.data.keyword.cloud_notm}} Projects**. Then, click **Next**.
1. Scope the access to **All resources** or **Specific resources**. Then, click **Next**.
1. Select any combination of roles or permissions, and click **Next**.
1. Optionally, add conditions to the policy. Then, click **Review**.
1. Click **Add** to add your policy configuration to your access summary.
1. Click **Assign**.

It's a best practice to [assign access to an access group](/docs/secure-enterprise?topic=secure-enterprise-access-enterprises#bp-enterprise-access-include-how_access) and then add users to the access group, instead of assigning access to users one by one. However, you can assign access to a single user by going to **Manage** > **Access (IAM)** > **Users** and selecting the user you want to assign access to.
{: tip}

## Access to the project tooling services
{: #user-create-role}

To create projects, users must have extra IAM privileges on the project tooling services.

| Service | Role | Description|
|-------------|---------------------|---------------------|
| {{site.data.keyword.bpshort}} | Editor & Manager | Allows a {{site.data.keyword.bpshort}} workspace to be created to deploy the other tooling services and additional workspaces to be created for each configuration. |
| Resource Group | Viewer | Allows a resource group for the project to be selected to deploy the tooling services. |
{: caption="Table 2. Access roles for project creators" caption-side="top"}
