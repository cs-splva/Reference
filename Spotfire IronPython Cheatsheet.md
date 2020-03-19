# Spotfire IronPython Cheatsheet

A lot can also be found at:
* https://www.sf-ref.com/
* https://community.tibco.com/wiki/ironpython-scripting-tibco-spotfire

#### Get or set Document Property:
``` python
Document.Properties["FUTUREONLY"] = "myvalue"
```

#### Read the Screen Size of the users device
``` python
visualizationAreaSize=Document.ActivePageReference.GetVisualizationAreaSize()

print visualizationAreaSize.Width
print visualizationAreaSize.Height
```

#### Update HTML in text area
``` python
from Spotfire.Dxp.Application.Visuals import HtmlTextArea
vis = ta.As[HtmlTextArea]()
vis.HtmlContent = "<strong>Inserted text</strong>"
```

#### Limit data by expression
``` python
from Spotfire.Dxp.Application.Visuals import *
myVis = myVis.As[Visualization]()

myVis.Data.WhereClauseExpression = "[Quantity] > 0 and [Movement Type] = 'X13'"
```
#### Use color libraries to set correct colors per visual
``` python
from Spotfire.Dxp.Application.Visuals import *
from Spotfire.Dxp.Data import *

#Declacre visualizations
accuracyPies = accuracyPies.As[Visualization]()

accuracyKPI = accuracyKPI.As[Visualization]()
accuracyKPI = accuracyKPI.ActiveKpi

# Get document property - which column is selected
dp = Document.Properties["columnNameAccuracy"]

# List of columns in completeness
completeness = ["admi_start_date","admi_end_date","shrd_start_date","shin_start_date","teco_status_date","admo_start_date","admo_end_date","completion_date","hist_date"]
accuracy = ["cir_in_usable","admi_shrd_usable","buff_usable","wip_usable","teco_admo_usable","cir_out_usable","hist_usable"]

# Based on document property decide what dataTable to use
if dp in completeness:
    newTable = Document.Data.Tables.Item['tat_rca_imro_completeness']
    accuracyPies.Data.DataTableReference = newTable
    accuracyKPI.Data.DataTableReference = newTable
    accuracyPies.ColorAxis.Coloring.Apply("completenessColors") # Apply correct color scheme

    Document.Properties["accuracyReasons"] = dp #Set document property for kpi_chart
    accuracyKPI.Data.WhereClauseExpression = ""	#Set limit by expression for kpi_chart
    accuracyKPI.ColorAxis.Coloring.Apply("accuracy_KPI_scheme")


if dp in accuracy:
    newTable = Document.Data.Tables.Item['tat_rca_imro_accuracy']
    accuracyPies.Data.DataTableReference = newTable
    accuracyKPI.Data.DataTableReference = newTable
    accuracyPies.ColorAxis.Coloring.Apply("accuracyColors") # Apply correct color scheme

    Document.Properties["accuracyReasons"] = dp[0:-7] + "_reason" #Set document property for kpi_chart
    accuracyKPI.Data.WhereClauseExpression = "${accuracyReasons} != 'No issues found'" #Set limit by expression for kpi_chart
    accuracyKPI.ColorAxis.Coloring.Apply("accuracy_ACC_scheme")

```
#### Use buttons to switch between visuals
``` python
from Spotfire.Dxp.Application.Visuals import *
myVis = myVis.As[Visualization]()

# Create button in a text area and assign a string 'A14' to it
if lokatie == "A14":
	myVis.Data.WhereClauseExpression = "[LOKATIE] = 'A14' and [GI_ZONE] = FALSE or [GI_ZONE] is Null"
	Document.Properties["title.MLC.notEWM"] = "A14 not in EWM"
	Document.Properties["title.MLC.EWM"] = "A14 in EWM"
	myVis.Trellis.RowAxis.Expression = "<[PIJPLIJN]>"
	myVis.Trellis.ColumnAxis.Expression = "<[in_ewm]>"

# Create button in a text area and assign a string 'notA14' to it
if lokatie == "notA14":
	myVis.Data.WhereClauseExpression = "[LOKATIE] != 'A14' and [GI_ZONE] = FALSE or [GI_ZONE] is Null"
	Document.Properties["title.MLC.notEWM"] = "Locations except A14 not in EWM"
	Document.Properties["title.MLC.EWM"] = "Locations except A14 in EWM"
	myVis.Trellis.RowAxis.Expression = "<[PIJPLIJN]>"
	myVis.Trellis.ColumnAxis.Expression = "<[in_ewm]>"

# Create button in a text area and assign a string 'GI_ZONE' to it
if lokatie == "GI_ZONE":
	myVis.Data.WhereClauseExpression = "[GI_ZONE] = TRUE"
	Document.Properties["title.MLC.notEWM"] = "GI ZONE"
	Document.Properties["title.MLC.EWM"] = ""
	myVis.Trellis.RowAxis.Expression = "<[PIJPLIJN]>"
	myVis.Trellis.ColumnAxis.Expression = "<>"
```
