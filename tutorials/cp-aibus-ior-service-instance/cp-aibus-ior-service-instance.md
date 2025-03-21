---
title: Create Service Instance for Invoice Object Recommendation
description: Create a service instance and the associated service key for Invoice Object Recommendation, one of the SAP AI Business Services, using SAP Business Technology Platform (SAP BTP) Trial.
auto_validation: true
time: 15
tags: [tutorial>beginner, topic>machine-learning, topic>artificial-intelligence, topic>cloud, products>sap-business-technology-platform, products>sap-ai-business-services, products>invoice-object-recommendation]
primary_tag: topic>machine-learning
author_name: Juliana Morais
author_profile: https://github.com/Juliana-Morais
---

## Prerequisites
- You have created a trial account on SAP BTP: [Get a Free Account on SAP BTP Trial](hcp-create-trial-account)
- You have a subaccount and dev space with **Europe (Frankfurt)** as region: [Manage Entitlements on SAP BTP Trial](cp-trial-entitlements). See also [Create a Subaccount](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/261ba9ca868f469baf64c22257324a75.html).

## Details
### You will learn
  - How to check your Invoice Object Recommendation entitlements
  - How to create a service instance of Invoice Object Recommendation
  - How to create a service key for your service instance
---

[ACCORDION-BEGIN [Step 1: ](Go To Your Trial Account)]

1. In your web browser, open the [SAP BTP Trial cockpit](https://cockpit.hanatrial.ondemand.com/).

2. Navigate to the trial global account by clicking **Go To Your Trial Account**.

    !![Trial global account](png-files/01_Foundation20Onboarding_Home.png)

    >If this is your first time accessing your trial account, you'll have to configure your account by choosing a region. **Please select Europe (Frankfurt)**. Your user profile will be set up for you automatically.

    >Wait till your account is set up and ready to go. Your global account, your subaccount, your organization, and your space are launched. This may take a couple of minutes.

    >Choose **Continue**.

    >!![Account setup](png-files/02_Foundation20Onboarding_Processing.png)

3. From your global account page, choose the `trial` tile to access your subaccount.

    !![Subaccounts](png-files/enter-trial-account.png)

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 2: ](Check entitlements)]

To try out Invoice Object Recommendation, you need to make sure that your subaccount is properly configured.

1. On the navigation side bar, click **Entitlements** to see a list of all eligible services. You are entitled to use every service in this list according to the assigned service plan.

2. Search for **Invoice Object Recommendation Trial**.

    If you find the service in the list, you are entitled to use it. Now you can set this step to **Done** and proceed with Step 3.

    !![Entitlements](png-files/check-entitlements.png)

>**Only if you do not find the service in your list, proceed as follows:**

>1. Click **Configure Entitlements**.

>     !![Configure Entitlements](png-files/configure-entitlements.png)

>2. Click **Add Service Plans**.

>     !![Add Service Plan](png-files/add-service-plans.png)

>3. Select **Invoice Object Recommendation Trial**, and choose the **standard** service plan. Click **Add 1 Service Plan**.

>     !![Add Service Plan](png-files/add-entitlements.png)

>4. **Save** your **Entitlements** changes.

>     !![Add Service Plan](png-files/save-entitlements.png)    

>You are now entitled to use Invoice Object Recommendation and create instances of the service.

>For more details on how to configure entitlements, quotas, subaccounts and service plans on SAP BTP Trial, see [Manage Entitlements on SAP BTP Trial](cp-trial-entitlements).

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 3: ](Access service via Service Marketplace)]

The **Service Marketplace** is where you find all the services available on SAP BTP.

1. To access it, click **Service Marketplace** on the navigation side bar.

    ![Service Marketplace](png-files/access-service-marketplace.png)

2. Next, search for **Invoice Object Recommendation** and click the tile to access the service.

    !![Invoice Object Recommendation in Service Marketplace](png-files/access-ior.png)

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 4: ](Create service instance)]

You will now create an instance of your service.

Click **Create Instance** to start the creation dialog.

!![Service Instance](png-files/create-instance.png)

In the dialog, leave the default value for the service and the service plan. Enter a name for your new instance, for example, `ior-inst` and click **Create Instance**.

!![Create Instance](png-files/create-instance-dialog.png)

In the following dialog, click on **View Instance** to be navigated to the list of your service instances.

![View Instances](png-files/view-instances.png)

You have successfully created a service instance for Invoice Object Recommendation.

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 5: ](Create service key)]

You are now able to create a service key for your new service instance. Service keys are used to generate credentials to enable apps to access and communicate with the service instance.

  1. Click the navigation arrow to open the details of your service instance. Then, click the dots to open the menu and select **Create Service Key**.

      !![Service Key](png-files/create-service-keys.png)

  2. In the dialog, enter `ior-key` as the name of your service key. Click **Create** to create the service key.

      ![Create Service Key](png-files/create-service-key-name.png)

You have successfully created a service key for your service instance. You can now view the service key in the browser or download it.

!![View Service Key](png-files/view-service-key.png)

You will need the service key values to create your `access_token` in the next tutorial: [Get OAuth Access Token for Invoice Object Recommendation Using Any Web Browser](cp-aibus-ior-web-oauth-token).

[VALIDATE_1]
[ACCORDION-END]
