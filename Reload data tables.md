# Reload spotfire tables

## IronPython Script
``` python
# Reload all data in all tables
Document.Data.Tables.ReloadAllData()

# Reload only linked data in all tables
Document.Data.Tables.ReloadLinkedData()

# Reload all data in a specific table
Document.Data.Tables["table1"].ReloadAllData()

# Reload only linked data in a specific table
Document.Data.Tables["table1"].ReloadLinkedData()
```

## HTML
Hidden button that activates python script
``` html
<!-- Hidden button used to trigger IronPython via JQuery -->
<DIV id="reloadtables" style="display:none;">
	<SpotfireControl id="9ea5053eb5aa4f11bc0068df1abd4929" />
</DIV>
```

## Javascript
``` javascript
$("Document").ready(function() {
		
	clicker = function() {
		// Spotfire button click to fire iron python
		console.log("Clicking... " + Date.now());
		$("#reloadtables input").click()
	}

	// Check for and clear any previous intervals in memory
	// If you don't do this, the intervals stack on each tab change(!)
	var lastMainInterval = localStorage.getItem('lastMainInterval');

	if (lastMainInterval != null) {
		console.log("Clearing last lastMainInterval: " + lastMainInterval);
		clearInterval(lastMainInterval); // Tidy up
	}

	// Click button that fires spotfire scripts every 60s
	var mainInterval = setInterval(function(){  clicker(); },60000);
	
	// Remember the interval Id
	localStorage.setItem('lastMainInterval',mainInterval);

});
```
