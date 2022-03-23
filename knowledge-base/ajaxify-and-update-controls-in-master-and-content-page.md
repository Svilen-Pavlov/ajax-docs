---
title: Ajaxify and Update Controls in Master and Content Page with the AjaxManager
page_title: Ajaxify and Update Controls in Master and Content Page with the AjaxManager
description: "Learn how to ajaxify and update controls in the master and content page with the AjaxManager."
slug: ajaxmanager/how-to/ajaxify-and-update-controls-in-master-and-content-page
previous_url: ajax/radajaxmanager/how-to/ajaxify-and-update-controls-in-master-and-content-page, controls/ajaxmanager/how-to/ajaxify-and-update-controls-in-master-and-content-page
tags: telerik, asp, net, ajax, manager, radajax, and, masterpage
published: True
type: how-to
category: knowledge-base
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® UI for ASP.NET AJAX AjaxManager</td>
		</tr>
	</tbody>
</table>

## Description

How can I enable AJAX and update every single control in my application with the AjaxManager in my `MasterPage`?

## Solution 

The following example shows how to achieve the desired scenario by adding the necessary AJAX settings programmatically. The sample application contains buttons in the master and content page. The two buttons update controls in the master and content page as well. 

>important * The initiator of the AJAX request (the first argument `AddAjaxSetting` receives) must be an `IPostBack` control. This means that the initiator must be a control that performs a postback on its own (like a button or a grid) and not a simple container (like an `<asp:Panel>` control). Containers do not invoke the request themselves and the AjaxManager cannot identify if the request comes from their children because the container ID is not present in the POST parameters.
>* Using a container like a `Panel` for an AJAX initiator can result in various issues like initiating full postbacks instead of AJAX requests, or an unexpected list of updated controls.


**Master Page**

````ASP.NET
<telerik:RadScriptManager ID="RadScriptManager1" runat="server">
</telerik:RadScriptManager>
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
    <AjaxSettings>
        <telerik:AjaxSetting AjaxControlID="btnDecrease">
            <UpdatedControls>
                <telerik:AjaxUpdatedControl ControlID="TextBox1" />
            </UpdatedControls>
        </telerik:AjaxSetting>
    </AjaxSettings>
</telerik:RadAjaxManager>
<asp:LinkButton ID="btnDecrease" runat="server" OnClick="btnDecrease_Click">Decrease</asp:LinkButton>
<asp:TextBox ID="TextBox1" runat="server">0</asp:TextBox>
<asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
</asp:ContentPlaceHolder>
````
````C#
protected void Page_Load(object sender, EventArgs e)
{
    Label Label1 = (Label)ContentPlaceHolder1.FindControl("Label1");
    RadAjaxManager1.AjaxSettings.AddAjaxSetting(btnDecrease, Label1);
}

protected void btnDecrease_Click(object sender, EventArgs e)
{
    Label Label1 = (Label)ContentPlaceHolder1.FindControl("Label1");
    Label1.Text = Int32.Parse(Label1.Text) - 1 + "";

    TextBox1.Text = Int32.Parse(TextBox1.Text) - 1 + "";
}
````
````VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
    Dim Label1 As Label = CType(ContentPlaceHolder1.FindControl("Label1"), Label)
    RadAjaxManager1.AjaxSettings.AddAjaxSetting(btnDecrease, Label1)
End Sub

Protected Sub btnDecrease_Click(ByVal sender As Object, ByVal e As EventArgs)
    Dim Label1 As Label = CType(ContentPlaceHolder1.FindControl("Label1"), Label)
    Label1.Text = Int32.Parse(Label1.Text) - 1 + ""

    TextBox1.Text = Int32.Parse(TextBox1.Text) - 1 + ""
End Sub 'btnDecrease_Click
````

**Content Page**

````ASP.NET
<asp:Content ID="Content1" ContentPlaceHolderID="ContentPlaceHolder1" runat="Server">
    <asp:Button ID="btnIncrease" runat="server" Text="Increase" OnClick="btnIncrease_Click" />
    <asp:Label ID="Label1" runat="server" Text="0"></asp:Label>
</asp:Content>
````
````C#
protected void Page_Load(object sender, EventArgs e)
{
    RadAjaxManager AjaxManager = RadAjaxManager.GetCurrent(Page);
    AjaxManager.AjaxSettings.AddAjaxSetting(btnIncrease, Label1);

    TextBox TextBox1 = (TextBox)this.Master.FindControl("TextBox1");
    AjaxManager.AjaxSettings.AddAjaxSetting(btnIncrease, TextBox1);
}

protected void btnIncrease_Click(object sender, EventArgs e)
{
    Label1.Text = Int32.Parse(Label1.Text) + 1 + "";

    TextBox TextBox1 = (TextBox)this.Master.FindControl("TextBox1");
    TextBox1.Text = Int32.Parse(TextBox1.Text) + 1 + "";
}
````
````VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
    Dim AjaxManager As RadAjaxManager = RadAjaxManager.GetCurrent(Page)
    AjaxManager.AjaxSettings.AddAjaxSetting(btnIncrease, Label1)

    Dim TextBox1 As TextBox = CType(Me.Master.FindControl("TextBox1"), TextBox)
    AjaxManager.AjaxSettings.AddAjaxSetting(btnIncrease, TextBox1)
End Sub 'Page_Load


Protected Sub btnIncrease_Click(ByVal sender As Object, ByVal e As EventArgs)
    Label1.Text = Int32.Parse(Label1.Text) + 1 + ""

    Dim TextBox1 As TextBox = CType(Me.Master.FindControl("TextBox1"), TextBox)
    TextBox1.Text = Int32.Parse(TextBox1.Text) + 1 + ""
End Sub 'btnIncrease_Click
````

