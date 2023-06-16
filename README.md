# **Modernizing and Innovating on Z just got a lot easier!**

Modernizing applications and automation on z/OS just got a lot easier with the latest release of the IBM Z and Cloud Modernization Stack! 


In the previous release of the IBM Z and Cloud Modernization Stack, we provided solutions such as the IBM z/OS Package Manager that allows you to easily install and manage z/OS native software on a target z/OS host, and the IBM IMS Operator that allows you the ability to provision and manage your IMS subsystem from OpenShift. Along with the additional features we’ve added to those services in the latest release, we’ve decided to take things a step further and open up our platform, by publishing our [Operator Collection Specification][oc-spec], allowing z/OS developers the ability to develop their own Operator Collections in OpenShift! We're also providing the [IBM Operator Collection SDK][oc-sdk], which delivers all of the tools you need to make the Operator Collection development experience as simple as possible.

In addition, we’ve also redesigned our IBM z/OS Cloud Broker operator catalog to promote the sharing of these Operator Collections in our IBM z/OS Cloud Broker Galaxy Operator Catalog. So now you can easily expose your Ansible automation in the OpenShift Container Platform, to be consumed in the same fashion as other cloud native services, while also discovering other open z/OS solutions in the Operator Collection community, that can also be leveraged to build z/OS applications running on OpenShift. 

## **So, what are Operator Collections?**

Operator Collections are simply Ansible Collections bundled with an additional operator configuration file, consumed by the IBM z/OS Cloud Broker, and converted into an Ansible Operator running in OpenShift. 

Generating automation as Ansible Collections is a great way to package and distribute automation to other Ansible developers. Once these collections are published to platforms like Ansible Galaxy, or Ansible Automation Platform, these collections can now be consumed within other collections as dependencies, downloaded for execution on your laptop, or executed directly in the Ansible Automation Platform. But what if you want to take your Ansible automation a step further and provide the same self-service experience as any other cloud service? This is just one of the many reasons why you should consider Operator Collections as an additional avenue during your application modernization mission.


## **Why would I want to execute my Ansible automation in OpenShift?**

Running your z/OS Ansible solutions on OpenShift has tons of advantages, and I’ll provide my top 3 reasons below:


### **1. Provides a consistent cloud experience for your Ansible solutions.**

Having the ability to provide a consistent cloud experience for both z/OS and non-z/OS services, provides developers the ability to build applications on OpenShift in a unified way. Take for example a developer attempting to build a web application running on OpenShift, that contains a secure HTTP connection, a backend database, and the ability to perform user management to grant access to the application using single sign-on. To enable this developer to secure their application, you’ve decided to provide a RACF certificate management Operator Collection on OpenShift. For the backend database, you’ve decided to provide a DB2 Operator Collection on OpenShift, that provisions and manages DB2 on z/OS. With these Operator Collections now available to the developer as operators in the OpenShift catalog, the developer can now self-provision the RACF certificate management operator to secure their application, and the DB2 operator for their backend database. As for the user management and single-sign on service, the developer can also install the Red Hat Single Sign-On Operator provided by Red Hat and running on OpenShift. With these Operator Collections available in OpenShift, developers can now have the same access to z/OS resources in the cloud, as they do with non-z/OS resources, allowing them the ability to build an entire application on OpenShift, with a consistent cloud experience for all their required services. 

### **2. Extend your solutions with custom Kubernetes API’s.**

Although OpenShift is considered a “Container Platform” powered by Kubernetes, orchestrating containers isn’t the only benefit to running on OpenShift. The other benefit is the ability to extend the Kubernetes API with your own custom API’s, allowing CRUD actions to be performed against your OpenShift operator, using REST requests against the OpenShift cluster. Let’s walk through an example to further explain…

When you’re building your Operator Collection using the [Operator Collection Specification][oc-spec], you’re actually building out the body for the API of the new object to be created in OpenShift. Take for example the RACF operator configuration in the video below. In this Operator Collection, we are generating an operator that allows for the self-service creation and deletion of a user ID on a z/OS host. 


