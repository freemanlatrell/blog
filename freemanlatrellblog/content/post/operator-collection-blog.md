+++
title = 'Modernizing and Innovating on Z just got a lot easier!'
slug = 'operator-collection-blog'
image = 'images/red_cloud_image.jpg'
date = "2023-06-17T00:00:00"
description = 'We are pleased to announce that modernizing applications and automation on z/OS has become significantly easier with the latest release of the IBM Z and Cloud Modernization Stack.'
disableComments = false
+++


In the previous release, we introduced valuable solutions, such as the IBM z/OS Package Manager, enabling effortless installation and management of z/OS native software on your target z/OS host. Additionally, we provided the IBM IMS Operator, empowering you to provision and manage your IMS subsystem from OpenShift. Building upon these services, we now offer even more capabilities in the latest release.

We have taken a step forward by publishing the [Operator Collection Specification][oc-spec]. This enables z/OS developers to create their own Operator Collections in OpenShift, expanding the possibilities of our platform. To facilitate the development process, we are offering the [IBM Operator Collection SDK][oc-sdk], a comprehensive toolkit designed to simplify the creation of Operator Collections.

Moreover, we have revamped the IBM z/OS Cloud Broker operator catalog to encourage the sharing of Operator Collections. By leveraging the IBM z/OS Cloud Broker Galaxy Operator Catalog, you can effortlessly expose your Ansible automation in the OpenShift Container Platform. It can be consumed in the same manner as other cloud-native services. Additionally, you can explore other open z/OS solutions in the Operator Collection community, expanding your options for building z/OS applications running on OpenShift.


## **So, what are Operator Collections?**

Operator Collections combine Ansible Collections with an operator configuration file, enabling their consumption by the IBM z/OS Cloud Broker and transforming them into Ansible Operators that run on OpenShift.

Creating automation as Ansible Collections offers a convenient method for packaging and sharing automation with fellow Ansible developers. Once these collections are published on platforms such as Ansible Galaxy or Ansible Automation Platform, they become consumable as dependencies within other collections. They can be downloaded for execution on your local machine or directly utilized in the Ansible Automation Platform. However, if you desire to elevate your Ansible automation to match the self-service experience offered by cloud services, Operator Collections present an invaluable option. Considering Operator Collections can greatly enhance your application modernization journey.


## **Why would I want to execute my Ansible automation in OpenShift?**

Executing your z/OS Ansible solutions in OpenShift offers numerous advantages. Here are my top three reasons:

### **1. Ensuring a consistent cloud experience for your Ansible solutions**

By providing a consistent cloud experience for both z/OS and non-z/OS services, developers can build applications on OpenShift in a unified manner. Imagine building a web application on OpenShift that requires a secure HTTP connection, a backend database, and user management with single sign-on. By offering Operator Collections like RACF certificate management and DB2 for z/OS within the OpenShift catalog, developers can seamlessly self-provision these operators to secure their application and manage the backend database. Additionally, by installing the Red Hat Single Sign-On Operator, developers can incorporate user management and single sign-on functionality. With Operator Collections available in OpenShift, developers can effortlessly access z/OS resources in the cloud, enabling them to build comprehensive applications with a consistent cloud experience for all required services.

### **2. Extending your Ansible solutions with custom Kubernetes APIs**

OpenShift, known as a "Container Platform" powered by Kubernetes, offers more than just container orchestration. It allows you to extend the Kubernetes API with custom APIs of your own. These custom APIs enable you to perform CRUD actions on your OpenShift operator using REST requests against the OpenShift cluster. Let's illustrate this with an example.

When building your Operator Collection using the [Operator Collection Specification][oc-spec], you're essentially defining the API structure for the new object in OpenShift. Consider the RACF operator configuration shown in the video below. This Operator Collection generates an operator that facilitates self-service creation and deletion of a user ID on a z/OS host.

