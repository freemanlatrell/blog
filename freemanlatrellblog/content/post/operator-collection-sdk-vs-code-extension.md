---
title: 'Enhance Your Operator Collection Development Experience with the IBM Operator Collection SDK VS Code Extension'
slug: 'operator-collection-sdk-vs-code-extension-blog'
image: 'images/oc-sdk-vs-code-extension-laptop.png'
date: "2023-11-03T00:00:00"
disableComments: false
author: Latrell Freeman
authorTitle: Lead Architect - IBM z/OS Cloud Broker
---

We are excited to announce the initial release of the [IBM Operator SDK VS Code extension][oc-sdk-vs-code], coinciding with the latest release of the IBM Z and Cloud Modernization stack. As part of the previous release, we introduced the [IBM Operator Collection SDK][oc-sdk], a powerful toolkit designed to streamline the creation and debugging of Operator Collections in OpenShift. Expanding on this foundation, our new IBM Operator SDK VS Code extension seamlessly integrates this toolkit into the VS Code editor, revolutionizing the Operator Collection development process and providing invaluable insights into your deployments and resources on OpenShift. 

Now, let's delve into the key features of the IBM Operator SDK VS Code extension that significantly simplify and enhance the Operator Collection development experience.

## Empower Your Workflow with One-Click Playbook Execution

The IBM Operator SDK VS Code extension brings a new level of efficiency to your development process. With this extension, you can effortlessly execute each IBM Operator Collection SDK Ansible playbook with a single click in the primary sidebar of the VS Code editor.

Take advantage of the following actions directly from the primary sidebar:

- **Create Operator**: Validate your changes in OpenShift by easily creating an operator with a single click. This action ensures that your modifications are accurately reflected in the environment.

- **Redeploy Operator**: Apply modifications swiftly by redeploying the operator. When you make updates to your Operator Collection, this action allows you to see the changes take effect in OpenShift without any hassle.

- **Delete Operator**: Once testing is complete, you can seamlessly remove the operator from OpenShift with a single click. This action helps you maintain a clean and organized environment.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/oc-sdk-vs-code-actions.mov">
</video>

{{< /rawhtml >}}

By simplifying the execution of the IBM Operator Collection SDK Ansible playbooks, the IBM Operator SDK VS Code extension empowers you to focus on your development tasks with greater ease and efficiency. Say goodbye to manual executing ansible-playbook commands, and embrace a seamless workflow within your VS Code editor.


## Effortlessly Monitor Your OpenShift Resources

Once your operator is deployed in OpenShift, the IBM Operator SDK VS Code extension provides seamless monitoring capabilities directly within the primary sidebar of your VS Code editor. Keep a close eye on your OpenShift resources and gain valuable insights without the need for switching between your editor and the OpenShift console.

Here are some of the key resources that you can conveniently monitor within the primary sidebar:

- **Operator Pods and Containers:** Keep track of the status of operator containers in OpenShift, and conveniently view container logs directly in the editor.

- **z/OS Cloud Broker Custom Resources:** Monitor the status of the z/OS Cloud Broker custom resources such as `ZosEndpoints`, `OperatorCollections`, and `SubOperatorConfigs`, which are essential for generating the operator.

- **Operator Custom Resources:** Create and monitor your operator custom resources in OpenShift, and easily view the ansible-runner execution logs generated during each reconciliation.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/oc-sdk-vs-code-monitoring.mov">
</video>

{{< /rawhtml >}}

With the IBM Operator SDK VS Code extension, monitoring your OpenShift resources becomes a breeze. Stay in control of your deployments, troubleshoot issues promptly, and optimize your operator collections with ease - all from within your VS Code editor.

## Streamline OpenShift Connectivity Management with Ease

Managing your OpenShift project's connectivity is now more efficient than ever with the IBM Operator SDK VS Code extension. Our extension empowers you to seamlessly log in to and update your OpenShift project directly from the editor, eliminating the disruptions caused by constant context switching between the terminal and the VS Code editor.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/oc-sdk-vs-code-ocp.mov">
</video>

{{< /rawhtml >}}

## Elevate Your Operator Collection Development with the Built-in Linter

Upon installing the IBM Operator SDK VS Code extension and detecting an Operator Collection in your workspace, the linter becomes automatically enabled, offering invaluable support throughout your development process. The Operator Collection linter provides instant validation and code completion against the `operator-config.yml` file, utilizing the most up-to-date Operator Collection specification. Additionally, you have the ability to hover over properties in the configuration to access comprehensive descriptions, providing the details needed to avoid misconfigurations in your operator config file.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/oc-sdk-vs-code-linter.mov">
</video>

{{< /rawhtml >}}

## Getting Started

The IBM Operator Collection SDK VS Code extension is readily available for free in the [VS Code Marketplace][oc-sdk-vs-code], conveniently accessible right from your VS Code editor. Designed to simplify and streamline the Operator Collection development process, this extension is a game-changer. Start your journey towards efficient and robust OpenShift deployments by downloading the extension today. Experience the power firsthand and unlock new levels of productivity.

To jumpstart your Operator Collection development in OpenShift, simply install the IBM z/OS Cloud Broker and optionally the IBM Wazi Sandbox. As part of our support to your journey, we invite you to explore a complimentary 60-day trial of the IBM Z and Cloud Modernization Stack, encompassing these essential products. Take advantage of this opportunity and [give it a try][trial-link] today!

## Learn More

For further insights on harnessing the potential of Operator Collections to amplify your existing Ansible automation, I encourage you to explore my [previous blog post](../operator-collection-blog) dedicated to this topic.

[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[oc-sdk-vs-code]:https://marketplace.visualstudio.com/items?itemName=IBM.operator-collection-sdk
[trial-link]:https://www.ibm.com/account/reg/us-en/signup?formid=urx-51680
