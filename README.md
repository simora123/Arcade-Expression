Arcade Expression #1<br />
Intersect. Finds locations from parks layer that are 1/2 miles<br />


var intersectLayer = Intersects(FeatureSetByName($map, "Recreation_Parks"),Buffer($feature, .5, 'mile'))<br />
var intersectLayer2 = Intersects(FeatureSetByName($map, "Trails"),Buffer($feature, .5, 'mile'))<br />
var parks = ""<br />
var pcount = 0<br />
for (var f in intersectLayer){<br />
    parks += f.PARK_NAME + TextFormatting.NewLine<br />
    pcount += 1<br />
}<br />
Count(parks)<br />
<br />
var tcount = 0<br />
var trails = ""<br />
for (var t in intersectLayer2){<br />
    tcount += 1<br />
    if (tcount != 0){<br />
        trails += t.TRL_NAME + " is 1/2 mile from location" + TextFormatting.NewLine<br />
    }<br />
}<br />
<br />
return "There is " + pcount + " Parks with a 1/2 miles of location" + TextFormatting.Newline + parks + TextFormatting.Newline + trails<br />
<br />
<br />
Arcade #2<br />
Adjusting labels with AGOL pop up<br />
<br />
var results = ''<br />
var total = 0<br />
<br />
total = $feature["Functional_Class"] + $feature["Interchange"] + $feature["Railroad"] + $feature["Primary_Grwth_Area"] + $feature["Secondary_Grwth_Area"] +<br /> $feature["Future_Grwth_Area"] + $feature["Sewer_Water_Availability"] + $feature["Broadband"] + $feature["Trans_Routes"]<br />
<br />
if ($feature["GA_TYPE"] == "Growth"){<br />
    results += "Total score is " + total + TextFormatting.NewLine + "(Property can have score of 0 to 9)" + TextFormatting.NewLine}<br />
else if ($feature["GA_TYPE"] == "Rural"){<br />
    results += "Total score is " + total + TextFormatting.NewLine + "(Property can have score of 0 to 6)" + TextFormatting.NewLine}<br />
<br />
if ($feature["Functional_Class"] == 0){<br />
    results += "Functional Class= No (Not within 1/2 mile)" + TextFormatting.NewLine}<br />
else if ($feature["Functional_Class"] == 1){<br />
    results += "Functional Class = Yes (Within 1/2 mile)" + TextFormatting.NewLine}<br />
<br />    
if ($feature["Interchange"] == 0){<br />
    results += "Interchange = No (Not within 1/2 mile)" + TextFormatting.NewLine}<br />
else if ($feature["Interchange"] == 1){<br />
    results += "Interchange = Yes (Within 1/2 mile)" + TextFormatting.NewLine}<br />
 <br />   
if ($feature["Railroad"] == 0){<br />
    results += "Railroad = No (Not adjacant)" + TextFormatting.NewLine}<br />
else if ($feature["Railroad"] == 1){<br />
    results += "Railroad = Yes (Adjacant)" + TextFormatting.NewLine}<br />
<br />
if ($feature["GA_TYPE"] == 'Growth' && $feature["Secondary_Grwth_Area"] == 0 && $feature["Future_Grwth_Area"] == 0){<br />    
    if ($feature["Primary_Grwth_Area"] == 0){<br />
        results += "Primary Growth Area = No" + TextFormatting.NewLine}<br />
    else if ($feature["Primary_Grwth_Area"] == 3){<br />
        results += "Primary Growth Area = Yes" + TextFormatting.NewLine}<br />
    else if ($feature["Primary_Grwth_Area"] == Null){<br />
        results += "Primary Growth Area = N/A" + TextFormatting.NewLine}<br />
}<br />
if ($feature["GA_TYPE"] == 'Growth' && $feature["Primary_Grwth_Area"] == 0 && $feature["Future_Grwth_Area"] == 0){<br />  
    if ($feature["Secondary_Grwth_Area"] == 0){<br />
        results += "Secondary Growth Area = No" + TextFormatting.NewLine}<br />
    else if ($feature["Secondary_Grwth_Area"] == 2){<br />
        results += "Secondary Growth Area = Yes" + TextFormatting.NewLine}<br />
    else if ($feature["Secondary_Grwth_Area"] == Null){<br />
        results += "Secondary Growth Area = N/A" + TextFormatting.NewLine}<br />
}<br />
if ($feature["GA_TYPE"] == 'Growth' && $feature["Primary_Grwth_Area"] == 0 && $feature["Secondary_Grwth_Area"] == 0){<br />      
    if ($feature["Future_Grwth_Area"] == 0){<br />
        results += "Future Growth Area = No" + TextFormatting.NewLine}<br />
    else if ($feature["Future_Grwth_Area"] == 1){<br />
        results += "Future Growth Area = Yes" + TextFormatting.NewLine}<br />
    else if ($feature["Future_Grwth_Area"] == Null){<br />
        results += "Future Growth Area = N/A" + TextFormatting.NewLine}<br />
}<br />    
if ($feature["Sewer_Water_Availability"] == 0){<br />
    results += "Sewer/Water Availability = No" + TextFormatting.NewLine}<br />
else if ($feature["Sewer_Water_Availability"] == 1){<br />
    results += "Sewer/Water Availability = Yes" + TextFormatting.NewLine}<br />
<br />    
if ($feature["Broadband"] == 0){<br />
    results += "Broadband = No" + TextFormatting.NewLine}<br />
else if ($feature["Broadband"] == 1){<br />
    results += "Broadband = Yes" + TextFormatting.NewLine}<br />
<br />    
if ($feature["Trans_Routes"] == 0){<br />
    results += "Transit Route = No (Not within 1/2 mile)" + TextFormatting.NewLine}<br />
else if ($feature["Trans_Routes"] == 1){<br />
    results += "Transit Route = Yes (Within 1/2 mile)" + TextFormatting.NewLine}<br />
<br />    
return results<br />
<br />
Arcade #3<br />
Arcade label adjustment<br />
<br />
var Submitted = $feature["Department"];<br />
<br />
var Deparment = IIF(Submitted != Null, 1,'')<br />
<br />
if (Submitted == "PC"){<br />
    return "YCPC"<br />
}<br />
if (Submitted == "RD"){<br />
    return "Recorder of Deeds"<br />
}<br />
if (Submitted == "TA"){<br />
    return "Tax Assessment"<br />
}<br />
<br />

