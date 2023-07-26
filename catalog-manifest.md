---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-26"

keywords: onboard, catalog management, private catalog, catalog manifest, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Specifying product metadata for onboarding a product to a private catalog
{: #manifest}

When you prepare to onboard a version of a deployable architecture or software to a private catalog, you can use a JSON file that is named `ibm_catalog.json`, also referred to as a catalog manifest file, to automatically import product and version information. By using this file, you can avoid manually entering metadata in the console each time you onboard a new version and automate the process of onboarding products to your private catalogs.
{: shortdesc}

A catalog manifest file includes information such as the name of a product, usage instructions, security and compliance controls, IAM access requirements, and more. If you plan to automate the onboarding process by [importing a version with the CLI](/docs/secure-enterprise?topic=secure-enterprise-onboard-custom&interface=cli), you must include this file in your root directory.

You can start from the `ibm_catalog.json` file that is provided by existing deployable architectures to help reduce time and effort manually creating it. For example, if you choose to customize a deployable architecture from the {{site.data.keyword.cloud_notm}} catalog, an `ibm_catalog.json` catalog manifest file is created for you with some information included. You can review, add, edit, delete, and update the file to fit your needs.

## Creating your catalog manifest file
{: #catalog-manifest-create}

When you find a deployable architecture in the {{site.data.keyword.cloud_notm}} catalog that interests you, you can customize it to fit your business needs. Then, you can share it with accounts, account groups, or the entire enterprise from a private catalog.

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](/catalog#reference_architecture){: external}, and select a deployable architecture.
1. Click **Review deployment options** > **Customize locally** > **Start customizing** to download a customization bundle that includes a prebuilt catalog manifest file.
1. Use the following documentation to review and customize the JSON file:

   - [Catalog manifest template](#manifest-template)
   - [Catalog manifest values](#manifest-values)

You must store your catalog manifest at the root of your repository and name the file `ibm_catalog.json`.
{: important}

## Catalog manifest template
{: #manifest-template}

You can use the following template to modify an existing catalog manifest. All values are optional, and you can determine which values you want to include and which values are not needed. For more information about each value, see [Catalog manifest values](#manifest-values).

You can also see the template in a swagger format. For more information, see [Catalog Management API](https://cm.globalcatalog.cloud.ibm.com/api){: external} and find the Catalog Manifest schema.
{: tip}

```text
{
    "products": [
        {
            "label": "DISPLAY NAME",
            "name": "VERSION PROGRAMMATIC NAME",
            "version": "VERSION NUMBER",
            "product_kind": "PRODUCT KIND",
            "tags": ["TAG"],
            "keywords": ["keyword"],
            "short_description": "SHORT DESCRIPTION",
            "long_description": "LONG DESCRIPTION",
            "provider_name": "PROVIDER NAME",
            "offering_docs_url": "DOCS URL",
            "offering_icon_url": "ICON URL",
            "support_details": "SUPPORT DETAILS",
            "features": [
                {
                    "title": "TITLE",
                    "description": "DESCRIPTION"
                }
            ],
            "module_info": [
            {
                "works_with":  [
                    {
                        "catalog_id": "CATALOG ID",
                        "name": "PRODUCT PROGRAMMTIC NAME",
                        "kind": "VERSION'S FORMAT KIND",
                        "version": "VERSION NUMBER",
                        "flavors": ["FLAVOR"]
                    }
                ]
            }
            ],
            "flavors": [
                {
                    "label": "LABEL",
                    "name": "VARIATION'S PROGRAMMATIC NAME",
                    "working_directory": "PATH",
                    "usage": "USAGE",
                    "license": [
                        {
                            "name": "LICENSE NAME",
                            "url": "LICENSE URL"
                        }
                    ],
                    "compliance": {
                        "authority": "scc-v3",
                        "profiles":[
                            {
                                "profile_name": "PROFILE NAME",
                                "profile_version": "PROFILE VERSION"
                            }
                        ],
                        "controls": [
                            {
                                "profile": {
                                    "name": "PROFILE NAME",
                                    "version": "PROFILE VERSION"
                                },
                                "names": [
                                    "CONTROL NAME",
                                    "CONTROL NAME"
                                ]
                            }
                        ]
                    },
                    "iam_permissions": [
                        {
                         "service_name": "SERVICE PROGRAMMATIC NAME",
                            "role_crns": [
                                "ROLE",
                                "ROLE"
                            ],
                            "resources": [
                                {
                                    "name": "NAME",
                                    "description": "DESCRIPTION",
                                    "role_crns": [
                                        "ROLE1",
                                        "ROLE2"
                                    ]
                                }
                            ]
                        }
                    ],
                    "architecture":[
                        {
                            "features": [
                                {
                                    "title": "FEATURE NAME",
                                    "description": "FEATURE DESCRIPTION"
                                }
                            ],
                            "diagrams": [
                                {
                                    "diagram": {
                                        "url": "URL",
                                        "api_url": "API URL",
                                        "url_proxy": {
                                            "url": "URL",
                                            "sha": "SHA"
                                        },
                                        "caption": "DIAGRAM LABEL",
                                        "type": "TYPE",
                                        "thumbnail_url": "THUMBNAIL URL"
                                    }
                                }
                            ],
                            "description": "DIAGRAM DESCRIPTION"
                        }
                    ],
                    "dependencies": [
                        {
                            "catalog_id": "ID",
                            "id": "ID",
                            "name": "PRODUCT PROGRAMMATIC NAME",
                            "kind": "FORMAT KIND",
                            "version": "VERSIONS OR RANGE OF VERSIONS",
                            "flavors": ["VARIATION NAME OR NAMES"]
                        }
                    ],
                    "release_notes_url": "RELEASE NOTES URL",
                    "configuration": [
                        {
                            "key": "KEY",
                            "type": "TYPE",
                            "default_value": "DEFAULT VALUE",
                            "display_name": "DISPLAY NAME",
                            "value_constraint": "CONSTRAINT",
                            "description": "DESCRIPTION",
                            "required": "REQUIRED",
                            "options": [
                                "OPTION"
                            ],
                            "hidden": "HIDDEN",
                            "custom_config":
                            {
                                "type": "TYPE",
                                "grouping": "GROUPING",
                                "original_grouping": "ORIGINAL GROUPING",
                                "grouping_index": "GROUPING INDEX",
                                "config_constraints": "CONFIG CONSTRAINTS",
                                "associations": "ASSOCIATIONS"
                            }
                        }
                    ],
                    "terraform_version": "TERRAFORM VERSION",
                    "outputs": [
                        {
                            "key": "KEY",
                            "description": "DESCRIPTION"
                        }
                    ],
                    "install_type": "INSTALL TYPE"
                }
            ]
        }
    ]
}

```
{: codeblock}

## Catalog manifest values
{: #manifest-values}

You can use the following values to build your catalog manifest file.

### products
{: #value-products}

The products value indicates an array of products with size one or more. If a catalog manifest file exists at the root of your repository, only the products within the file can be imported. Products are imported one at a time. The following values can be included at the `products` level:

label
:   The product display name. The label that is listed in the catalog manifest must match the display name that you provide during onboarding.

name
:   The programmatic name of the product.

version
:   The version of the product in SemVer format, including the major version, minor version, and revision, for example, 1.0.0.

product_kind
:   The kind of product that you are onboarding. Valid values are software, module, or solution.

tags
:   An array of tags that can help users identify and learn more about your product.

keywords
:   An array of works, phrases, and other key seaarch terms that can help users identify and learn more about your product.

short_description
:   A concise summary of what your product is and its value.

long_description
:   A detailed description of your product that explains the product's value and benefits to users.

provider_name
:   Users can filter the catalog by the provider of a product. When you onboard a product to a private catalog, the provider name is set to `Community` by default. However, you can customize this field to display your company or organization name.

offering_docs_url
:   A link to documentation about the product that users can access.

offering_icon_url
:   A link to the icon that you want to appear on the product's catalog entry page.

support_details
:   Support information in markdown format that can include support contacts, support locations, and support methods.

features
:   Section header for details that highlight the processes, abilities, and results of the product.

    title
    :   The name of the feature.

    description
    :   A concise description of the feature.

### module_info
{: #value-module}

The modules value indicates information about other products that the deployable architecture is compatible with. The following values can be included at the `module_info` level:

works_with
:   Section header for information about a singular product that is compatible with the deployable architecture.

    catalog_id (optional)
    :   ID of the catalog that houses the product. If not specified, the {{site.data.keyword.cloud_notm}} catalog is the default.

    id (optional)
    :   ID of the product. The ID is not required in the `name` value is set.

    name (optional)
    :   Programmatic name of the product that works with the deployable architecture.

    kind
    :   Format kind of the product that works with the deployable architecture.

    version
    :   Version or range of product versions that work with the deployable architecture in SemVer format.

    flavors (optional)
    :   The programmatic names of the compatible variations.

### flavors
{: #value-variations}

Section header for information about the deployable architecture variations. The following values can be included at the `flavors` level:

label
:   Variation display name.

name
:   Variation programmatic name.

working_directory
:   The path from the root of your repository to the variation. For example, `examples/basic`.

usage
:   Information on how to embed the architecture or run it locally.

licenses
:   Information about the end-user license agreements that users are required to accept when they install the product. The license agreements are in addition to the {{site.data.keyword.cloud_notm}} Services Agreement.

    name
    :   The license name.

    url
    :   A URL to where the user can access the license agreement.

compliance
:   Section header that indicates that the architecture is compliant.

    You can list multiple profiles in your catalog manifest JSON file, but note that only the first profile is added to your compliance information in a private catalog.
    {: important}

    authority
    :   The version of Security and Compliance Center that you are adding controls from.

    profiles
    :   Section header that indicates that the variation has claimed a profile. You can view predefined profiles in the {{site.data.keyword.compliance_full}}.

        profile_name
        :   The name of the claimed profile. For example, `NIST`. You can find the profile name in {{site.data.keyword.compliance_short}}.

        profile_version
        :   The version of the profile. For example, `1.0.0`. You can find the profile name in {{site.data.keyword.compliance_short}}.

    controls
    :   Section header that indicates that the variation has claimed controls. The catalog manifest accepts an array of controls that you can claim on your variation by specifying a control's `name`, profile `name`, and profile `version`. You can view predefined profiles in the {{site.data.keyword.compliance_full}}.

        profile
        :    Section header that indicates that you are adding controls from a specific profile.

            name
            :   The profile name of the claimed control. For example, `NIST`. You can find the profile name in {{site.data.keyword.compliance_short}}.

            version
            :   The version of the profile. For example, `1.0.0`. You can find the profile name in {{site.data.keyword.compliance_short}}.

        names
        :   Section header to indicate a list of claimed controls. For example:

        ```text
        "names": [
           "CM-7(b)",
           "AC-2(a)"
         ]
        ```

    If you have included controls in your readme and your catalog manifest file, the manifest file takes precedence. It is best practice to make sure the controls listed in your catalog manifest file match the controls in your readme file.
    {: note}

iam_permissions (optional)
:   Section header for a list of all IAM permissions that are required to deploy the variation. IAM permission information includes the programmatic name of the service that is required and a list of CRNs for roles that are needed. If you build your catalog manifest file from the UI, the CRNs are already included.

    service_name
    :   The programmatic name of the service that users must have access to.

    role_crns
    :   Section header to indicate a list of access roles. For example:

    ```text
    "role_crns": [
        "ROLE",
        "ROLE"
        ]
    ```
    {: codeblock}

    resources
    :   The resources for a permission.

        name
        :   The name of the resource.

        description
        :   A description of the resource.

        role_crns
        :   Section header to indicate a list of access roles. For example:

        ```text
        "role_crns": [
        "ROLE",
        "ROLE"
        ]
        ```
        {: codeblock}

architecture
:   Information about the variation's architecture that includes an architecture description, features, and an architecture diagram.

    features
    :   Details that highlight the processes, abilities, and results of the version, or if applicable, architecture variation. If your product has multiple architecture variations, users can compare highlights (features) to decide which variation suits their needs.

        title
        :   Name of the feature.

        description
        :   A description of the feature.

    diagrams
    :   Information about the architecture diagram that includes the diagram caption, the URL to embed the SVG of the diagram, the diagram metadata such as element ID and element description, and the description of the reference architecture.

        diagram
        :   Section marker for information about a singular architecture diagram.

            url
            :   The URL to the diagram's SVG.

            api_url
            :   The catalog management API URL to the diagram.

            url_proxy
            :   Section header for information about a proxied image.

                url
                :   The URL to the proxied image.

                sha
                :   The sha indientifier of the image.

            caption
            :   A short label for the architecture diagram.

            type
            :   The type of media.

            thumbnail_url
            :   A link to a thumbnail for the diagram.

        description
        :   Information about architecture diagram as a whole, including the outline of the system and the relationships, constraints, and boundaries between components of the deployable architecture.

dependencies
:   Section header for a list of prerequisite products that are required to deploy the architecture. Information includes the programmatic name of the product and product versions. Optionally, you can include the catalog ID and a list of dependent variations.

    catalog_id (optional)
    :   ID of the catalog that houses the product. If not specified, the {{site.data.keyword.cloud_notm}} catalog is the default.

    id (optional)
    :   The product ID. The ID is not required if the `name` value is set.

    name (optional)
    :   Programmatic name of the product.

    kind
    :   The format kind of the dependency.

    version
    :   A version or range of versions to include as dependencies in SemVer format.

    flavors (optional)
    :   List of variations that the architecture depends on.

release_notes_url
:   URL to the architecture's release notes.

configuration
:   Section header for configuration information, including configuration key, type, default values, display names, and descriptions. Most values are already set during the onboarding process, but you might need to override the values generated during onboarding, or set values that are not configured during the onboarding process.

    required
    :   Indicates if users are required to specify the parameter during installation.

    hidden
    :   Indicates if the parameter should be hidden from users during installation.

    options
    :   An array of options that users can choose from for a parameter.

    custom_config
    :   Section header use to indicate that a custom configuration can be used.

        type
        :   The ID of the widget type used for configuration

        grouping
        :   Where the configuration type should appear in the catalog. Valid values are `Target`, `Resource`, and `Deployment`.

        original_grouping
        :   Where the configuration type originally appeared. Valid values are `Target`, `Resource`, and `Deployment`.

        grouping_index
        :   The order of this configuration item when there are mulitple.

        config_constraints
        :   Map of constraint parameters that are given to the custom widget.

        associations
        :   Section header for parameters that are associated with the configuration.

            parameters
            :   List of parameters.

terraform_version
:   The Terraform version needed to validate and install the version. Setting this value overrides what is specified in the source code.

outputs
:   Section header for information about output values.

    key
    :   Specifies the output value.

    description
    :   A short summary of the output value.

install_type
:   Specifies whether a deployable architecture is full stack or extension. Architectures listed as extensions require prerequisites.
