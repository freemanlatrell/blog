---
title: 'An even better Operator Collection Development Experience'
slug: 'operator-collection-sdk-vs-code-extension-blog'
image: 'images/oc_sdk_vs_code_extension.png'
date: "2023-10-31T00:00:00"
disableComments: false
author: Latrell Freeman
authorTitle: Lead Architect - IBM z/OS Cloud Broker
---

In conjunction with the latest release of the IBM Z and Cloud Modernization stack, we're happy to announce the initial release of the IBM Operator Collection SDK VS Code extension, to continue to improve the Operator Collection development experience. In the previous release of the IBM Z and Cloud Modernization Stack, we also released the [IBM Operator Collection SDK][oc-sdk] Ansible collection, which provides a comprehensive toolkit designed to simplify the creation, and debugging of Operator Collections in OpenShift. Now, with the release of the [IBM Operator SDK VS Code extension][oc-sdk-vs-code], we are now integrating that toolkit in the VS Code editor, to further simplify the Operator Collection development experience, and provide better insight into your deployments and resources on OpenShift. Here are a few of the features that are available in the IBM Operator SDK VS Code extension to simplify and improve the Operator Collection development experience.


## Single-click Actions To Deploy Operator Collection to OpenShift

With this extension, users will now have the ability to execute each IBM Operator Collection SDK Ansible playbooks with a single click of an action in the primary side bar in the VS Code editor. These actions consist of creating an operator once you're ready to validate your changes in OpenShift, redeploying the operator to quickly apply modifications in OpenShift, and deleting the operator once your testing is complete.  

![Deploy and manage operator](/static/images/oc-sdk-actions.png)


## Monitor OpenShift Resources

Once your operator is deployed in OpenShift, you can now monitor your OpenShift resources within the primary side bar in the VS Code editor. 

Below are some of the resources that are viewable in the primary side bar:

- **Operator Pods and Containers:** Monitor the status of operator containers in OpenShift, while also providing the ability to view container logs in the editor. 
- **z/OS Cloud Broker Custom Resources:** Monitor the status of the z/OS Cloud Broker custom resources such as `ZosEndpoints`, `OperatorCollections`, and `SubOperatorConfigs`, which are used to generate the operator.
- **Operator Custom Resources:** Create and monitor your operator custom resources in OpenShift, while also having the ability to view the ansible-runner execution logs generated during each reconciliation.

## Manage OpenShift Connectivity

Quickly log in and update your OpenShift Project directly from the VS Code editor, removing the need to context switch between the terminal and the VS Code editor to manage OpenShift access.

## Operator Collection Linting

Once the extension is installed, and an Operator Collection is detected in the workspace, the linter is automatically enabled to provide assistance during Operator Collection development. The Operator Collectin linter provides instant validation and code completion against the `operator-config.yml` file using the latest Operator Collection Specification, and also the ability to hover and display descriptions of each avaialble property in the configuration.

## Getting Started

The IBM Operator Collection SDK VS Code extension is available for free in the VS Code Marketplace, which is also accessible directly in your VS Code editor.

Developing an Operator Collection in OpenShift requires the installation of the IBM z/OS Cloud Broker, and optionally the IBM Wazi Sandbox. You can now access a free 60-day trial of the IBM Z and Cloud Modernization Stack, which includes these products. We invite you to [try it out][trial-link]!

## Learn More
To learn more about Operator Collections and why they can be a useful enhancement to your existing Ansible automation, please check out my previous blog [here](../operator-collection-blog).

[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[oc-sdk-vs-code]:https://marketplace.visualstudio.com/items?itemName=IBM.operator-collection-sdk
[trial-link]:https://www.ibm.com/account/reg/us-en/signup?formid=urx-51680
