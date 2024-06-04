---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-09"

keywords: onboard, catalog management, private catalog, catalog manifest, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Versioning your deployable architecture in the catalog
{: #version-da-catalog}

As changes are made to your deployable architecture for various reasons, you can make the new versions of your architecture available through the catalog by importing a new version and making the neccessary configurations through the console or catalog manifest file.
{: shortdesc}


## Importing a new version by using the console
{: #custom-import-ui}
{: ui}

1. Go to **Manage** > **Catalogs** > **Private catalogs** in the {{site.data.keyword.cloud_notm}} console.
1. Select the private catalog where you want to add your product, and click **Add**. If you do not have any private catalogs, click **Create** to add one.
1. Select **Deployable architecture** as the type of the product that you're adding.
1. Choose **Terraform** as your delivery method.
1. Select the type of repository. If the source for your deployable architecture is located in a private repository, you need to authenticate with a personal access token.
1. Enter the source URL. This source URL ends in `tar.gz` and must point to the release snapshot for the version that you're importing.
1. If you created multiple variations of the customized deployable architecture, select the variation you'd like to import first. Variations are used to provide different options within your single catalog tile. For example, a single deployable architecture might have proof of concept and production workload variations as options for users to choose from when deploying.
1. Enter the software version in the format of major version, minor version, and revision, for example `1.0.0`. Typically, this version matches the version number of your release snapshot.

   If there are multiple variations for a single deployable architecture, make sure that you're using the same version for all variations. This way all variations appear as options on the tile in the catalog.
   {: important}

1. Select a category. The following two categories are commonly used for deployable architectures: Converged infrastructure and Enterprise applications. If you included a category in your catalog manifest file, it is automatically imported.
1. Click **Add product**.
1. If your deployable architecture has multiple variations, click **Add version** to import your next variation. The delivery method, repository type, source URL, and software version must match the information in your catalog manifest JSON. Each variation must be added as a separate version of your deployable architecture. When you are done adding all of the variations, continue to the next step.

## Importing a new version by using the CLI
{: #custom-import-cli}
{: cli}

First, install the {{site.data.keyword.cloud_notm}} CLI. For more information, go to [Get started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

Complete the following steps to import your deployable architecture to a private catalog. When a `ibm_catalog.json` catalog manifest file is present, certain metadata is automatically imported to the private catalog when you import a product.

1. Run the [ibmcloud catalog create](/docs/cli?topic=cli-manage-catalogs-plugin#create-catalog) command to create a private catalog. Private catalogs provide a way for you to manage access to products for users in your account. If you already have a private catalog that is created, you can skip this step.

    ```bash
    ibmcloud catalog create --name CATALOG [--catalog-description "DESCRIPTION"]
    ```
    {: codeblock}

1. Run the [ibmcloud catalog offering create](/docs/cli?topic=cli-manage-catalogs-plugin#create-offering) command to add the deployable architecture to your private catalog.

    ```bash
    ibmcloud catalog offering create [--catalog CATALOG-NAME] [--zipurl URL]
    ```
    {: codeblock}

    If you want to import from a private repository, you can use a personal access token by adding `[--token TOKEN]` to your command.
    {: important}

1. Run the [ibmcloud catalog offering add-category](/docs/cli?topic=cli-manage-catalogs-plugin#add-category-offering) command to add a category to your product. If no category is selected, the **Developer tools** category is added by default for new products.

    If you included a category in a catalog manifest file, you can skip this step.
    {: note}

    ```bash
    ibmcloud catalog offering add-category --catalog CATALOG_NAME [--offering OFFERING] [--category CATEGORY]
    ```
    {: codeblock}

1. Run the [`ibmcloud catalog offering import-version`](/docs/cli?topic=cli-manage-catalogs-plugin#import-offering-version) command for each variation of your deployable architecture:

    ```sh
    ibmcloud catalog offering import-version -c <CATALOGID> -o <OFFERINGID> --zipurl <TGZ> --flavor <FLAVOR_LABEL>
    ```
    {: codeblock}