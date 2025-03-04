---
title: Implement a Business Add-in (BAdI) To Check a Purchase Requisition
description: Define and implement a developer extension (BAdI), which performs checks during creation of a purchase requisition item.
auto_validation: true
time: 30
tags: [ tutorial>intermediate, products>sap-btp--abap-environment]
primary_tag: topic>abap-development
author_name: Julie Plummer
author_profile: https://github.com/julieplummer20

---

## Prerequisites
- **IMPORTANT**: It is essential that you are a member of SAP Early Adopter program
- You have a license for SAP S/4HANA Cloud and have a developer user in this system
- You have installed SAP ABAP Development Tools (ADT), version 3.16 or later, and have created an ABAP Cloud project for your SAP S/4HANA Cloud System in it
- You are familiar with the concept of extensions to the SAP standard and with `BAdIs` in particular. If not, see the **More Information** section at the end of this tutorial
- To test the `BAdI`: In SAP Fiori launchpad, you have the authorization for the app **Process Purchase Requisitions - Professional**, i.e. **`SAP_BR_PURCHASER`**


## Details
### You will learn  
- How to log on to SAP S/4HANA Cloud ABAP Environment
- How to create an ABAP package
- How to find relevant existing `BAdI` enhancement spots for your line of business, in this case **Materials-Management-Purchasing**
- How to implement checks for the field quantity and delivery date during creation of purchase requisition item

### Defining and implementing the enhancement: Overview
A **Business Add-In (`BAdI`)** enables you to implement enhancements to standard SAP applications with out modifying the original code.

In this case, the `BAdI` is implemented in the SAP Fiori app as follows:

1. Use an existing enhancement spot **`MM_PUR_S4_PR`**, with an existing `BADI` definition **`MM_PUR_S4_PR_CHECK`**
2. Create a container ( **enhancement implementation** ) in the enhancement spot
3. Create a **`BADI` implementation** for the `BADI` definition.

### At runtime:
1. The user creates a purchase requisition.
2. The enhancement checks:
    - the quantity of items ordered is **10 or fewer**
    - the date is **180 days or less in advance**
3. If not, the application returns an error.

The application will look roughly like this:

!![step0-app-overview](step0-app-overview.png)
.

!![step0-app-w-badi](step0-app-w-badi.png)


Throughout this tutorial, objects name include a prefix, such as **`xx`** or suffix, such as **`XXX`**. Always replace this with your group number or initials.

---


[ACCORDION-BEGIN [Step 1: ](Log on to SAP S/4HANA Cloud ABAP Environment)]
1. Open ADT, select **File** > **New** > **Other**.

    ![logon](logon.png)

2. Search **ABAP Cloud Project**, select it and choose **Next >**.

    ![logon](logon2.png)

3. Select **SAP S/4HANA Cloud ABAP Environment**, enter the ABAP service instance URL and choose **Next**.

    ![logon](logon3.png)

4. To log on, choose **Open Logon Page in Browser**, then choose **Next**. (Alternatively, e.g. if you have an admin user and a developer user in the SAP BTP Cloud landscape, you may need to choose **Copy Logon URL...** .)

    ![logon](logon4.png)

    ![logon](logon5.png)

5. Check your ABAP service instance connection and choose **Finish**.

    ![logon](logon6.png)

Your project is available in the Project Explorer.

![logon](logon7.png)

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 2: ](Create package)]
First, create a package for your development objects.

1. Choose your project, then choose **New > ABAP Package** from the context menu.

    !![step1a-package-new](step1a-package-new.png)

2. Enter the following.
    - **`Zxx_MM_PUR_S4_BADI`**
    - **`BADIs` for MM Purchasing**

3. Choose **Add to favorite packages**, then choose **Next**

    !![step1b-package-name](step1b-package-name.png)

4. Choose **Create a new request**, enter a meaningful description, e.g. **Test `BADIs` MM-PURCHASING** then choose **Finish**.

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 3: ](Choose enhancement spot)]
1. First make sure that the released APIs are displayed by application component: In your project, navigate to **Released Objects**.The tree should show the Released Objects sorted by Application Component.

    !![step2b-released-objects](step2b-released-objects.png)

2. If not, choose **Configure Tree** from the context menu, then select **Application Component** from the left side ( **Available Tree Levels** ) and add it to the right side ( **Selected Tree Levels** ). Move it to the top. Then choose **Finish**.


    !![step2a-tree-configure](step2a-tree-configure.png)
    .
    !![step2b-application-component-add](step2b-application-component-add.png)

3. In the tree, drill down to **MM-PUR-REQ > Enhancements > Enhancement Spots > `MM_PUR_S4_PR`** and open it by double-clicking.

    !![step2c-enhancement-spot-choose](step2c-enhancement-spot-choose.png)

The `BAdI` enhancement spot appears in a new editor, showing you the available `BAdI` definitions (1).

To help you create your own enhancements, example classes are provided (2).

!![step2d-enhancement-spot-editor](step2d-enhancement-spot-editor.png)    

[DONE]
[ACCORDION-END]


[ACCORDION-BEGIN [Step 4: ](Create enhancement implementation)]
Now that you have identified the correct enhancement spot, you need a container within this enhancement spot for your `BADI` implementations. This is known as an enhancement implementation.

1. Select your package **`Zxx_MM_PUR_S4_BADI`** and choose **New > Other ABAP Object** from the context menu.

    !![step3a-badi-implem-create](step3a-badi-implem-create.png)

2. Filter by `BAdI`, choose **`BAdI` Enhancement Implementation**, then choose **Next**.

