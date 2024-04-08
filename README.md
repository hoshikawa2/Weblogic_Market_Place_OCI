# Weblogic OCI Market Place

## Introduction

In this material, we will show how to create an Oracle Weblogic cluster on Oracle Cloud through Market Place. Oracle Cloud Market Place is a rich library of click-to-deploy Terraform stacks that provides complete, fully automated solutions for deploying third-party software on Oracle Cloud Infrastructure.

Through the Market Place, we will have a Weblogic cluster operating in high availability, scalable and integrated with OCI's VCN network. In addition, we will activate OCI Observability where it will be possible to monitor and track the operating metrics of the Weblogic cluster.

### Create an Object Storage to save your Terraform Script

First of all, we need to create a bucket to store the **Terraform** script generated automatically in the **OCI Market Place**. Go to the Main Menu and click on Storage and Bucket options

![img_6.png](img_6.png)

Select your compartment and click on **Create Bucket**. This bucket will be used to store the **Terraform** script.

![img_7.png](img_7.png)

Put a name for your Bucket. Put **Terraform_Scripts** as an example for this tutorial. Maintain the other options as is and click **Create** button.

![img_8.png](img_8.png)

### Create a Secret

Now we need to create 2 secrets in the **OCI Vault**. For security reasons, the **OCI Vault** is a very good way to store passwords and certificates and the **Weblogic Cluster** will use:

- A password for the Admin Console
- A password to use and store the **auto-scaling functions** in the **OCI Container Registry** (Image repository in OCI)

Now, go to the Main Menu and click on **Identity & Security** and **Vault** options.

![img_26.png](img_26.png)

Select the compartment you want to store the secrets and click on **Create Vault** button

![img_29.png](img_29.png)

Put a name for your vault, confirm the compartment and click on **Create Vault** button

![img_30.png](img_30.png)

Confirm the vault creation and let's create a key. Click on **Create Key** button

![img_33.png](img_33.png)

Confirm the compartment and put a name for your key. For example, put **weblogickey** on Name and click on **Create Key** button

![img_34.png](img_34.png)

Confirm the key creation

![img_35.png](img_35.png)

Now, click on **Secrets** option and click on **Create Secret** button

![img_31.png](img_31.png)

We will create the **Weblogic Admin** password. Confirm the compartment, put a name for your first secret. Select **Manual secret generation** to include the password. Select **Plain-Text** option on **Secret Type Template** and write your password. Finally, click on **Create Secret** button.

![img_47.png](img_47.png)

