---
title: Overview
page_title: AjaxManager Overview 
description: 
slug: ajaxmanager/overview
previous_url: ajax/radajaxmanager/overview
tags: telerik, aspnet, ajax, ajaxmanager, overview
published: True
position: 0
---

# AjaxManager Overview


The AjaxManager enables you to rapidly configure practical and complex AJAX solutions in your project.

The following image shows an AjaxManager in action with applied Grid paging and an AjaxLoadingPanel for visual indication.

![RadAjaxManager in Action](images/AJAXinAction.gif)


## Main Features

* **Availibility** - You can AJAX-enable all controls that normally work with postbacks. 

* **Design-time UI support** - It lets you define visually and codeless (in Visual Studio design-time) which controls should initiate AJAX requests and which controls should be updated.

* **Convenience** - You do not need to modify your application logic.

* **Practicality** - You can update a number of page elements at once regardless of their position on the page.

* **Efficiency** - You do not need to write any JavaScript or invoke AJAX requests manually.

Using a single **RadAjaxManager** on the page you can create complex web applications, such as Microsoft Outlook® Web Access portal:

[Telerik Web Mail Demo](https://demos.telerik.com/aspnet-ajax/webmail/)

## Quick Example

Here is an example you can simply copy-paste to your project to see the prowess of AJAX:  
```ASP.NET
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
    <AjaxSettings>
        <telerik:AjaxSetting AjaxControlID="RadButton1">
            <UpdatedControls>
                <telerik:AjaxUpdatedControl ControlID="RadLabel1" />
            </UpdatedControls>
        </telerik:AjaxSetting>
    </AjaxSettings>
</telerik:RadAjaxManager>
<telerik:RadButton ID="RadButton1" runat="server" Text="With AJAX"
    OnClick="RadButton1_Click">
</telerik:RadButton>
<telerik:RadLabel ID="RadLabel1" runat="server">Output 1</telerik:RadLabel>
<br />
<telerik:RadButton ID="RadButton2" runat="server" Text="Without AJAX"
    OnClick="RadButton2_Click">
</telerik:RadButton>
<br />
<telerik:RadLabel ID="RadLabel2" runat="server">Output 2</telerik:RadLabel>
```
```C#
protected void RadButton1_Click(object sender, EventArgs e)
{
    RadLabel1.Text = "Success";
}
protected void RadButton2_Click(object sender, EventArgs e)
{
    RadLabel2.Text = "Success";
}
```
```VB
Protected Sub RadButton1_Click(ByVasender As Object, ByVal e As EventArgs)
    RadLabel1.Text = "Success"
End Sub
Protected Sub RadButton2_Click(ByVasender As Object, ByVal e As EventArgs)
    RadLabel2.Text = "Success"
End Sub
```



## Using in Projects

In order to use **RadAjaxManager**, it is sufficient to just drag it from the **Visual Studio** toolbox to your page.

>note It is sufficient to have just one **RadAjaxManager** in a single page.
>

If you are using MasterPage or WebUserControl scenario, the best option is to use a single **RadAjaxManager** on the master/main page and have a **RadAjaxManagerProxy** control on the content/ascx pages: 
* [RadAjaxManagerProxy Overview]({%slug ajaxmanager/radajaxmanagerproxy/overview%})
* [RadAjax and MasterPage]({%slug ajaxmanager/how-to/radajax-and-masterpage%})
* [RadAjax and WebUserControls]({%slug ajaxmanager/how-to/radajax-and-webusercontrols%})

>caution It is a nice practice to implement AJAX last in your app. The reason behind this is that [AJAX tends to hide server and client-side errors](https://www.telerik.com/support/kb/aspnet-ajax/ajaxmanager/details/get-more-descriptive-errors-by-disabling-ajax).
>

## Capabilities

The visual designer of **RadAjaxManager** , accessible in Visual Studio, lets you set even the most complicated update scenarios such as the one shown in **Figure 2** :

![Update schema](images/ControlsUpdate.png)

**Figure 2** - Example of scenario with Ajax-enabled controls

1. Single control updates one or more controls with an AJAX request – **1** updates **2** and **3**

2. Second control updates other controls (or even controls from the previous scenario) with an AJAX request – **3** updates **2** and **5**

3. A control updates itself with an AJAX request – **6** updates **6** (i.e., itself)

4. Call the **RadAjaxManager** API from a control on the page and update control(s) on the page. – Using the **RadAjaxManager** API, **2** is made to update **1** and **4** .

## Parent-Child Control Configuration

It is not possible to have child elements to be the AjaxSetting initiator and update their parent container element. If you add a container or parent control to be updated, it is mandatory to also add it itself or some external control to be the initiator. You can imagine it like placing a telerik:RadAjaxPanel or asp:UpdatePanel on the page - it will affect only things inside this panel. RadAjaxManager is similar, but just achieves this behind the curtains.


## See Also
 * [Getting Started - What is AJAX?]({%slug ajaxmanager/getting-started/what-is-ajax%})

 * [First Steps with UI for ASP.NET AJAX]({%slug introduction/installation/installing-the-telerik-controls-from-msi-file%})

 * [RadAjaxManagerProxy Overview]({%slug ajaxmanager/radajaxmanagerproxy/overview%})

 * [RadAjaxManager Client-side programming Overview]({%slug ajaxmanager/client-side-programming/overview%})
 
 * [Controls Wrapped in AjaxPanel and Added to AjaxManager Settings]({%slug ajaxmanager/troubleshooting/controls-wrapped-in-ajaxpanel-and-added-to-ajaxmanager-settings%})
 
 * [RadAjaxManager Overview demo](https://demos.telerik.com/aspnet-ajax/ajaxmanager/overview/defaultcs.aspx)

