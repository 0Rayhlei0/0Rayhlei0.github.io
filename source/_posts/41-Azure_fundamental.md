---
title: "[数据分析] Azure基础知识"
date: 2024-4-27 15:58:45
tags: [日常学习, Azure, 云计算]
categories: 数据分析
description: "[第41篇] 本章为通过DataCamp学习的Azure平台的相关基础知识。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/data.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/41-Azure_fundamental.jpg
---

# 序言

2024年回家过年把心玩散了，一直到现在接近年中了才忽然发觉原来已经很久没有更新网站了，最近工作上客户价格敏感度模型已经做出了一个比较合理的使用方案，马上将投入实例测试，届时有了结果我会再把具体的细节记录一下。这次重新开始写文章是因为公司开始了一些转型，准备将日常工作接入云计算平台和数据科学平台。云计算平台我们使用的是微软的Azure，所以这次就系统地复习了解一下Azure是什么，以及他能帮到我们完成什么任务。

# 正文

## 1. 云计算

互联网需要服务器来处理各种请求，交换信息。而当一个网站的访问量以及数据处理量增加时，公司只能靠增加服务器来增加数据处理速度，因此如果一个网站建立在`内部部署(on-premise)`的服务器上， 那么这些服务器就需要能够处理网站访问高峰期的流量，否则就会出现网站延迟卡顿无法访问的情况，而当网络访问量减小时这些多出来的服务器算力则只能被闲置浪费。所谓云计算(Cloud computing)就是通过互联网提供算力、存储、数据库、网络连接、软件等等技术服务，通过互联网共享云服务器的算力，从而控制服务器部署的时间和使用效率成本。

### 1.1 云计算的特点

云计算还有以下很多主要特点：

1. 虚拟化(Virtualization)：云计算是在服务器中建立虚拟层，将算力分成多个虚拟服务器，每个虚拟服务器运行独立的操作系统和应用，这种方式可以使服务器算力资源得到更充分利用， 而且可以将虚拟层和物理层有效分隔开，更便于在云环境中管理或变动使用各个虚拟服务器。

![传统服务器对比虚拟服务器](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20240427203624638.png)

2. 易扩增性(Scalability)：云计算的资源分配具有较高的易扩增性，用户可以按需随时增加或者减少所需的资源，资源可以`竖向扩增(Vertical Scaling)`或`横向扩增(Horizontal Scaling)`，前者是指增加单个服务器的算力，后者则是指增加服务器的数量。
3. 成本(Cost)：云计算相较于传统的本地部署可以节约更多成本，主要原因是第一可以按时间分配算力，以实际使用的资源计价；第二云计算不需要部署各种服务器软硬件，或者聘请专业维护人员。
4. 速度(Speed)：云计算资源的部署速度要远快与传统服务器，不需要从头购买部署硬件。
5. 性能(Performance)：云计算可以拥有非常快速而高效的服务器性能。
6. 增长(Growth)：由于其不受硬件限制，云平台可以让业务增长不受地理限制。
7. 可靠性(Reliability)：云计算服务提供商通常会在多个服务器备份数据从而确保数据的可用性。
8. 安全性(Security)：由于云计算需要将数据资料存储在第三方服务提供商的服务器中，因此有时企业会基于数据安全的考虑而使用内部部署服务器。

### 1.2 云服务模式

|      | IaaS<br />(Infrastructure as a Service)                      | PaaS<br />(Platform as a Service)                            | SaaS<br />(Software as a Service)                            |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 定义 | 内部部署服务器的云解决方案                                   | 通过网络提供应用开发所需的软硬件                             | 通过网络提供软件服务                                         |
| 优势 | 相较内部部署服务器设施更快速易扩增                           | 开发者不需要从头开始开发应用                                 | 不需要在本地安装软件                                         |
| 用户 | 系统管理员                                                   | 程序开发者                                                   | 终端客户                                                     |
| 举例 | 云服务器<br />(Google Compute Engine, Microsoft Azure, Amazon Web Services) | Web apps, logic apps<br />(Google App Engine, Windows Azure, AWS Elastic beanstalk) | 互联网应用程序<br />(Google G suite, Microsoft Office 365, Dropbox) |

### 1.3 云部署模式

