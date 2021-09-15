# Gain hidden insights from your data using IBM Watson Studio


Introduction

The purpose of this tutorial is to demonstrate features within IBM® Watson™ Studio that help you visualize and gain insights into your data, then cleanse and transform your data to build high-quality predictive models.

Prerequisites

To complete the tutorials in this learning path, you will need an IBM Cloud account, which gives you access to IBM Cloud, IBM Watson Studio, and the IBM Watson Machine Learning Service.

Estimated time

It should take you approximately 30 minutes to complete this tutorial.

Steps

Set up your environment

The following steps are required to complete all of the tutorials in this learning path.

Create IBM Cloud Object Storage service

An Object Storage service is required to create projects in Watson Studio. If you do not already have a storage service provisioned, complete the following steps:

From your IBM Cloud account, search for “object storage” in the IBM Cloud Catalog. Then, click the Object Storage tile.

object-storage-tile

Enter a name and select the Standard version of the service.

object-storage-create

For the Resource Group, you can use the default value, but a better choice is to use a dedicated group that you have created in IBM Cloud. You can find the command for creating new resource groups in IBM Cloud using the Manage > Account menu option, and then navigating to Account resources > Resource groups in the toolbar to the left. The Create button is in the upper right corner of the page.

Click Create.

Launch Watson Studio

Launch Watson Studio, select an appropriate region, and then enter the username name associated with your IBM Cloud account.

studio-login

NOTE: You may notice that the “IBM Watson Studio” banner will in some cases be replaced with the name “IBM Cloud Pak for Data”. The banner used is dependent on the number and types of services you have created on your IBM Cloud account. The change will have no effect on how the service functions or is navigated.

Create Watson Studio project

In Watson Studio, we use the concept of a project to collect and organize the resources used to achieve a particular goal (resources to build a solution to a problem). Your project resources can include data, collaborators, and analytic assets like notebooks and models, etc.

To create a new project, you can either:

Click Create a project from the Watson Studio home page

project-home-page

Or, click on Projects -> View all projects in the left-side navigation menu (☰), then click New project +

menu-projects-list

On the create project panel, you can either create an empty project, or import a file that contains project assets.

create-empty-project

When creating a new project, you will need to provide a unique project name, and an object storage instance. For Storage, you should select the IBM Cloud Object Storage service you created in the previous step. If it is the only storage service that you have provisioned, it is assigned automatically.

create-empty-project

Click Create to finish creating the project.

Provision IBM Cloud services

NOTE: This section discusses creating new services for your project. If you have previously provisioned any of these services, you can choose to use them instead of creating new ones.

Watson Machine Learning service

To provision the Machine Learning service and associate it with the current project:

Select the Settings tab for the project.

Scroll down to the Associated services section.

add-watson-service-menu

Click Add Service.

Select Watson from the drop-down menu.

On the next page, you will be presented with a list of Watson services that you have provisioned on your IBM account.

watson-new-services

If you do not have a Watson Machine Learning service provisioned, or you would like to create a new one, you can do so by clicking the New service + button.

You will then be presented with a list of all available Watson services that can be provisioned from your IBM Cloud account. You can use the search bar to filter the choices to locate the Machine Learning service.

wml-tile

Click the Machine Learning tile to provision your machine learning service.

wml-create-1

From the Machine Learning creation panel, choose the appropriate Region and select the Lite plan.

Note: Make sure you select the same region where your IBM Watson Studio instance is provisioned.

wml-create-2

Use the default Service Name or enter a unique name, then click Create. This will add the new service to your list of available services to associate.

wml-create-2

To associate the service with the project, click the checkbox next to the Watson Machine Learning service instance, then click Associate service.

Note: If you have multiple Machine Learning services, make sure you select the one that is in the same region as is your IBM Watson Studio service.

Once complete, the machine learning service will be listed in the Associated Services section of the project Overview panel.

wml-service-added

IBM Cognos Dashboard Embedded service

