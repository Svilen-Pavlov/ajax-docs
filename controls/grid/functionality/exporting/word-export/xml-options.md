---
title: XML Options
page_title: XML Options for Word Format (HTML-Based) - RadGrid
description: Check our Web Forms article about Word Format (HTML-Based).
slug: grid/functionality/exporting/word-export/xml-options
previous_url: controls/grid/functionality/exporting/export-formats/word-and-excel-export/word-format-(html-based)
tags: word,format,(html-based)
published: false
position: 2
---

# XML Options for HTML-Based (DOC)

## Styles / Appearance

**Microsoft Word 2003** displays grid lines by default. These lines just shows where the table/cell/row borders are. If you want to remove them, you should choose **Table>>Show Gridlines** (uncheck this option).

## XML Options

**XmlOptions** property allows you to set different options of the exported file. The XML element contains one or more sub-elements. These include **DocumentProperties** which is valid for Word and Excel, **WordDocument** which can be used when exporting to Word, and finally **ExcelWorkbook** which applies to Microsoft Excel.

A list of the supported WordDocument values is represented below.


| WordDocument | Represents |
| ------ | ------ |
|\<w:View\> \</w:View\>|This element may contain one of the following values: **MasterPages**, **Normal**, **Print**, **Web** (default)|
|\<w:Zoom\> \</w:Zoom\>|This element may contain one of the following values: **A numerical value between 1 and 500** - this value represents the zoom percentage. The default value is 100; **BestFit** - zoom to page width. Only available in print layout view; **FullPage** - zoom to whole page. Only available in print layout view; **TextFit** - Zoom to text width. Only available in print layout view.|
|\<w:HideSpellingErrors/\>|If this property is specified, the document's spelling errors are hidden.|
|\<w:HideGrammaticalErrors/\>|If this property is specified, the document's grammatical errors are hidden.|

Example:



````C#
protected void RadGrid1_HTMLExporting(object sender, GridHTMLExportingEventArgs e)
{
    e.XmlOptions = @"<xml>
                        <w:WordDocument>
                            <w:HideSpellingErrors/>
                            <w:View>Print</w:View>
                        </w:WordDocument>
                     </xml>";
}
````
````VB	
Protected Sub RadGrid1_HTMLExporting(sender As Object, e As GridHTMLExportingEventArgs)
    e.XmlOptions = "<xml><w:WordDocument><w:HideSpellingErrors/><w:View>Print</w:View></w:WordDocument></xml>"
End Sub	
````

