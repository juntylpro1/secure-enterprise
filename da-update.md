---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-13"

keywords: onboard, catalog management, private catalog, catalog manifest, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Editing your deployable architecture
{: #edit-da}


After your deployable architecture is added to a private catalog, you can use the console to continue to make changes to your product information and add new versions of your architecture. 



If you prefer to make the changes locally, you can always use the [available manifest values](/docs/secure-enterprise?topic=secure-enterprise-manfest-values) to update your catalog manifest file.
{: tip} 




## Before you begin
{: #edit-da-before}

Before you can start sharing your deployable architecture with others, be sure that you have the following prerequisites.

* The required access to work with private catalogs and deployable architectures.
    * Administrator on all account management services and all IAM services.
    * Editor on the catalog management service.
    * Manager service access role for {{site.data.keyword.bplong}}.
    * Other roles that are required for specific resources in your customized deployable architecture.
* A private catalog.
* A [deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-create-da) that you have previously onboarded into a private catalog.

    Don't have a deployable architecture ready to use? [Use the sample deployable architecture to test the flow](https://github.com/IBM/catalog-create-sample-da){: external}.
    {: tip}



## Editing offering details
{: #edit-da-details}

To edit the details about your deployable architecture after it's been created, you can use the following steps.

1. Go to the **Manage > Catalogs > Private catalogs** page of the console.
2. Select the private catalog that you want to add a product to. The catalog details page opens.
3. Select the product that you want to provide more details for.
4. On the details page, click **Edit**.
5. Make your desired changes.
6. Click **Save**.
7. From the **Actions** drop-down, select **Download manifest**. 
8. Replace the `ibm_catalog.json` file in your source code repository.
9. Create a new release.
10. Add it to the catalog as a new version of your deployable architecture.


## Editing product details
{: #specify-details}

