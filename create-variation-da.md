---

copyright:
   years: 2024
lastupdated: "2024-05-08"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Creating a deployable architecture variations
{: #create-variation-da}



A deployable architecture can include variations of capability or complexity. For example, you might create a quick start variation with basic capabilities for simple, low-cost deployment, and then you might have a standard variation with a more complex architecture that would be used in production. Each of these variations is itself a deployable architecture, which is onboarded and configured to appear together as options for the same tile in the IBM Cloud catalog.
{: shortdesc}


If you're working in the `ibm_catalog.json` catalog manifest file, `variations` are referred to as `flavors`. However, in all user-facing documentation and the catalog details page, they are referred to as variations.
{: tip}

Here's an example of a deployable architecture with two variations in the IBM Cloud catalog as a user would see it. These are two variations that use the same product name and version during onboarding to the catalog to ensure that they show up side by side after a user selects the catalog tile in the IBM Cloud catalog:

![A deployable architecture with two variations](images/variation-example.png "Deployable architecture with two variations"){: caption="Figure 1. Deployable architecture with two variations" caption-side="bottom"}

## How to decide if it's a variation
{: #decide-variation}


Typically, you have a core architecture pattern that solves a specific business problem. For example, Landing zone is used to have a secure network for workloads to run in. The variations of the core architecture often vary in the following key areas:

- Cost
- Compliance
- Complexity in time and use
- It deploys something different for a specific use case, but solves the same overall business problem (for example, single site vs. cross-regional Object Storage buckets)


## Starting with multiple variations
{: #multiple-variations}

When you first onboard your deployable architecture (Terraform or stack) to the IBM Cloud catalog, you might have more than one variation ready. This means that you have multiple working directories in your `terraform-ibm-modules` repo, and your `ibm_catalog.json` file has multiple `flavors` specified with all of the accompanying details like required IAM permissions, compliance claims, dependencies, architecture features and diagram, and so on.

The outcome of onboarding these variations and creating your first IBM Cloud catalog tile is that you will have one tile in the catalog and then multiple options within that tile that users can evaluate and select from when determining which option they want to deploy. Typically, from a user's perspective, these variations have different costs, included features, capacity requirements, and so on. You might see "Quick start" and "Standard" variations. Usually, that Quick start variation will cost less, deploy less resources, possibly have less or no compliance claims, and simply be a way for the user to kick the tires before spending a lot of money.

After your automation code and manifest detailing the variations is available as a Git release in your source repo, you can onboard the two or more variations to create your first tile:

1. Go to **Manage > Catalogs**, then click **Private catalogs**.
1. Select the row for an existing private catalog or click **Create** for a new one.
1. Click **Add product**, enter the required details for the first deployable architecture variation, and then click **Add product**.
1. Review the catalog entry details and make adjustments as needed.
1. Click **Versions**, then click **Add version**.
1. Enter the required information for the second variation.

   The source URL of the repo release will be the same for all of the variations within that release and they should be imported with the same version number. The product name and version number are how the variations are linked together and then result as options on the same catalog tile.
   {: tip}

1. Click **Add version**.
1. Now follow the steps in the console to complete the review and validation of this variation.

   On the **Add deployable architecture details** page, step 3 includes adding highlights. These are known as features in the `ibm_catalog.json` manifest file. You might have already added these in the manifest, so you can review them here. If not, go ahead and add some highlights. These should be short ability, process, capacity, or other features of this specific architecture. You will use the same highlight "Name" across all variations. The description is where there should be differences. This enables users to evaluate the differences in the architectures by using the text highlights on the catalog details page.
   {: important}

1. Go back to the Verions page, and click on the version that you haven't validated yet, and repeat the process to review the details and validate this version.

If you plan to publish to the IBM Cloud catalog, after both versions have been validated, you can import them to Partner Center and your product manager can continue the onboarding process by getting approval to [publish in the IBM Cloud catalog](/docs/solution-as-code?topic=solution-as-code-publish-da).

If you don't plan to publish to the IBM Cloud catalog, you can choose to publish to the [community registry](/docs/solution-as-code?topic=solution-as-code-publish-community-da) or [share with users that have access to the private catalog](/docs/secure-enterprise?topic=secure-enterprise-catalog-enterprise-share&interface=ui) or specify other accounts or enterprises that you have access to share with.
{: tip}


## Adding a variation to an existing deployable architecture
{: #add-variation}

A variation that is being added to an existing deployable architecture is treated as a deployable architecture as far as requirements are concerned, such as including the same artifacts like a reference architecture and readme file, and so on. If you're adding to a tile in the IBM Cloud catalog, it must go through the Service Framework requirements and Partner Center approval process.

The main difference is that you store the automation and reference architecture in your existing `terraform-ibm-modules` repo and when you onboard it, you link it to the existing deployable architecture tile that you want it to be a variation of, so that a new tile in the catalog isn't created.

To add a variation to an existing deployable architecture tile in the catalog, you must complete the following steps:

1. Create the deployable architecture for this variation including the automation code, architecture diagram, reference architecture, readme file, and so on.
1. Add it to your existing repo in `terraform-ibm-modules`:
   * Add your code to a new working directory in your existing repo.
   * Update the `reference-architectures` folder with the new architecture diagram and design requirements heatmap. For more information about reference architectures, see [Creating reference architectures](/docs/writing?topic=writing-reference-architectures).
   * Add to the flavor array in the `ibm_catalog.json` to include the details for this new variation. For more information about the fields in this section, see [Specifying product metadata](https://test.cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-manifest#value-variations).
   * Create a release. You will need this URL to onboard to the IBM Cloud catalog.
1. Onboard this variation to the IBM Cloud catalog.
   1. Go to **Manage > Catalogs**, then click **Private catalogs**.
   1. Select the row for your private catalog that has the existing deployable architecture that this is a variation of.
   1. Select the row for your deployable architecture.
   1. Click **Versions**.
   1. Click **Add version**.
   1. Enter the required details for Delivery method, repo type, and add the Source URL for the new release (`.tgz`). By using this URL, the name of your new variation should be available as a selection.
   1. For Software version, if you are not updating the original version of your existing variation, then enter the same version number as the other that is already in the private catalog. If you are updating the original variation while also adding the new variation, specify a new version number. Then, repeat this process using the same version number to add the updated version of the existing variation in your private catalog.

      The version number and product name being the same between variations is how they get linked together as options in the catalog details page for a single deployable architecture tile.
      {: note}

   1. Follow through the console flow to continue to onboard, validate, and publish this variation.

      Make sure to use the same features list as the other variations for the deployable architecture with custom responses that show how this variation meets each (or doesn't). This list of features helps users compare variations in the catalog. See the following example showing where you can set these in the `ibm_catalog.json` or the console onboarding flow.
      {: tip}

      ![Adding variation features](images/variation-features.png "Adding variation features"){: caption="Figure 1. Adding variation features" caption-side="bottom"}
1. Get approval to publish this variation to the IBM Cloud catalog in Partner Center. For more information about importing a new version and going through the approval center in Partner Center, see [Publishing a deployable architecture to the catalog](/docs/solution-as-code?topic=solution-as-code-publish-da).

   If you don't plan to publish to the IBM Cloud catalog, you can choose to publish to the [community registry](/docs/solution-as-code?topic=solution-as-code-publish-community-da) or [share with users that have access to the private catalog](/docs/secure-enterprise?topic=secure-enterprise-catalog-enterprise-share&interface=ui) or specify other accounts or enterprises that you have access to share with.
   {: tip}
