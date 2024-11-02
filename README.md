# ForEach Plugin

# Description
Budibase ForEach plugin.

Find out more about [Budibase](https://github.com/Budibase/budibase).

This plugin can be used to run actions on every row of a dataprovider. You could also leverage the plugin to execute actions on binding changes.


## Instructions

Install the plugin and add the component to your application. The component requires a "row number" binding and an event to trigger when this "row number" changes. The event handler will fire on every change of the "row number" binding, except if the "row number" binding is not parseable as a number or parses to a negative number. If the dataprovider binding is set, the event handler will also receive the object from the dataprovider at the selected row. The plugin also exposes the current "row number" and the current row data (If dataprovider is set) as context variables if you want to track the status.

### ForEach Flow
To implement a full "ForEach", the following is the recommended implementation:
 - Bind a *selectedRow* state variable to the **Next Line Number** setting.
 - Bind your data provider to the **Data Provider** setting.
 - Add the following actions to the **Event** setting:
     1. ...Some custom action
     2. Set the *selectedRow* state variable to the following binding `{{ add Line Number 1 }}`
     3. Note: If you do not have a dataprovider set, you will need to conditionally skip the above step yourself.
