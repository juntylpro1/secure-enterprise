---

copyright:
  years: 2023
lastupdated: "2023-04-17"

keywords:

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Using DevSecOps to build a secure software supply chain
{: #secure-software-supply-chain}

With the [DevSecOps](#x9892260){: term} tools and services available through {{site.data.keyword.cloud}}, you can take advantage of using a verified secure software supply chain for developing and deploying your application code. Your agile development practices require rapid application deployment, but at the same time, you need to ensure that your applications are secure.
{: shortdesc}

DevSecOps requires automating security and compliance controls as part of continuous integration and continuous delivery processes. Evidence is also collected so you can easily demonstrate to auditors that necessary controls are being met. By using [DevSecOps with {{site.data.keyword.contdelivery_short}}](/docs/devsecops?topic=devsecops-devsecops_intro), you can implement a shift-left approach by preventing new vulnerabilities from reaching production, ensure frequent updates to production with quality and control, and collect evidence for handling security audits.\

Learn more about the background of [agile, DevOps, and DevSecOps](/docs/devsecops?topic=devsecops-devsecops_intro#devsecops-background).

## Exploring DevSecOps with {{site.data.keyword.contdelivery_short}}
{: #learn-devsecops}

DevSecOps uses {{site.data.keyword.contdelivery_short}} ({{site.data.keyword.gitrepos}}, Tekton Pipelines, {{site.data.keyword.DRA_short}}, and Code Risk Analyzer), Secrets Manager, Key Protect, {{site.data.keyword.cos_short}}, Container Registry, and Vulnerability Advisor. Aligned with the requirements of the Financial Services industry, {{site.data.keyword.contdelivery_short}} provides a reference implementation of [NIST Configuration Management](https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/release-search#!/controls?version=5.1&family=CM){: external} controls as a service.

Out of the box, DevSecOps with {{site.data.keyword.contdelivery_short}} also uses scanning tools such as SonarQube, Gosec, OWASP Zap (dynamic scan), any unit test framework, and GPG signing. It can also be used with more tools such as external Git providers and artifact stores. DevSecOps supports hybrid deployments, in particular by using [pipeline private workers](/docs/ContinuousDelivery?topic=ContinuousDelivery-private-workers), and can be interfaced with other deployment tools such as Satellite Config and ArgoCD.

Learn how you can [Deploy a secure app with DevSecOps](/docs/devsecops?topic=devsecops-tutorial-cd-devsecops).
