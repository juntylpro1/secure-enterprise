---

copyright:

  years: 2023, 2024

lastupdated: "2024-02-20"

keywords: target account, manage resources, enterprise architecture, administration account, resources, existing resources, organize resources

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Organizing existing resources by using a project
{: #organize-resources}

You can use a project to organize and track resources across accounts, which can help large enterprises [separate management accounts from workload accounts and applications](/docs/enterprise-account-architecture?topic=enterprise-account-architecture-principles#mgmt-workload). Separating management accounts from workload accounts reduces the number of users who need access to your workload accounts, which makes those accounts more secure. For example, you can gather resources that are related to a particular workload across your development and production accounts into a single project in an administration account. By doing so, your resources remain deployed in their respective accounts, but you gain an at-a-glance view of those resources in your project. 
{: shortdesc}

This is an experimental feature that is available for evaluation and testing purposes and might change without notice.
{: experimental}

![An enterprise account with an administration account and two business unit account groups A and B. Account group B contains an administration account and two other accounts, workload accounts A and B. The group B administration account includes a project with two configurations that contain resources from workload accounts A and B.](images/manage-resources.svg "An administration account that tracks resources from business unit accounts"){: caption="Figure 1. An administration account that tracks resources from business unit accounts" caption-side="bottom"}

Within an enterprise account architecture, tracking resources in a project can help a user in a [business unit administration account](/docs/enterprise-account-architecture?topic=enterprise-account-architecture-bu-admin-account) manage separate workload accounts and applications. The resources exist in different accounts, for example, workload account A, and workload account B. But by adding resources from workload account A and B to a project in the administration account, the resources are visible from the project in the administration account as well. 

Within a project, you can further refine groups of resources by adding them to different configurations. Consider grouping the resources based on their function. For example, within the same project, you can add one configuration that contains the resources for your infrastructure on your development environment, and another configuration for the resources on your production environment. 
{: tip}

## Watch and learn
{: #watch-and-learn}

Prefer to see it in action? Check out the following video to learn how to organize existing resources in your project by using the console.

![Organizing existing resources in a project](https://www.youtube.com/embed/3QzfoswV0S8?si=pye4vobzYP_i4xdH){: video output="iframe" data-script="#video-transcript-resources" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

### Video transcript
{: #video-transcript-resources}
{: notoc}

{{site.data.keyword.cloud_notm}} is working on a new feature to organize resources by using a project.

Within your project, this is achieved by creating a configuration from existing resources. 

After you create your configuration, provide authentication details for the target account that contains your existing resources. 

After you’ve authenticated with the target account, click **Add** to select resources.

When you’re done selecting your resources, click **Save draft** to save your changes. 

Then, click **Apply changes** to finalize your draft and add your resources to the project. 

Within your configuration, you now have a view of the existing resources from your target account. 

Moving forward, we’re exploring ways to automatically organize resources in a project, and provide meaningful data in your project, like usage and cost information.

## Before you begin
{: #prereq-resources}

Make sure that you are assigned the following access in the account that contains your project: 
* The Editor role or greater on the {{site.data.keyword.cloud}} Projects service.
* The Viewer role on the resource group for the project. 

<!-- Make sure that you are assigned the following access in the target account that contains your existing resources: 
* The Viewer role for All Identity and Access enabled services. Scope the access to all resources. 
* The Viewer role for the resource group that contains the existing resources.  -->

You must also have an authentication method to grant your project access to the account that contains your resources. You can [use an API key or secret](/docs/secure-enterprise?topic=secure-enterprise-authorize-project) or you can [use a trusted profile](/docs/secure-enterprise?topic=secure-enterprise-tp-project) to grant your project access. Make sure that the API key or trusted profile has the following access: 
* The Viewer role for All Identity and Access enabled services. You can allow access to all resources, or [scope the access to a select few](/docs/secure-enterprise?topic=secure-enterprise-tp-project#serviceid-access-existing-resources). 
* The Viewer role for the resource group that contains the existing resources. 

## Adding existing resources to a project
{: #add-existing-resources}

To add existing resources to a project, complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **[Projects](/projects/)** and create or select a project. 
1. In the project, go to the Configurations tab and select **Create** > **From existing resources** and enter a name for your configuration. 
1. In the Configure section, select an authentication method that you want to use to authenticate with the target account that contains your resources.
1. In the Add resources section, click **Add**.
1. Select the resources that you want to organize in your project, and click **Add**. 

   Resources that are in a {{site.data.keyword.bplong}} workspace or were already added to another configuration can’t be added and don't display in the list of resources. Some resources might not be included in the list if the authentication method was scoped to specific resources, as opposed to all of them.
   {: note}

1. Click **Save draft** to save your changes as a draft. 
1. Click **Apply changes** to finalize your draft and add your resources to the project. 

Within your configuration, the resources that you added are listed on the Resources tab. 