>**Note:** The password must start with a letter, is between 8 and 30 characters long, contain at least one number, and, optionally, any number of the special characters ($ # _). **If you don't respect this rule, the Weblogic Instance cannot be created.** 

![img_37.png](img_37.png)

Now we will create a new secret for your Image Repository (**OCI Container Registry**).

**Oracle Cloud Infrastructure Container Registry** is an open standards-based, Oracle-managed Docker registry service for securely storing and sharing container images. Engineers can easily push and pull Docker images with the familiar Docker Command Line Interface (CLI) and API. To support container lifecycles, Registry works with Container Engine for Kubernetes, Identity and Access Management (IAM), Visual Builder Studio, and third-party developer and DevOps tools

If you don't know about how to use the **OCI Repository**, please see this article [Push an Image to Oracle Cloud Infrastructure Registry](https://www.oracle.com/webfolder/technetwork/tutorials/obe/oci/registry/index.html), you will need to know your **token** access.

Again, click on **Create Secret** button and fill the **Secret Contents** with your **OCIR token**. Click on **Create Secret** button.

![img_40.png](img_40.png)

You can see the **Base 64** conversion value of your token by clicking the **Show Base64 conversion** toggle key.

![img_46.png](img_46.png)

Confirm if your 2 secrets were created

![img_41.png](img_41.png)

### Create an Observability Application Performance Monitoring

Use Oracle Cloud Infrastructure observability and management services to gain visibility and actionable insights that help you to manage your cloud environment.

Oracle Cloud Infrastructure services related to observability and management let you monitor, audit, and alert to changes in your cloud environment. Insights driven by amachine learning help you to manage resources that are deployed on a variety of technology across all layers of the stack.

A top priority is to increase automation that enables scalable, predictable results. Use integrated functionality and automation for DevOps monitoring and IT operations management to prevent and solve IT problems.

You can use the **Application Performance Monitoring (APM**). Application Performance Monitoring provides deep visibility into applications performance and enables rapid diagnostics in order to deliver a consistent level of service. This includes the monitoring of the multiple components and application logic spread across clients, third-party services, and back-end computing tiers, on premises or on the cloud.

Let's create an **APM** in the **OCI**. Open the Main Menu and select **Observability & Management** and the **Administration** option.

![img_49.png](img_49.png)

Select your compartment to create an **APM** domain and click in the **Create APM domain** button

![img_50.png](img_50.png)

Put a name for your **APM Domain**, confirm your compartment and click on **Create** button.

![img_51.png](img_51.png)

### Create the Weblogic Clustered Instance

Let's create your **Weblogic Cluster**. Go to the Main menu

![img_1.png](img_1.png)

Select **Marketplace** option

![img.png](img.png)

Now select the **All Applications**

![img_2.png](img_2.png)

Write on **Search** text box "webogic". The **Weblogic** options will appear on screen

For the **Weblogic H.A.** option, select for example the **Weblogic Enterprise** or **Weblogic Suite**.

![img_3.png](img_3.png)

Select the **Version** and compartment for your **Weblogic Cluster**, confirm the acceptance terms and click on **Launch Stack** button

![img_4.png](img_4.png)

Click on **Use custom Terraform providers** option to generate your Terraform scripts. Select the compartment of your bucket previously created and your bucket name. 

![img_9.png](img_9.png)

You can put a name for your stack or leave the default name.

![img_10.png](img_10.png)

Click **Next** button. Put a prefix name for your **Weblogic** stack. All resources created in Terraform process will contain this prefix name

![img_11.png](img_11.png)

Generate a Public and Private key file. Put the public key here. This will be used to authenticate your bastion instance.

![img_12.png](img_12.png)

Maintain **OCI Policies** enabled.

![img_13.png](img_13.png)


### Working with VCN, Subnets, Private/Public, Bastion

You can use a valid **VCN** inside the **OCI** or create a new one. If you don't have any **VCN** create, select **Create a Virtual Cloud Network** option.

![img_14.png](img_14.png)

### Working with Load Balancer

Your **Weblogic** instance will be created on a clustered environment. So, you can stablish the number of **Weblogic** instances and can balance the use of this servers through a **Load-Balancer**. Select **Provision Load Balancer** option.

![img_15.png](img_15.png)

You can customize the **CIDR** block and performance options for the **Load Balancer**

![img_24.png](img_24.png)

### Working with IDCS

**Oracle Identity Cloud Service (IDCS)** is an Identity-as-a-Service (IDaaS) solution available in Oracle Public Cloud (OPC). It is designed to extend enterprise controls by automating PaaS and SaaS account provisioning and deprovisioning, simplifying the user experience for accessing cloud applications by providing seamless integration with enterprise identity stores and authentication services, and facilitating compliance activities by clearly reporting on cloud application usage

You can integrate your **Weblogic Cluster** with IDCS. If you want to integrate with **IDCS**, click on **Enable Authentication Using Identity Cloud Service** option

![img_16.png](img_16.png)

### Observability

If you want to integrate the **OCI Observability** with your **Webloigc Cluster**, enable this options:

![img_17.png](img_17.png)

And select your **APM Domain** created previously in your compartment.

![img_39.png](img_39.png)

### Auto Scaling

The **Weblogic** stack available on **Oracle Cloud Market Place** allows the use of the automated mechanism for auto-scaling. This feature is available thanks to the use of **OCI functions** that are automatically implemented when creating the Weblogic stack.
To activate this option, simply enable the "Autoscaling" option and configure the **OCI Registry** with your previously configured username and token.
Also configure thresholds to automate autoscaling.

![img_18.png](img_18.png)

![img_42.png](img_42.png)

### File System - H.A.

There is the possibility of working with shared storage, which is very important when it comes to creating a Weblogic cluster for high availability.
To do this, simply enable the "Add File System" option and configure the subnet's CIDR block to mount the target. Be careful to establish a CIDR block that does not overlap an existing one.

![img_19.png](img_19.png)

![img_25.png](img_25.png)

### Configure a VCN

Now you need to create where your **Weblogic** instance will operate. That means to configure the VCN and subnets. You selected to create a new **VCN**, so you can put here a name for your **VCN** and choose optionaly the **CIDR** block for the network. Subnets will be created automatically. Remember to check your compartment for your **VCN**.

![img_20.png](img_20.png)

### Domain Configuration

Let's configure the **Weblogic** domain. Put the **Admin User Name**, default is weblogic.
Select the compartment of your secret created previously and select the **weblogicadmin** secret.
Select your **JDK** version and if you want, you can create a sample application, just select **Deploy Sample Application** option for this.

![img_38.png](img_38.png)

### Configure Weblogic Instances

Here you can configure your cluster machines. Select your **OCI** compute shape, the **OCPUs** size and the number of **Nodes** for your cluster.
You can configure the **CIDR** block for your servers subnet.

![img_22.png](img_22.png)

### Working with Bastion

Bastion usually helps to mantain your **Weblogic** cluster secure, so you need to access the **Weblogic** admin through this **bastion** server. While bastion will be exposed over a public IP, your **Weblogic** machines will be maintained in a secure private subnet.

Enable "Assign Reserved Public IP to Bastion Instance", configure the **CIDR** block for the subnet and choose the Bastion shape.

Remember to use your private key configured previously to access your bastion in a **SSH** connection.

![img_23.png](img_23.png)

Obtain the **Public IP** of your bastion in the **Compute** menu and in you bastion detail.

An example to access your bastion is:

    ssh -i <PrivateKey.pem>  opc@<Bastion Public IP> -L 7002:localhost:7002

So you can stablish a tunnel for your Weblogic Admin Server.

You can now access your admin server with your browser with:

    https://localhost:7002/console

## Confirm the Stack creation

![img_43.png](img_43.png)

![img_44.png](img_44.png)

![img_45.png](img_45.png)

## Reference

- [Create a Non-JRF Instance Using Oracle WebLogic Server for OCI With New VCN](https://docs.oracle.com/en/cloud/paas/weblogic-cloud/wlcgs/index.html)
- [Autoscaling Weblogic in OCI](https://blogs.oracle.com/weblogicserver/post/monitoring-and-autoscaling-oracle-weblogic-server-for-oci-stack-with-customized-domains)
- [OCI APM Agent for Weblogic](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/deploy-apm-java-agent.html#GUID-081D2588-8A46-46CA-9297-3654002702D0)
- [Install and Configure APM Java Agent On Oracle Weblogic Server](https://docs.oracle.com/en/cloud/paas/management-cloud/dmapm/install-and-configure-apm-java-agents-oracle-weblogic-server.html#GUID-05347698-5AED-4980-BBAC-0588BED98DDE)
- [Push an Image to Oracle Cloud Infrastructure Registry](https://www.oracle.com/webfolder/technetwork/tutorials/obe/oci/registry/index.html)
