# Fiddler To Load Impact k6 script
Export Fiddler recordings to Load Impact k6 script

Adding a new handler in Fiddler.js

```js
 public static ContextAction("set Load Impact Group Name")
    function DoSetLIGroupName(oSessions: Session[]) {
        if (oSessions == null) 
        {
            MessageBox.Show("Please select session(s) to set LI Group Name for", "No action");
            return;
        }
        
        var sString: String = FiddlerObject.prompt("LI Group Name", "", "LI Group Name");
        
        for (var x:int = 0; x < oSessions.Length; x++) 
        {
            oSessions[x]["addon.loadimpact.ligroup"] = sString;
        }
        
        FiddlerApplication.UI.RefreshRange(oSessions);
    }
```

Adds a new context menu option to set the LI Group Name value to group requests as named groups when exporting to Load Impact script.

It uses the new o-flag value "addon.loadimpact.ligroup" which is used in the exporter to get the Load Impact group name.

But there has to be a column to hold the value as well. That is defined inside the Main function.

```js
FiddlerObject.UI.lvSessions.AddBoundColumn("LI Group", 512, "addon.loadimpact.ligroup");
```

This adds a named column, "LI Group", of size 512 characters and with the o-flag "addon.loadimpact.ligroup". Both the o-flag value and the column name are used in the exporter so don't change them unless you really know what you're doing and update the exporter code as well.

Oh, and where is Fidller you might wonder?  [Fiddler](http://www.telerik.com/fiddler)