基于业务需求和预算， 用户需要决定使用怎样的云部署方式，最常见的云部署方式有公共，私有和混合：

- 私有云(Private Cloud)：云设施为用户专用，通过网页链接访问，因此用户拥有对云资源的直接控制权。譬如使用特定的操作系统或硬件等。但这种模式需要更多的资本和时间投入，这种方式与内部部署服务器的区别在于私有云将资源私有化，因此可以不用内部部署服务器(off-premises)。
- 公共云(Public cloud)：云设施由普通大众共享使用，由云服务提供商所有并管理，用户通过互联网访问。相较于私有云，公共云可以以更小的投资更快地实现部署，并且可以快速扩增，但用户没有硬件和数据中心的访问权。
- 混合云(Hybrid cloud)：用户可以将上两种模式混合使用，比如使用私有云存储敏感数据而使用公共云上的应用做分析计算；或是使用`云爆发(cloud bursting)`技术，在当请求超过私有云算力极限时暂时性使用公共云算力来避免服务中断。

其他还有一些云部署方式例如使用多个云提供商服务的`多云(Multicloud)`，或由某个团体共享设施的`社区(Community)`等。

### 1.4 云服务提供商

截至2023年末，市场上的主要云服务提供商的市场份额如下，其中以亚马逊的AWS，微软的Azure和谷歌的Google cloud市场份额最大，我们本章主要了解这三家提供商的特点和强项。

![截至2023年末主要云服务提供商市场份额](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20240428224055756.png)

#### AWS

AWS全称Amazon Web Service，于2006年成立。他的三个主要的专业云应用有`云文件存储的Simple Storage Service(S3)`，`云计算的Elastic Compute Cloud(EC2)`，和`数据库服务的Relational Database Service(RDS)`。数据方面他们有提供数据分析和数据仓库服务的`Redshift`， 实时数据分析的`Kinesis`，以及机器学习平台`SageMaker`。

#### MS Azure

Azure是微软的云平台，微软首先是把自己家的MS Office, Windows Server, SQL Server等移到了云上，因此这些微软的应用与Azure的生态联系比较紧密。Azure的主要产品有提供`云存储的Azure Blob Storage`，`云计算的Azure Virtual Machines`，和`数据库的Azure SQL Database`。另一个关键的云计算产品是Microsoft Fabric，这是一个微软为企业设计的一体化解决方案，涵盖了数据传送，数据科学，实时分析，商业只能等各种服务。数据方面，Azure还提供存储未处理数据的`Data Lake Storage`，实时数据分析的`Stream Analytics`，以及机器学习服务的`Machine Learning`。 

#### Google Cloud

谷歌认为由于用户不希望被某个云服务提供商锁定，因此他们认为多云是未来的趋势，他们的Google Cloud Anthos可以让客户同时管理多个不同的云平台上的混合云服务而不需要担心运行环境或接口。Google Cloud有提供`云存储的Google Cloud Storage`，提供`云计算的Google Cloud compute engine`，还有提供`数据库的Google Cloud SQL`。数据方面则有数据仓库服务的`Big Query`，方便数据分析的`Dataflow`，以及机器学习方面的`AutoML`。

## 2. Azure核心组件

- 资源(Resources)：每当用户在Azure购买一个服务（譬如网站托管，虚拟机等）时，他们会收到一个被称为资源的JSON文件，其中包含了四个基本属性：type, API version, name和location，有些服务的资源还会有其他参数。这些资源被分类存放在`资源组(Resource groups)`中，用户可以将相关的资源按服务种类，应用生态，位置或部门等分类，便于管理即可。
- Azure Resource Manager (ARM)：ARM是Azure使用统一语言集中管理资源和资源组的层，每当用户需要新建、管理、或删除一个资源时，ARM就会将用户权限与Azure ActiveDirectory对比，这是微软的一个云上身份权限管理服务系统。

![ARM示意](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20240429215644814.png)

Azure资源管理的结构图如下：

![Azure hierarchical structure](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20240704225706630.png)

## 3. Azure服务

