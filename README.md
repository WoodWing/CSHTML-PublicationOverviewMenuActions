# CSHTML-PublicationOverviewMenuActions



This script will help to convert old-style (CS9 and older) ContentStation `<PublicationOverviewActions>` 
   to CS10 `Publication-Overview` actions.
   
#### Documentation / sample code for other actions
The functionality of this script is based on the SDK documentation `sdk/po-ui-sdk.md` and the sample code in `sdk/samples/po-ui-sdk-sample.js`
   
The actions added to the Publication-overview menu can be found under the Publication-Overview menu (three dots)
 
#### Use old-definitions from WWsettings.xml
The old defintion for CS9 is located in wwsettings.xml, in the `<PublicationOverviewActions>` section.

   
a wwsetting line looks like:
`<PublicationOverviewAction tooltip="PurplePublish"  icon="{SERVER_URL}config/plugins/PurplePublish/images/purple-logo.png" url="{SERVER_URL}config/plugins/PurplePublish/purplePublish.php?ticket={SESSION_ID}&brand={BRAND_ID}&issue={ISSUE_ID}&edition={EDITION_ID}&category={CATEGORY_ID}&status={STATUS_ID}" displayMode="external"/>`

The lines from that section can be converted to the new defintion by making some small changes.
        	    
*    replace:  `'<PublicationOverviewAction'` with '{'
*   replace:  ending '/>' with '}'
*   replace:  'tooltip=' with 'label:'
*   replace: the '=' behind each field with a ':'
   add a comma between each field
*   replace &amp; with &	

The line above will then look like:

`{ label:"PurplePublish",  icon:"{SERVER_URL}config/plugins/PurplePublish/images/purple-logo.png", url:"{SERVER_URL}config/plugins/PurplePublish/purplePublish.php?ticket={SESSION_ID}&brand={BRAND_ID}&issue={ISSUE_ID}&edition={EDITION_ID}&category={CATEGORY_ID}&status={STATUS_ID}", displayMode:"external" }`  

	

## menu list definition
The  menu list needs to contain definitions with the following structure
   '{ label: '' , icon: '', url:'', displayMode:'', subMenu: ''}'
   
where:
 
*   label -> the text in the Menu
*   icon  -> the icon that will show in front of the label
*   url   -> the path to the server call. 
*   displayMode -> use one of the following strings:

		'external' open in new window
		'internal' open in same window
		'dialog' open in popup	
		'info'   show simple dialog with close
		'silent' will not show any result
   				
		- html pages using POST/GET will need to use 'external'
		- html/javascript pages that use ajax can use internal or dialog
*   subMenu	 -> if set, this action will be under the specified submenu
   
  
The URL defined in the actionList can contain placeholders which will be replaced on execution time:

*    {SERVER_URL}	will be replaced with the serverURL of the Enterprise Server 
*    {SESSION_ID}	will be replaced with the active ticket
*    {BRAND_ID} 	will be replaced with the filter value of the brand
*    {ISSUE_ID}	will be replaced with the filter value of the issue
*    {EDITION_ID}	will be replaced with the filter value of the edition
*    {CATEGORY_ID}	will be replaced with the filter value of the category
*    {STATUS_ID}	will be replaced with the filter value of the status