3. Add the following and choose **Next**.
    - Name: **`Zxx_BADI_CHECK_PURCH_REQ`**
    - Description: **Check date and quantity in Purchase Requisition**
    - Enhancement Spot: **`MM_PUR_S4_PR`**

    !![step3b-badi-enhancement-implem](step3b-badi-enhancement-implem.png)

4. Choose the transport request, then choose **Finish**.

Your `BAdI` enhancement implementation appears in a new editor. It implements the enhancement spot **`MM_PUR_S4_PR`**.

!![step3c-BAdi-enh-impl-editor](step3c-BAdi-enh-impl-editor.png)

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 5: ](Add `BAdI` Implementation)]
1. Choose **Add `BAdI`**.

    !![step4a-badi-enh-implem-add](step4a-badi-enh-implem-add.png)

2. Add the following, then choose **Next**:
    - `BAdI` Definition: **`MM_PUR_S4_PR_CHECK`** (Add by clicking on **Browse**)
    - `BAdI` Implementation Name: **`ZXX_IMPL_CHECK_PURCH_REQ`**

    !![step5b-badi-input-values](step5b-badi-input-values.png)

Ignore the error. You will fix this in the next step.

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 6: ](Create implementing class)]
1. Choose **Implementing Class**.

    !![step5a-implementing-class-create](step5a-implementing-class-create.png)

2. Add the following, then choose **Next**.
    - Name: **`ZCL_CHECK_PURCH_REQ_XXX`**
    - Description: **Implement checks on creating Purchase Requisition**
    - (Added automatically): Interfaces: **`IF_MM_PUR_S4_PR_CHECK`**

    !![step5b-implementing-class-name](step5b-implementing-class-name.png)

3. Choose the transport request, then choose **Finish**.

    The class appears in a new editor with skeleton code.

    !![step5c-class-editor](step5c-class-editor.png)

4. Format, save, and activate the class ( **`Shift+F1, Ctrl+S, Ctrl+F3`** ).

5. Go back to your `BAdI` implementation **`ZXX_IMPL_CHECK_PURCH_REQ`** and activate it too.

The error will disappear.

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 7: ](Implement code)]
1. Add the following code to the method implementation **`if_mm_pur_s4_pr_check~check.`**.

    ```ABAP
    DATA ls_message TYPE mmpur_s_messages.
    **
    READ TABLE  purchaserequisitionitem_table  INTO DATA(ls_pur_req_itm) INDEX 1    .

    IF ls_pur_req_itm-orderedquantity > 10.
      ls_message-messageid = 'DUMMY'.
      ls_message-messagetype = 'E'.
      ls_message-messagenumber = '001'.
      ls_message-messagevariable1 = ' Quantity limit 10'.           "Place holder
      APPEND ls_message TO messages.

    ENDIF.

    IF ls_pur_req_itm-deliverydate - ( cl_abap_context_info=>get_system_date( ) ) > 180.
      ls_message-messageid = 'DUMMY'.
      ls_message-messagetype = 'E'.
      ls_message-messagenumber = '001'.
      ls_message-messagevariable1 = 'Delivery date limit 180 days '.           "Place holder
      APPEND ls_message TO messages.

    ENDIF.

    ```

2. Format, save, and activate ( **`Shift+F1, Ctrl+S, Ctrl+F3`** ) your code.

Check that yours is the implementation that will be called:

!![step5d-impl-called](step5d-impl-called.png)

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 8: ](Test BAdI)]
Now test that the checks are performed in the app.

1. In SAP Fiori launchpad, open the app **Process Purchase Requisitions (Professional)**.

    !![step7a-app-open](step7a-app-open.png)

2. Display the existing purchase requisitions by choosing **Go**, then choose **Create**.

    !![step7b-go](step7b-go.png)

3. In the next screen, choose **Create** again, then choose **Material**.

    !![step7c-create-material](step7c-create-material.png)

4. The Details screen appears. From the **Material** field, choose **Value Help**.

5. Then choose the material **RM122**, **Plant 1010**.

    !![step7e-material-rm122-choose](step7e-material-rm122-choose.png)

6. The system fills some fields with default values. Now enter a wrong quantity, e.g. **20**, and date, e.g. **09.11.2021**.

    !![step7f-wrong-date-and-quantity](step7f-wrong-date-and-quantity.png)

7. The system shows you 2 errors. To display the errors, select the red box at the bottom left.

    !![step7g-errors](step7g-errors.png)

8. Enter correct values, choose **Apply**, then choose **Save**.

Your new order appears in the Overview List.
.

!![step7h-new-order](step7h-new-order.png)

[DONE]
[ACCORDION-END]

[ACCORDION-BEGIN [Step 9: ](Test yourself)]

[VALIDATE_1]
[ACCORDION-END]

---

### More Information
- Start here: SAP blog post: [How to Extend SAP Standard Using ADT](https://blogs.sap.com/2020/08/05/how-to-extend-sap-standard-using-adt/)
- SAP Help Portal: [Working with Business Add-Ins (`BAdIs`)](https://help.sap.com/viewer/5371047f1273405bb46725a417f95433/Cloud/en-US/04a1d9415efd4e4fbc58534c99c3a0d3.html)
- SAP Help Portal: Sourcing and Procurement: [Adaptation of App Behavior (Overview and List of Available `BAdIs`)](https://help.sap.com/viewer/DRAFT/0e602d466b99490187fcbb30d1dc897c/2111.500/en-US/259a396e6bdb4d08b130049880a3920f.html)


---