Under the `resources` section, we are creating a new object (in Kubernetes this is called a `Kind`) in OpenShift called `ZosUserID`. In the `playbook` field we are telling OpenShift which playbooks to execute when an instance is created (or a POST request is sent to the API server), and the `finalizer` field is telling OpenShift which playbook to execute when the instance is deleted (or a DELETE request is sent to the API server). For this object we’d like to require that the following fields are passed in the API request to execute the Operator Collection. In this example those fields are `name` and `userid`. Once this Operator Collection is deployed to OpenShift, a new object is now available in the cluster called `ZosUserID`, which we can now perform REST requests (via the `oc` CLI or an API tool of your choice) to execute this collection in OpenShift.

<video src=https://github.com/freemanlatrell/blog/assets/24191850/4f9693ce-d901-47ba-8883-6fcd353b3d8e controls="controls" style="max-width: 730px;">
</video>

Taking this a step further, we can also store these `.yml` files for our user IDs in a source-controlled management system like Git. Then we can build a CI/CD pipeline around our repository that executes these API’s, to quickly redeploy these user IDs on newly provisioned z/OS hosts. Adding a new user in a production environment can now be managed via a Pull Request in GitHub, that adds a new `.yml` file to the repository, while the available operator in OpenShift also allows for the self-service ID creation for developers needing a new ID created on a development Wazi Sandbox environment. Which takes me to my third and final advantage which is…

### **3. Provides self-service consumption of your Ansible solution.**

Having the ability to provide solutions as a self-service, provides users with instant access to automation, tools, and applications that would’ve previously required requests to an administrator to handle these deployments for the user. Admins can now publish their Ansible automation in the OpenShift catalog as Operator Collections, and allow users the ability to consume this automation at their own leisure. This tremendously reduces the administrative burden, while also improving the speed and efficiency for the end user.  

Take the example above with our RACF Operator Collection. Developers which little to no knowledge of RACF user ID configuration, can now install a Wazi Sandbox instance to deploy and test their z/OS application in a sandbox environment, while also leveraging the RACF Operator Collection to generate user ID’s on this sandbox. This is all without any intervention or request to an administrator to provide guidance on how to perform this configuration.

Take a moment to consider all of the mundane tasks currently being executed by admins in your organization, the time that it takes to manage these requests for each user, and how having the ability to have this process managed as a self-service could greatly reduce the time that it takes to handle these requests. Also consider the developer who’s deploying a Wazi Sandbox environment with limited z/OS skills, but would like the ability to quickly configure this environment to have a similar configuration as the production environment. By simply creating an Ansible Playbook for each task, and converting this to an Operator Collection in OpenShift, you can now enable your developers with the resources they need to perform this configuration without any assistance from a z/OS admin.



## **Ok, I’m convinced and ready to get started!**

As mentioned above, along with the latest release of the IBM Z and Cloud Modernization Stack, we’ve also made available a free open-source tool called the [IBM Operator Collection SDK][oc-sdk], to simplify the development process for creating Operator Collections by providing the following features:
- **Scaffold generation:** The SDK enables scaffolding a new operator collection with a preconfigured set of requirements. It also incorporates the necessary operator-config.yml file into existing Ansible collections, enabling their conversion to operator collections supported by the z/OS Cloud Broker.
- **Efficient debugging:** The SDK enables rapid deployment and debugging of your Ansible automation in an operator in OpenShift by using a local build of your latest Ansible modifications.

In this repository, you will also have access to the [RACF operator tutorial][oc-sdk-tutorial] to guide you through the process of creating your first Operator Collection, and the Operator Collection development guide for best practices when developing Operator Collections.

Developing an Operator Collection in OpenShift also requires the installation of the IBM z/OS Cloud Broker, and optionally the IBM Wazi Sandbox. These products are now available in a free 60 day trial of the IBM Z and Cloud Modernization Stack which we invite you to try here. (ADD TRIAL LINK HERE)

Now that you’re equipped to take advantage of the endless possibilities of Operator Collections, I’d like you to also consider publishing non-proprietary solutions to Ansible Galaxy, to become available to the community in the z/OS Cloud Broker Galaxy Operator Catalog. 

Let’s innovate and modernize z/OS together, with open-source solutions that can help grow the z/OS platform faster than ever before!


[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[oc-sdk-tutorial]:https://github.com/IBM/operator-collection-sdk/blob/main/docs/tutorial.md
[oc-spec]:https://github.com/IBM/operator-collection-sdk/blob/main/docs/spec.md
[example-operator]:https://github.com/IBM/operator-collection-sdk/tree/main/examples/racf-operator
