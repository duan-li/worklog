---
layout: post
title: Machine Learning APIs
date: 2019-05-31 22:33 +0000
---


## Overview
APIs (Application Programming Interfaces) are software programs that give developers access to computing resources and data. Companies from many different fields offer publicly available APIs so that developers can integrate specialized tools, services, or libraries with their own applications and codebase.

This lab will teach you about the architecture and basic functioning of APIs. This will be supplemented with hands-on practice, where you will configure and run [Cloud Storage API](https://cloud.google.com/storage/docs/json_api/) methods in Google Cloud Shell. After taking this lab you will understand key principles of API communication, architecture, and authentication. You will also gain practical experience with APIs, which you can apply to future labs or projects.


### Objectives
In this lab, you will learn about:

* Google APIs
* API architecture
* HTTP protocol and methods
* Endpoints
* REST (Representational State Transfer) and RESTful APIs
* JSON (JavaScript Object Notation)
* API authentication services


### Prerequisites


This is an **introductory level** lab. This assumes little to no prior knowledge of APIs or experience using Google APIs. Familiarity with shell environments and command line interface tools is recommended, but not required. Familiarity with the GCP Console and Cloud Storage is recommended, so please at a minimum take the following labs before attempting this one:

* [A Tour of Qwiklabs and the Google Cloud Platform](https://google.qwiklabs.com/catalog_lab/1281)
* [Cloud Storage: Qwik Start - Console](https://google.qwiklabs.com/catalog_lab/1089)


Once you're ready, scroll down and follow the steps below to set up your lab environment.


### Setup and Requirements

#### Qwiklabs setup

##### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access the Google Cloud Platform for the duration of the lab.


##### What you need
To complete this lab, you need:

* Access to a standard internet browser (Chrome browser recommended).
* Time to complete the lab.

**Note**: If you already have your own personal GCP account or project, do not use it for this lab.


### APIs - What and Why


As mentioned earlier, an API (Application Programming Interface) is a software program that gives developers access to computing resources and data. APIs adhere to specific rules and methods to clearly communicate requests and responses.

The ability to access data and computing resources greatly increases a developer's efficiency. It is much easier to use an API than to build every single program, method, or dataset from scratch. APIs are built on the principle of abstraction—you don't need to understand the inner workings or complexities of an API to use it in your own environment.

APIs are built with the developer in mind and often times do not offer a graphical user interface (GUI). However, there are exceptions to this standard. Google has released a new tool called [APIs Explorer](https://developers.google.com/apis-explorer/#p/), which allows you to explore various Google APIs interactively (be sure to check out the [APIs Explorer: Qwik Start](https://google.qwiklabs.com/catalog_lab/1241) lab afterwards if you are interested in learning more.)


### APIs in GCP
Google offers APIs that can be applied to many different fields and sectors. APIs are often used in web development, machine learning, data science, and system administration workflows. However, these are only a handful of use cases. If you explore [AnyAPI](https://any-api.com/), for example, you will start to see just how many APIs are available.

When Qwiklabs provisions a new GCP Project for a lab instance, it enables most APIs behind the scenes so you can work on the lab's tasks right away. If you create your own GCP projects outside of Qwiklabs, you will have to enable certain APIs yourself.

As you gain proficiency as a GCP user, you will start to use more APIs in your workflow. Experienced GCP users will integrate and use Google APIs in their local environments almost exclusively, rarely using the GCP Console to run tools and services. Dozens of labs are available that give you practice with various Google APIs in different languages. Here are two for example:

* [Cloud Natural Language API: Qwik Start](https://google.qwiklabs.com/catalog_lab/709)
* [Entity and Sentiment Analysis with the Natural Language API](https://google.qwiklabs.com/catalog_lab/1113)
You will now explore the [API library](https://console.cloud.google.com/apis/library?project=hello-world-sean-200116&folder&organizationId) to see what Google APIs are available.



### API Library
Open the **Navigation menu** and select **APIs & Services** > **Library**:

![API Library](/assets/images/ml-01/IhN1xAfMsp0KrMIwX50LGtlzcsup+fK45UA1wseaaa4=.gif)


The **API library** offers quick access, documentation, and configuration options for 200+ Google APIs. Even though it's housed in the Console, it's important to note that the library offers access to all Google APIs — not only GCP centric ones. This highlights an important theme: APIs are fundamental to all Google services, and Google APIs don't all fall under the GCP category.

Time for some hands-on practice enabling an API in the API library. Assume that you are a mobile developer for a fitness site and you want to use the [Google Fitness API](https://developers.google.com/fit/) to build your application.

In the "Search for APIs and Services" search bar, type in Fitness API and press Enter. Click on the Fitness API from the result list. Then, click Enable. If you return to the Fitness API in the API library by clicking on the back button in your browser window twice, you will see that the API is now enabled:



![Fitness API](/assets/images/ml-01/ITUhZGXAvVpHh+xqaIT0Vy9UAMrWL6h8kYpL8PSeKZI=.png)

The API library provides links to tutorials and documentation, terms of service, and interactive methods offered in the APIs Explorer. To see metric and usage information, you will use the API Dashboard.


### API Dashboard
Inspect the Fitness API in the GCP Console's API Dashboard. Open the navigation menu and and select APIs & Services > Dashboard:

![API Dashboard](/assets/images/ml-01/luTPsurvO5Bl_BZKKUmqRZAtBJavYoBvx+bsdov_t00=.png)


The API Dashboard details your project's usage of specific APIs, including traffic levels, error rates, and even latencies, which helps you quickly triage problems with applications that use Google services.

From the API list, select Fitness API:


















---