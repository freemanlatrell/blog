---
title: 'Harnessing the Potential of IBM Operator Collection SDK and Ansible Lightspeed with IBM Watson Code Assistant'
slug: 'building-an-operator-collection-with-ansible-lightspeed'
image: 'images/light-speed.jpg'
imageDescription: Photo by Joshua Sortino on Unsplash
date: "2023-07-11T00:00:00"
disableComments: false
author: Latrell Freeman
authorTitle: Lead Architect - IBM z/OS Cloud Broker
---

The development process of [Operator Collections][oc-blog] has been simplified with the release of the [IBM Operator Collection SDK][oc-sdk]. This groundbreaking SDK provides developers with a comprehensive set of tools for deploying and debugging Ansible content in OpenShift. But that's not all - the recent [Tech Preview release of Ansible Lightspeed with IBM Watson Code Assistant][light-speed] takes the development process to the next level by leveraging generative AI.

Ansible Lightspeed with IBM Watson Code Assistant is a powerful generative AI tool designed to facilitate the efficient and rapid development of high-quality Ansible code. It seamlessly integrates with the Ansible VS Code extension in your VS Code editor, ensuring a smooth and intuitive experience. The underlying model, trained on open-source data, offers valuable task recommendations based solely on the entered task name.

In this blog post, we will take you through a step-by-step guide on how to initialize an Operator Collection using the IBM Operator Collection SDK, create playbooks using Ansible Lightspeed with IBM Watson Code Assistant, and deploy the Operator Collection to OpenShift for validation using the IBM Operator Collection SDK. With these tools at your disposal, you'll be able to streamline your development process and enhance your productivity.

Join us as we explore the exciting world of Operator Collection development and discover how the IBM Operator Collection SDK and Ansible Lightspeed with IBM Watson Code Assistant can revolutionize your workflow. Let's dive in!

## Step 1: Install the IBM z/OS Cloud Broker Operator
In order to create an Operator Collection and successfully deploy it in OpenShift, the first step is to install the [IBM z/OS Cloud Broker][broker] operator. This can be achieved by finding the IBM z/OS Cloud Broker operator from the OperatorHub catalog, installing it into our designated namespace, and then proceeding to create a `ZosCloudBroker` instance.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_1.mp4">
</video>

{{< /rawhtml >}}

## Step 2: Initialize the Operator Collection
In our journey to create an Operator Collection, we will utilize the IBM Operator Collection SDK. By leveraging this SDK, we can easily initialize our Operator Collection and generate a scaffold that includes all the necessary requirements to be consumed by the IBM z/OS Cloud Broker. To kickstart the initialization process, we need to provide the name of our Ansible Collection and specify the Ansible Galaxy namespace for this collection.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_2.mp4">
</video>

{{< /rawhtml >}}

## Step 3: Generate playbook tasks using Ansible Lightspeed with IBM Watson Code Assistant
Having successfully initialized our Operator Collection, we can now tap into the power of Ansible Lightspeed with IBM Watson Code Assistant to effortlessly generate tasks in our playbooks. It all begins by specifying a task name that outlines the desired action, allowing Ansible Lightspeed with IBM Watson Code Assistant to provide expert recommendations on how to accomplish the task.

In this demonstration, we'll kick off with a playbook named `create_file.yml`. This playbook is designed to create a new directory on our host, and touch a new file in the directory that was previously created. As we enter each task name, Ansible Lightspeed with IBM Watson Code Assistant promptly suggest a recommended approach to fulfill the task. By simply pressing the `tab` key, we can readily accept these recommendations.

While following along in the video, you'll notice that for the second task, I accepted the recommendation but also made a modification to utilize a variable called `filename` instead of the suggested filename from Ansible Lightspeed with IBM Watson Code Assistant. It's worth noting that the accepted tasks and any additional modifications are valuable in training the models used within Ansible Lightspeed with IBM Watson Code Assistant. This ongoing feedback loop enables the tool to enhance and refine the recommendations over time.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_3.1.mp4">
</video>

{{< /rawhtml >}}

Additionally, we'll create the `delete_file.yml` playbook to delete the previously created file when the instance is deleted in OpenShift.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_3.2.mp4">
</video>

{{< /rawhtml >}}