Azure提供的云服务主要涵盖四个方面：`Compute（计算）`、`Storage（存储）`、`网络（Networking）`、以及`数据库（Databases）`。计算服务包括Virtual Machines, Container Instances, Kubernetes等；存储服务包括Azure Data Lake Storage，Azure Files, Azure Blob Storage等；网络服务包括Content Delivery Networking, Virtual Network Manager, VPN Gateway等；数据库服务包括Cosmos DB, SQL Database, SQL Managed Instance等。

一些数据与AI相关的的服务简介如下：

- Azure Data Lake：用于统一存储所有不同来源的数据的巨型数据“蓄水池”。
- HDInsight：用于处理并筛选Data Lake中的数据。
- Azure Synapse：集成大数据技术的数据仓库和分析平台。
- Stream Analytics： 提供数据实时分析服务。
- Azure Machine Learning：流水化机器学习模型搭建、训练、部署。
- Azure Cognitive Services： 提供预置的AI功能，例如语言理解、计算机视觉、语音识别等。
- Azure Databricks：大数据机器学习分析平台。
- Azure AI services： 为应用增加AI功能，例如语言理解语音识别等。

### 3.1 Azure Compute

Azure的计算方面主要有几个核心产品：Virtual Machine, Azure App Service, Azure Function, Azure Kubernetes Service, Azure Container Apps, 以及 Azure Container Instances。

`Virtual Machine`按需提供易扩增且高度自定义的算力，用户可以随时增删电子化的计算机，且用户拥有该虚拟机系统和软件的完全控制权。使用Virtual Machine的一个场景可能是你的某个应用需要使用特定版本的软件，而你可以用Virtual Machine将该应用与其他使用更新版本软件的应用隔离。
`Azure App Service`则是辅助网页应用和手机应用开发的工具，他可以让开发者无需关心硬件设施而只需关注写代码开发功能。他还能使用版本控制工具连接到GitHub、Azure repository等仓库进行持续集成和开发。

`Azure Function`是Azure提供给开发者的serverless计算服务，用于云上执行函数计算而不需要管理基础设施。

`Container(容器)`是指携带程序运行所需的所有如库、配置文件等必要依赖的轻量包。与虚拟机相比，容器不需要有整个操作系统就可以避免运行应用时遭遇兼容性问题，你有时甚至可以同时运行多个容器。Azure有多种不同的部署容器化应用的选项，例如Azure Kubernetes Service(AKS)、Azure Container Apps、Azure Container Instances等。

`Kubernetes`相当于一个大型乐团中的指挥家，用于协调管理一个计算机簇中的各个容器。而`AKS`则是用于自动化管理容器安排、健康监控、扩增等；是一个便于应用开发测试部署的集成环境。

`Container Instances`是Azure提供的另一个serverless服务，可以让用户不需要操心虚拟机或Kubernetes管理等的轻量化容器服务，主要用于快速应用开发测试，微服务部署等等小型或单次的项目，所谓`微服务(microservices)`是一种将应用分隔成更小的独立的服务的方法，例如购物平台中不同功能由不同的微服务支持，不同微服务通过API与其他微服务沟通。

`Azure Container Apps`则是一个便于现代应用和微服务部署和管理的应用平台，不要把它和Azure App Service搞混，虽然都是用来托管应用程序的平台，但ACA主要用于部署容器化应用或微服务，用于管理使用不同环境的微服务等；而AAS则是主要用来托管网页应用。

### 3.2 Azure Storage

 Azure的存储服务最多分为四挡，`Hot`最快最贵，适用于高访问频率，例如网站图片；`Cool`其次，较为便宜且适用较低评率访问量，但依然不慢，例如客户上传资料等； `Cold`通常是较少访问的数据，比如短期备份。`Archive`最便宜，适合长期储存，访问频率更低的数据，比如长期备份。这里介绍Azure提供的四种主要存储服务：Blob Storage, Data Lake Storage, Files和Backup/Recovery。

`Azure Blob(Binary large object) Storage`主要用于储存文字，视频或图像等`非结构化数据(unstructured data)`。Blob存储的主要特点是易扩增且能被全球访问，用户能通过HTTP/HTTPS协议从世界各地访问这些存储的数据。

