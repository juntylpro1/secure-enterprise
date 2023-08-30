---

copyright:
  years:  2023
lastupdated: "2023-08-30"

keywords: change log for Projects, updates to Projects

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Projects API change log
{: #projects-api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [Projects API](/apidocs/projects). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## 06 July 2023
{: #06-jul-2023}

The response models for all methods now enforce a lower snake case format in `state` values. This format is to be expected in the response when you are calling the project and configuration endpoints. This update is a breaking change.
{: important}

Project `state` values can now be `ready`, `deleting`, and `deleting_failed`. For an example, see [the response schema for the `update-project` method](/apidocs/projects#update-project).

Configuration `state` values can now be `deleted`, `deleting`, `deleting_failed`, `installed`, `installed_failed`, `installing`, `not_installed`, `uninstalling`, `uninstalling_failed`, and `active`. For an example, see [the response schema for the `get-config` method](/apidocs/projects#get-config).