## Step 4: Update the operator-config.yml file
Once we have configured our playbooks, it is essential to provide the necessary values in our `operator-config.yml` file. This file serves as a central place to define crucial details about our operator, including its name, description, and the icon to be displayed in OpenShift. Moreover, it allows us to extend the Kubernetes API with our own custom API called `File`, by specifying a [custom resource][custom-resource] name. Additionally, we can specify the playbooks that should be executed when a user creates or deletes an instance of our new `File` API. We can also define variables that will be accessible to the user in OpenShift, enabling them to supply values to our playbook. For this demostration, we will only require a single variable named `filename`.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_4.mp4">
</video>

{{< /rawhtml >}}

## Step 5: Create the Operator using the IBM Operator Collection SDK
With our playbooks in place and the `operator-config.yml` file properly configured, it's time to proceed with the validation of our Operator Collection in OpenShift. Thankfully, we can simplify the entire manual process of packaging the collection, uploading it to the IBM z/OS Cloud Broker, and configuring the operator and host via the IBM z/OS Cloud Broker UI. Instead, we can effortlessly execute the `create_operator.yml` playbook, conveniently provided by the IBM Operator Collection SDK, by utilizing the `ocsdk-create-operator` [alias][alias-commands] on the command line.

During this step, we'll be prompted to enter the desired name, host, and port for the endpoint we'd like our operator to execute against. Additionally, we'll need to provide our SSH credentials for establishing a connection to the designated host. By executing the playbook, the IBM Operator Collection SDK takes care of generating all the necessary resources to deploy our operator in OpenShift. Soon after, our operator will be installed within our designated namespace.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_5.mp4">
</video>

{{< /rawhtml >}}

## Step 6: Create a File instance in OpenShift
To validate the functionality of our `create_file.yml` playbook, we should create an instance of the new `File` custom resource. This involves specifying the `filename` to create, and the host against which the file will be created.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_6.1.mp4">
</video>

{{< /rawhtml >}}

Once the instance is successfully created, we can SSH into the host to verify the presence of the new file.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_6.2.mp4">
</video>

{{< /rawhtml >}}

## Step 7: Delete the File instance in OpenShift
To confirm the proper functioning of our `delete_file.yml` playbook, we should delete the `File` instance created in OpenShift. This action will trigger the `delete_file.yml` playbook before removing the custom resource instance from OpenShift.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_7.mp4">
</video>

{{< /rawhtml >}}

## Wrapping Up
In this comprehensive blog post, we delved into the remarkable potential of combining Ansible Lightspeed with IBM Watson Code Assistant, along with the IBM Operator Collection SDK. These cutting-edge tools empower developers to swiftly create, test, and deploy Ansible content as operators in OpenShift. To begin leveraging these incredible resources, take advantage of the following free offerings:

- Experience the power of the IBM Z and Cloud Modernization Stack with a complimentary 60-day trial: https://www.ibm.com/account/reg/us-en/signup?formid=urx-51680
- Access the Tech Preview release of Ansible Lightspeed with IBM Watson Code Assistant: https://www.ansible.com/blog/welcome-to-the-ansible-lightspeed-technical-preview?sc_cid=701f2000000txokAAA&utm_source=bambu&utm_medium=organic_social&blaid=4724585
- Find the source code for this tutorial: https://github.com/freemanlatrell/file-manager-operator-collection/tree/ansible-lightspeed/freemanlatrell/file_manager

Prepare to be amazed! The immense potential of generative AI, in conjunction with the robust tools available in the IBM Z and Cloud Modernization Stack, are poised to transform our IBM Z modernization journey. Join me in embracing the excitement of these newfound capabilities!

[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[light-speed]:https://www.ansible.com/blog/welcome-to-the-ansible-lightspeed-technical-preview?sc_cid=701f2000000txokAAA&utm_source=bambu&utm_medium=organic_social&blaid=4724585
[oc-blog]:../operator-collection-blog
[broker]:https://www.ibm.com/docs/en/cloud-paks/z-modernization-stack/2023.2?topic=automate-zos-resources-provisioning-zos-cloud-broker
[custom-resource]:https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/
[alias-commands]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk#configure-alias-commands-to-simplify-playbook-execution