`Azure Data Lake Storage`是一个用于存储分析大量数据的服务，将Blob Storage的大量文件储存能力与文件管理系统相结合，使该服务能满足快速高效的数据访问和分析。Data Lake可以高效处理PB级别的各种结构化，半结构化，和非结构化数据，因此非常适合做大数据分析项目。如前文所提，Data Lake的存在使所有数据源不需要互相适配接口，而将所有数据都统一存放在湖中，再在需要使用时直接从湖中访问。

`Azure Files`则是一个云上的文件分析服务，在组织中需要内部分享文件或是需要无缝合作时可以使用，将Azure Files服务可以与Windows File Explorer直接连接，使用方法和其他本地硬盘分区无异。一旦存储接入Azure云，这些文件就可以从各种操作系统访问，适合需要各种操作系统协同作业时的工作场景。

`Azure Backup and Recovery`主要用于安全地备份本地和云上文件，使用Azure存储服务来保障备份数据的安全性和灾难后的数据恢复，数据备份是在后台进行而无需用户关心的。

最后Azure提供了几项Data redundancy的选项，`Locally redundant storage(LRS)`是最便宜的，也即只将数据在本地数据中心备份，`Geo-redundant storage(GRS)`将数据备份在另一个不同的地区，而`zone-redundant storage(ZRS)`则将数据备份在同一个地区的不同三个数据中心中，以保证可访问性。最贵的redundancy选项则是同时具备GRS和ZRS特性的GZRS选项。

其他Azure Storage服务还有便于存储瞬时序列数据如双十一购物节时的订单信息等的`Queues`;便于存储大量易访问的类似key-value pairs这样非结构化数据的`Tables`等。

### 3.3 Data Processing in Azure

这里介绍Azure中与数据处理相关的5种不同工具：Synapse Analytics, Stream Analytics, Databricks, Data Factory和HDInsight。

`Azure Synapse Analytics`是一个集成在新的Microsoft Fabric分析套中的数据分析工具，它包含了大数据系统和数据库等功能，可以将数据收集准备并提供给类似PowerBI的分析工具用作分析，并且集成Azure machine Learning等服务以作分析或建模。

`Azure Stream Analytics`则更偏向解决需要实时数据分析的应用场景，比如银行的诈骗分析，流水线的生产效率分析等。

`Azure Databricks`是微软和Databricks合作的产物，是适配于Azure的数据分析平台，其集成了数据工程，数据分析，和机器学习。用户可以通过该平台共同实时参与大数据项目。该平台集成了许多Azure服务或工具，比如使用Azure Data Lake作为存储工具，用Active Directory做身份验证，PowerBI和Synapse analytics做数据分析，可以满足各种各样的数据处理需求。

`Azure Data Factory`是一个基于云技术的数据ETL处理集成服务，可用于自动化处理各种来源的数据，包括SQL, NoSQL数据库，Blobs等。

`Azure HDInsight`可以用于低成本快速自订地处理大量数据的服务，他可以在各种类似于Hadoop, Spark, Kafka这样的开源平台上运行。HDInsight可以快速适应需求，并且完美适配Azure存储方案。

### 3.4 Azure Networking

`网络(Networking)`是关于连接电脑设备并分享数据和资源，提供交流和协作。网络的涵盖范围包括硬件（路由器和网线）和数据交换的通信协议。Azure使用`Azure virtual network（VNET）`来建立虚拟机、网页应用、数据库等云资源间的联系，VNET是虚拟的因为资源间并非直接物理连接而是通过软件连接。VNET使用私有IP互相连接，因此云资源彼此间可以通信但不能通过互联网访问，VNET内的资源想要连接互联网必须要附加一个公共端点，例如虚拟机想要连接互联网就可以通过给它分配公共IP来实现。

不用VNET内的资源也可以通过使用微软的网络进行`network peering`来绕过公共网络实现信息通信。Azure还可以通过VPN服务(即Aure VPN Gateway) 来实现本地部署环境与云环境的信息通信，这样虽然通信会经过互联网，但内部信息是加密且拒绝非授权访问的。如果公司需要更加安全的连接方式，Azure还有Azure ExpressRoute可以通过私有连接直接连接本地部署的网络至云环境。

# 最后

本篇只是一个对于云计算和Azure的最基本的了解和概览，我们工作中具体会使用的应该只是Azure中某个服务而已，例如Azure Databricks平台。后续我会更新Databricks相关的学习笔记。



[第41篇]

