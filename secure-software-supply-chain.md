---

copyright:
  years: 2023, 2024
lastupdated: "2024-06-04"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Using DevSecOps to build a secure software supply chain
{: #secure-software-supply-chain}

With the [DevSecOps](#x9892260){: term} tools and services available through {{site.data.keyword.cloud}}, you can take advantage of using a verified secure software supply chain for developing and deploying your application code. Your agile development practices require rapid application deployment, but at the same time, you need to ensure that your applications are secure. Learn more about the background of [agile, DevOps, and DevSecOps](/docs/devsecops?topic=devsecops-devsecops_intro#devsecops-background).
{: shortdesc}

You can use the [DevSecOps Application Lifecycle Management](/docs/devsecops-alm?topic=devsecops-alm-devsecops-alm-overview) deployable architecture, which is a solution available from the {{site.data.keyword.cloud_notm}} catalog that uses {{site.data.keyword.contdelivery_short}} and others tools to help you automate the integration of security at every phase of the application software development lifecycle, from development through integration, testing, deployment, and software delivery. Evidence is also collected so that you can easily demonstrate to auditors that necessary controls are being met. By using DevSecOps Application Lifecycle Management, you can implement a shift-left approach by preventing new vulnerabilities from reaching production, ensuring frequent updates to production with quality and control, and collecting evidence for handling security audits.

DevSecOps Application Lifecycle Management uses {{site.data.keyword.contdelivery_short}} ({{site.data.keyword.gitrepos}}, Tekton Pipelines, {{site.data.keyword.DRA_short}}, and Code Risk Analyzer), Secrets Manager, Key Protect, {{site.data.keyword.cos_short}}, Container Registry, and Vulnerability Advisor. Aligned with the requirements of the Financial Services industry, {{site.data.keyword.contdelivery_short}} provides a reference implementation of [NIST Configuration Management](https://csrc.nist.gov/projects/cprt/catalog#/cprt/framework/version/SP_800_53_5_1_1/home){: external} controls as a service.

Out of the box, DevSecOps with {{site.data.keyword.contdelivery_short}} also uses scanning tools such as SonarQube, Gosec, OWASP Zap (dynamic scan), any unit test framework, and GPG signing. It can also be used with more tools such as external Git providers and artifact stores. DevSecOps supports hybrid deployments, in particular by using [pipeline private workers](/docs/ContinuousDelivery?topic=ContinuousDelivery-private-workers), and can be interfaced with other deployment tools such as Satellite Config and ArgoCD. For more information, see [DevSecOps with {{site.data.keyword.contdelivery_short}}](/docs/devsecops?topic=devsecops-devsecops_intro).

You can configure this deployable architecture from the catalog by adding it to a [project](#x2035151){: term}, configuring the input variables, validating your updates, and deploying it in just a short time. Learn about how you can [Deploy DevSecOps Application Lifecycle Management with projects](/docs/devsecops-alm?topic=devsecops-alm-devsecops-alm-proj).
