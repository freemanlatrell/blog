---
title: 'Building an Operator Collection using Ansible Lightspeed with Watson Code Assistant'
slug: 'building-an-operator-collection-with-ansible-lightspeed'
image: 'images/light-speed.jpg'
imageDescription: Photo by Joshua Sortino on Unsplash
date: "2023-07-06T00:00:00"
disableComments: false
author: Latrell Freeman
authorTitle: Lead Architect - IBM z/OS Cloud Broker
---

With the release of the [IBM Operator Collection SDK][oc-sdk], we've simplified the [Operator Collection][oc-blog] development process by providing all of the tools needed to quickly deploy and debug your Ansible content in OpenShift. Now, with the [Tech Preview release of Ansible Lightspeed with IBM Watson Code Assistant][light-speed], we can further simplify this development process using generative AI, to streamline the creation of the Ansible content in your Operator Collection.

Ansible Lightspeed with IBM Watson Code Assistant is a generative AI tool, used to build quality Ansible code quickly and efficiently. This is enabled via the Ansible VS Code extension in your VS Code editor. The foundational model trained on open source data, allows for task recommendations based soley off of the task name entered by the user.

In this blog, we'll walk through the steps on how to initialize an Operator Collection using the IBM Operator Collection SDK, create two playbooks that create and delete a file on a remote host using Ansible Lightspeed with IBM Watson Code Assistant, and deploy this Operator Collection to OpenShift using the IBM Operator Collection SDK, where we can then validate that our operator is working as expected.

## Step 1: Install the IBM z/OS Cloud Broker Operator
To develop an Operator Collection and deploy it in OpenShift, we must first install the [IBM z/OS Cloud Broker][broker] operator.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_1.mp4">
</video>

{{< /rawhtml >}}

## Step 2: Initialize the Operator Collection
Using the IBM Operator Collection SDK, we will now initialize our Operator Collection, to generate a template with all of the requirements needed to be consumed by the IBM z/OS Cloud Broker.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_2.mp4">
</video>

{{< /rawhtml >}}

## Step 3: Generate playbook tasks using Ansible Lightspeed with IBM Watson Code Assistant
Now that we've initialized our Operator Collection, we can now use Ansible Lightspeed with IBM Watson Code Assistant to generate the tasks in our playbooks by simply specifying a task name with what we want our task to execute, and allowing Ansible Lightspeed to provide the recommendation to accomplish that task. 

We'll start with a playbook called `create_file.yml` which will create a new directory on our host, and touch a new file in the directory that was previously created.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_3.1.mp4">
</video>

{{< /rawhtml >}}


We'll also create a playbook called `delete_file.yml`, to delete the previously created file when the instance is deleted in OpenShift.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_3.2.mp4">
</video>

{{< /rawhtml >}}


## Step 4: Update the operator-config.yaml file
Once we've configured our playbooks, we should now configure the required values in our `operator-config.yml` file. Here is where we'll specify the name of our operator, the description, and provide an icon to display in OpenShift. This is also where we will specify the [custom resource][custom-resource] name which allows us to extend the Kubernetes API with our own custom API called `File`, the playbooks to execute when a user creates/deletes an instance of our new `File` API, and variables that will be exposed to the user in OpenShift to be supplied to our playbook. In this example, we only need a single variable called `filename`.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_4.mp4">
</video>

{{< /rawhtml >}}

## Step 5: Create the Operator using the IBM Operator Collection SDK
Now that we've created our playbooks and configured the `operator-config.yaml` file, we are now ready to validate our Operator Collection in OpenShift. To avoid manually packaging our collection, uploading the collection to the IBM z/OS Cloud Broker, and configuring our operator and host in the IBM z/OS Cloud Broker UI, we can simply execute the `create_operator.yml` playbook provided by the IBM Operator Collection SDK using the `ocsdk-create-operator` alias on the command line.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_5.mp4">
</video>

{{< /rawhtml >}}

## Step 6: Create a File instance in OpenShift
To validate that our `create_file.yml` playbook is working as expected, we should create an instance of the new `File` custom resource, specifying the `filename` to create, and the host to create this file against.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_6.1.mp4">
</video>

{{< /rawhtml >}}


Once the instance is created successfully, we can SSH into our host to validate that the new file exists.

{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_6.2.mp4">
</video>


{{< /rawhtml >}}

## Step 7: Delete the File instance in OpenShift
To validate that our `delete_file.yml` playbook is working as expected, we should delete the `File` instance that was just created in OpenShift, which should trigger our `delete_file.yml` playbook before removing the custom resource instance in OpenShift.


{{< rawhtml >}} 

<video width=75% controls autoplay>
    <source src="../../images/broker_lightspeed_step_7.mp4">
</video>

{{< /rawhtml >}}


## Wrapping Up
What I have covered above are the capabilities that are now available to Ansible developers to rapidily develop Ansible content using Ansible Lightspeed with IBM Watson Code Assistant, and rapidly deploy and test this content as an operator in OpenShift using the IBM Operator Collection SDK. I encourage you to try this out for yourself using the links below for everything your need to get started. All of the tools used in this demo are free to get started, with the 60 day free trial of the IBM Z and Cloud Modernization Stack now available to access the IBM z/OS Cloud Broker, and the Tech Preview release of Ansible Lightspeed with IBM Watson Code Assistant also available for free.

I hope you are as excitied as I am about the new capabilities of generative AI, in combination with the tools available in the IBM Z and Cloud Modernization Stack, to help accelerate our IBM Z modernization journey! 


## Resources
- 60 day free trial of the IBM Z and Cloud Modernization Stack: https://www.ibm.com/account/reg/us-en/signup?formid=urx-51680
- Tech Preview release of Ansible Lightspeed with IBM Watson Code Assistant: https://www.ansible.com/blog/welcome-to-the-ansible-lightspeed-technical-preview?sc_cid=701f2000000txokAAA&utm_source=bambu&utm_medium=organic_social&blaid=4724585

[oc-sdk]:https://github.com/IBM/operator-collection-sdk/tree/main/ibm/operator_collection_sdk
[light-speed]:https://www.ansible.com/blog/welcome-to-the-ansible-lightspeed-technical-preview?sc_cid=701f2000000txokAAA&utm_source=bambu&utm_medium=organic_social&blaid=4724585
[oc-blog]:../operator-collection-blog
[broker]:https://www.ibm.com/docs/en/cloud-paks/z-modernization-stack/2023.2?topic=automate-zos-resources-provisioning-zos-cloud-broker
[custom-resource]:https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/