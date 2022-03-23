---
title: Ajaxify Particular Templated GridView Buttons with AjaxManager
page_title: Ajaxify Particular Templated GridView Buttons with AjaxManager
description: "Learn how to ajaxify particular templated GridView buttons with the AjaxManager."
slug: ajaxmanager/how-to/ajaxify-particular-templated-gridview-buttons
previous_url: ajax/radajaxmanager/how-to/ajaxify-particular-templated-gridview-buttons, controls/ajaxmanager/how-to/ajaxify-particular-templated-gridview-buttons
tags: telerik, asp, net, ajax, manager, ajaxify, particular, templated, gridview, buttons
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

How can I ajaxify specific controls, residing in the template column of the GridView control, to update other controls, for example, outside of the GridView, without a postback? 

## Solution 

To achieve the desired scenario, ajaxify the whole GridView. 


````ASP.NET
<asp:ScriptManager ID="ScriptManager" runat="server" />
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
	<AjaxSettings>
	    <telerik:AjaxSetting AjaxControlID="GridView1">
	        <UpdatedControls>
	            <telerik:AjaxUpdatedControl ControlID="GridView1" />
	            <telerik:AjaxUpdatedControl ControlID="TextBox" />
	        </UpdatedControls>
	    </telerik:AjaxSetting>
	</AjaxSettings>
</telerik:RadAjaxManager>
````





However, you may need another column to make regular postbacks or even the rest of the actions to trigger standard postback requests.

This is when the RadAjaxManager comes into place. You can add the manager settings programmatically and specify each particular control which you want to ajaxify or update. The essential part is to attach the appropriate event or events in which to apply the Ajax settings. For the GridView in this scenario, the proper place is the `Row_PreRender` event handler.

The GridView in the sample contains one template and one button column. The `ImageButtons` in the template column are ajaxified by the AjaxManager and the buttons in the `ButtonField` start regular postbacks. Both the image and the push buttons update the text box outside of the GridView.





````ASP.NET
<asp:TextBox ID="TextBox1" runat="server" Width="400px" Text="not updated"></asp:TextBox>
<asp:ScriptManager ID="ScriptManager" runat="server" />
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
</telerik:RadAjaxManager>
<asp:GridView ID="GridView1" DataSourceID="AccessDataSource1" AllowPaging="true"
	        runat="server">
	        <Columns>
	            <asp:TemplateField HeaderText="TemplateField">
	                <ItemTemplate>
	                    <asp:ImageButton ID="ImageButton1" CommandName="MyCommand" CommandArgument='<%# Eval("CustomerID") %>'
	                        ImageUrl="arrow.gif" runat="server" />
	                </ItemTemplate>
	            </asp:TemplateField>
	            <asp:ButtonField ButtonType="Button" HeaderText="ButtonField" CommandName="Test"
	                Text="Button" ImageUrl="arrow.gif" />
	        </Columns>
</asp:GridView>
<asp:AccessDataSource ID="AccessDataSource1" DataFile="~/Grid/Data/Access/Nwind.mdb"
	runat="server" SelectCommand="SELECT * FROM [Customers]"></asp:AccessDataSource>
````
````C#
	
protected void GridView1_RowCreated(object sender, System.Web.UI.WebControls.GridViewRowEventArgs e)
{
	if (e.Row.RowType == DataControlRowType.DataRow)
	    {
	        e.Row.PreRender += new System.EventHandler(Row_PreRender);
	    }
}
	
protected void GridView1_RowCommand(object sender, System.Web.UI.WebControls.GridViewCommandEventArgs e)
{
	TextBox1.Text = string.Format("CommandName:{0}, CommandArgument:{1}", e.CommandName, e.CommandArgument);
}
	
protected void Row_PreRender(object sender, System.EventArgs e)
{
	ImageButton ImageButton1 = ((ImageButton)(((Control)(sender)).FindControl("ImageButton1")));
	RadAjaxManager1.AjaxSettings.AddAjaxSetting(ImageButton1, TextBox1);
}
				
````
````VB
Protected Sub GridView1_RowCreated(ByVal sender As Object, ByVal e As System.Web.UI.WebControls.GridViewRowEventArgs) Handles GridView1.RowCreated
	        If e.Row.RowType = DataControlRowType.DataRow Then
	            AddHandler e.Row.PreRender, AddressOf Row_PreRender
	        End If
End Sub
	
Protected Sub GridView1_RowCommand(ByVal sender As Object, ByVal e As System.Web.UI.WebControls.GridViewCommandEventArgs) Handles GridView1.RowCommand
	        TextBox1.Text = String.Format("CommandName:{0}, CommandArgument:{1}", e.CommandName, e.CommandArgument)
End Sub
	
Protected Sub Row_PreRender(ByVal sender As Object, ByVal e As System.EventArgs)
	        Dim ImageButton1 As ImageButton = CType(CType(sender, Control).FindControl("ImageButton1"), ImageButton)
	        RadAjaxManager1.AjaxSettings.AddAjaxSetting(ImageButton1, TextBox1)
End Sub
	
	
````


## See Also

* [Demo: Ajaxifying Particular Controls in the Template Column of the Grid with the AjaxManager](https://demos.telerik.com/aspnet-ajax/ajaxmanager/application-scenarios/partial-ajaxification/defaultcs.aspx)
