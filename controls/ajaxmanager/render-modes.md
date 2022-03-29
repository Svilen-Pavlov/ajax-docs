---
title: Render Modes
page_title: AjaxManager Render Modes
description: 
slug: ajaxmanager/appearance-and-styling/render-modes
previous_url: ajax/appearance-and-styling/render-modes, controls/ajaxmanager/appearance-and-styling/render-modes
tags: telerik, aspnet, ajax, ajaxmanager, render, modes
published: True
position: 7
---

# Render Modes



## 

No matter which control you would chose, the updated via AJAX controls would render in a HTML DIV tag which displays, by default, as a block element.In order to change this behaviour, RadAjax exposes three properties that you can set: UpdatePanelsRenderMode, UpdatePanelRenderMode and RenderMode.

**UpdatePanelsRenderMode** - You can set this property to the RadAjaxManager itself to control the render mode for all AJAX-enabled controls. UpdatePanelsRenderMode has two possible values: Block (the default value) and Inline. Example 1 shows setting the UpdatePanelsRenderMode value to Inline.

````ASP.NET
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server" UpdatePanelsRenderMode="Inline">
	<AjaxSettings>
	    <telerik:AjaxSetting AjaxControlID="Button1">
	        <UpdatedControls>
	         <telerik:AjaxUpdatedControl ControlID="Label1" />
	         <telerik:AjaxUpdatedControl ControlID="Label2" />
	        </UpdatedControls>
	    </telerik:AjaxSetting>
	</AjaxSettings>
</telerik:RadAjaxManager>
````



**UpdatePanelRenderMode** - You can set this property for a particular AjaxUpdatedControl setting in the RadAjaxManager. Its default value is Block. You can change it to Inline as shown in Example 2.

````ASP.NET
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
	<AjaxSettings>
	    telerik:AjaxSetting AjaxControlID="Button1">
	        <UpdatedControls>
	                <telerik:AjaxUpdatedControl ControlID="Label1" UpdatePanelRenderMode="Inline" />
	                telerik:AjaxUpdatedControl ControlID="Label2" />
	        </UpdatedControls>
	    </telerik:AjaxSetting>
	</AjaxSettings>
</telerik:RadAjaxManager>
````



**RenderMode** - You can change the render mode of controls wrapped in RadAjaxPanel control by setting its RenderMode property to Inline (see Example 3) or Block (the default value).

````ASP.NET
<telerik:RadAjaxPanel ID="RadAjaxPanel1" runat="server" RenderMode="Inline">
	 <asp:Button ID="Button1" runat="server" Text="AJAX" />
	 <asp:Label ID="Label1" runat="server" Text="Label1" />
</telerik:RadAjaxPanel>
````



>caution If one updated control has several initiators and is present in several places in the AjaxSettings,then setting UpdatePanelRenderMode="Inline" at one place will guarantee that the final render mode of the generated update panel is "Inline". The only way to override this is at runtime in AjaxSettingCreated:
>




````C#
	
protected void RadAjaxManager1_AjaxSettingCreated(object sender, AjaxSettingCreatedEventArgs e)
	{
	    if (e.Updated.ID == "Label1")
	    e.UpdatePanel.RenderMode = UpdatePanelRenderMode.Block;
	}  
				
````
````VB.NET
Protected Sub RadAjaxManager1_AjaxSettingCreated(ByVal sender As Object, ByVal e As AjaxSettingCreatedEventArgs)
	If e.Updated.ID = "Label1" Then
	    e.UpdatePanel.RenderMode = UpdatePanelRenderMode.Block
	End If
End Sub
	
````


>caution Note that the following scenario is currently unsupported (including the properties for both the RadAjaxManager and per AjaxUpdatedControl):
>


````ASP.NET
<telerik:RadAjaxManager ID="RadAjaxManager1" runat="server" UpdatePanelsRenderMode="Inline">
	<AjaxSettings>
	    <telerik:AjaxSetting AjaxControlID="Button1">
	        <UpdatedControls>
	            <telerik:AjaxUpdatedControl ControlID="Label1" UpdatePanelRenderMode="Block" />
	            <telerik:AjaxUpdatedControl ControlID="Label2" />
	        </UpdatedControls>
	    </telerik:AjaxSetting>
	 </AjaxSettings>
</telerik:RadAjaxManager>
````