Under the `resources` section, a new object called `ZosUserID` (referred to as a `Kind` in Kubernetes) is created in OpenShift. The `playbook` field specifies which playbooks to execute when an instance is created (or a POST request is sent to the API server). The `finalizer` specifies which playbooks to execute when an instance is deleted (or a DELETE request is sent to the API server). This object requires specific fields (`name` and `userid`) in the API request for executing the Operator Collection. Once deployed to OpenShift, a new object named `ZosUserID` is available in the cluster, and you can use REST requests (via the `oc` CLI or an API tool) to execute this collection in OpenShift.

https://github.com/IBM/operator-collection-sdk/blob/5c3ab6e59a86d7ce363f46f7d675668fc735ac08/examples/racf-operator/operator-config.yml#L1-L39

Additionally, you can store the `.yml` files containing user IDs in a source-controlled management system like Git. By incorporating a CI/CD pipeline for your repository, you can execute these APIs and quickly redeploy user IDs on newly provisioned z/OS hosts. For instance, adding a new user in a production environment becomes a pull request in GitHub that includes a new `.yml` file in the repository. The available operator in OpenShift enables self-service ID creation for developers who need a new ID in a development Wazi Sandbox environment. This brings me to the third advantage which is...


### **3. Enabling self-service consumption of your Ansible solutions**

Enabling self-service solutions gives users instant access to automation, tools, and applications that previously required administrator involvement for deployment. Admins can publish their Ansible automation as Operator Collections in the OpenShift catalog, empowering users to consume these resources at their convenience. This significantly reduces administrative burden while improving speed and efficiency for end users.

Consider the example of the RACF Operator Collection mentioned earlier. Even developers with minimal knowledge of RACF user ID configuration can now deploy and test their z/OS applications in a sandbox environment by installing a Wazi Sandbox instance. They can leverage the RACF Operator Collection to generate user IDs in this sandbox without requiring guidance or intervention from an administrator.

Take a moment to contemplate the mundane tasks currently handled by admins in your organization, the time spent managing user requests, and how implementing self-service capabilities can drastically reduce the response time. Additionally, think about developers deploying a Wazi Sandbox environment with limited z/OS skills but needing a configuration similar to the production environment. By creating Ansible playbooks for each task and converting them into Operator Collections in OpenShift, you empower your developers with the necessary resources for configuration, eliminating the need for assistance from a z/OS admin.


## **Ok, I'm convinced and ready to get started!**

Alongside the latest release of the IBM Z and Cloud Modernization Stack, we are excited to offer the [IBM Operator Collection SDK][oc-sdk], a free open-source tool that streamlines the development process for creating Operator Collections. This SDK provides the following features:
- **Scaffold generation:** The SDK enables scaffolding a new operator collection with a preconfigured set of requirements. It also incorporates the necessary operator-config.yml file into existing Ansible collections, enabling their conversion to operator collections supported by the z/OS Cloud Broker.
- **Efficient debugging:** The SDK enables rapid deployment and debugging of your Ansible automation in an operator in OpenShift by using a local build of your latest Ansible modifications.

To assist you further, the repository includes the comprehensive [RACF operator tutorial][oc-sdk-tutorial], guiding you through the creation of your first Operator Collection. You will also find the Operator Collection development guide, offering best practices for developing Operator Collections.

Developing an Operator Collection in OpenShift requires the installation of the IBM z/OS Cloud Broker and optionally the IBM Wazi Sandbox. You can now access a free 60-day trial of the IBM Z and Cloud Modernization Stack, which includes these products. We invite you to [try it out][trial-link]!

Now that you have the tools to unlock the limitless potential of Operator Collections, we encourage you to share your non-proprietary solutions on Ansible Galaxy. By doing so, you make them available to the community through the z/OS Cloud Broker Galaxy Operator Catalog.

Let's embark on an exciting journey of innovation and modernization for z/OS together. Together, we can leverage open-source solutions to propel the z/OS platform forward like never before!


[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[oc-sdk-tutorial]:https://github.com/IBM/operator-collection-sdk/blob/main/docs/tutorial.md
[oc-spec]:https://github.com/IBM/operator-collection-sdk/blob/main/docs/spec.md
[example-operator]:https://github.com/IBM/operator-collection-sdk/tree/main/examples/racf-operator
[trial-link]:https://www.ibm.com/account/reg/us-en/signup?formid=urx-51680