To provision the IBM Cognos Dashboard Embedded service and associate it with the current project:

Select the Settings tab for the project.

Scroll to the Associated services section.

Click Add service.

Select Dashboard from the drop-down menu.

add-dashboard-service

On the next page, select New Service to create a new service. This should bring up the IBM Cognos Dashboard Embedded service tile.

cognos-tile

Click the tile to provision your dashboard service.

Select a region and use the Lite plan. Enter a unique name and click the Create button to create the service.

From the Associate service panel, select the new dashboard service, then click Associate service.

You should now have both services listed in the Associated services section of the Settings tab.

associated-services

Upload data set

Use the following link to download the Customer Churn data from Kaggle to your local system.

customer-churn-kaggle.csv
Next, we will upload the file to Watson Studio.

From your Watson Studio project panael, select Assets.

If not already open, click the 1000 data icon at the upper right of the panel to open the Files sub-panel. Then, click Load.

assets-load-data

Drag the file to the drop area to upload the data into Watson Studio.

Wait until the file has been uploaded.

Background

After completing the steps to setting up your environment, you can now focus on the main topic of this tutorial, which is all about data. You’ll learn how to visualize it, then prepare and transform it so that it can be used to build optimized high-quality predictive models.

A classical data science approach to perform these activities is to use the Python programming language running in a Jupyter Notebook. While we cover this method later in the learning path tutorial Build models using Jupyter Notebooks in IBM Watson Studio, this tutorial focuses on alternative ways to achieve the same goal, using features and tools provided by Watson Studio, with no programming required.

Basic visualization in Watson Studio

After data is collected, the next step is referred to as the data understanding phase. This consists of activities that enable you to become familiar with the data, identify data quality problems, and discover first insights into the data.

You can achieve this in Watson Studio by simple user interactions, without a single line of code. To view the data set in Watson Studio, locate the data asset and then click the name of the data set to open it.

select-data-set

Watson Studio shows you a preview of the data in the Preview tab.

data-preview

Alternatively, the Profile tab gives you profiling information that shows the distribution of the values. For numerical features, it also shows the maximum, minimum, mean, and standard deviation for the feature.

To generate the profile the first time:

Select the Profile tab.

Invoke the Create Profile command.

Wait a short while and then refresh the page.

data-profile

Notice that although the numerical columns are identified to be of type varchar, the profiler is smart enough to recognize these to be numerical columns, convert them implicitly, and compute the mean and the standard deviation.

Notice that the churn parameter does not provide a balanced distribution of churn and no-churn observations. This might mean that you should adopt cross-validation strategies during the model building and evaluation phase.

churn-values

More visualizations using the Cognos Dashboard service

You can look further into the data set by creating a dashboard with associated visualizations. This basically requires three steps: creating an empty dashboard, adding a data source to be used for visualizations, and adding appropriate visualizations to the dashboard.

To create the dashboard:

Click Add to project + and then select Dashboard to create a new dashboard.

add-dashboard-to-project

Follow these steps in the New Dashboard page:

Enter a Name for the dashboard (for example, ‘customer-churn-dashboard’.)

Provide a Description for the dashboard (optional).

For Cognos Dashboard Embedded Service, select the dashboard service that you created previously.

create-dashboard

Click Create.

On the next page, select the default tabbed layout and template.

free-form-diagram

Click OK to create an empty freeform dashboard with a single Tab.

To add a data connection:

Click the Add a source button (the + icon) in the upper-left part of the page:

select-source

Click Select to select the customer churn data source.

select-source-file

Back in the dashboard, select the newly imported data source.

Preview the data source by clicking the icon located at the bottom of the tab panel.

show-churn-data

Expand the customer churn data source by clicking > to show the columns.

![data-source-columns](https://s3.us.cloud-object-storage.appdomain.cloud/developer/default/tutorials/watson-studio-data-visualization-preparation-transformation/images/data-source-columns.png)
