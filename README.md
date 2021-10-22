Arcade Expression #1
Intersect. Finds locations from parks layer that are 1/2 miles


var intersectLayer = Intersects(FeatureSetByName($map, "Recreation_Parks"),Buffer($feature, .5, 'mile'))
var intersectLayer2 = Intersects(FeatureSetByName($map, "Trails"),Buffer($feature, .5, 'mile'))
var parks = ""
var pcount = 0
for (var f in intersectLayer){
    parks += f.PARK_NAME + TextFormatting.NewLine
    pcount += 1
}
Count(parks)

var tcount = 0
var trails = ""
for (var t in intersectLayer2){
    tcount += 1
    if (tcount != 0){
        trails += t.TRL_NAME + " is 1/2 mile from location" + TextFormatting.NewLine
    }
}

return "There is " + pcount + " Parks with a 1/2 miles of location" + TextFormatting.Newline + parks + TextFormatting.Newline + trails


Arcade #2
Adjusting labels with AGOL pop up

var results = ''
var total = 0

total = $feature["Functional_Class"] + $feature["Interchange"] + $feature["Railroad"] + $feature["Primary_Grwth_Area"] + $feature["Secondary_Grwth_Area"] + $feature["Future_Grwth_Area"] + $feature["Sewer_Water_Availability"] + $feature["Broadband"] + $feature["Trans_Routes"]

if ($feature["GA_TYPE"] == "Growth"){
    results += "Total score is " + total + TextFormatting.NewLine + "(Property can have score of 0 to 9)" + TextFormatting.NewLine}
else if ($feature["GA_TYPE"] == "Rural"){
    results += "Total score is " + total + TextFormatting.NewLine + "(Property can have score of 0 to 6)" + TextFormatting.NewLine}

if ($feature["Functional_Class"] == 0){
    results += "Functional Class= No (Not within 1/2 mile)" + TextFormatting.NewLine}
else if ($feature["Functional_Class"] == 1){
    results += "Functional Class = Yes (Within 1/2 mile)" + TextFormatting.NewLine}
    
if ($feature["Interchange"] == 0){
    results += "Interchange = No (Not within 1/2 mile)" + TextFormatting.NewLine}
else if ($feature["Interchange"] == 1){
    results += "Interchange = Yes (Within 1/2 mile)" + TextFormatting.NewLine}
    
if ($feature["Railroad"] == 0){
    results += "Railroad = No (Not adjacant)" + TextFormatting.NewLine}
else if ($feature["Railroad"] == 1){
    results += "Railroad = Yes (Adjacant)" + TextFormatting.NewLine}

if ($feature["GA_TYPE"] == 'Growth' && $feature["Secondary_Grwth_Area"] == 0 && $feature["Future_Grwth_Area"] == 0){    
    if ($feature["Primary_Grwth_Area"] == 0){
        results += "Primary Growth Area = No" + TextFormatting.NewLine}
    else if ($feature["Primary_Grwth_Area"] == 3){
        results += "Primary Growth Area = Yes" + TextFormatting.NewLine}
    else if ($feature["Primary_Grwth_Area"] == Null){
        results += "Primary Growth Area = N/A" + TextFormatting.NewLine}
}
if ($feature["GA_TYPE"] == 'Growth' && $feature["Primary_Grwth_Area"] == 0 && $feature["Future_Grwth_Area"] == 0){  
    if ($feature["Secondary_Grwth_Area"] == 0){
        results += "Secondary Growth Area = No" + TextFormatting.NewLine}
    else if ($feature["Secondary_Grwth_Area"] == 2){
        results += "Secondary Growth Area = Yes" + TextFormatting.NewLine}
    else if ($feature["Secondary_Grwth_Area"] == Null){
        results += "Secondary Growth Area = N/A" + TextFormatting.NewLine}
}
if ($feature["GA_TYPE"] == 'Growth' && $feature["Primary_Grwth_Area"] == 0 && $feature["Secondary_Grwth_Area"] == 0){      
    if ($feature["Future_Grwth_Area"] == 0){
        results += "Future Growth Area = No" + TextFormatting.NewLine}
    else if ($feature["Future_Grwth_Area"] == 1){
        results += "Future Growth Area = Yes" + TextFormatting.NewLine}
    else if ($feature["Future_Grwth_Area"] == Null){
        results += "Future Growth Area = N/A" + TextFormatting.NewLine}
}    
if ($feature["Sewer_Water_Availability"] == 0){
    results += "Sewer/Water Availability = No" + TextFormatting.NewLine}
else if ($feature["Sewer_Water_Availability"] == 1){
    results += "Sewer/Water Availability = Yes" + TextFormatting.NewLine}
    
if ($feature["Broadband"] == 0){
    results += "Broadband = No" + TextFormatting.NewLine}
else if ($feature["Broadband"] == 1){
    results += "Broadband = Yes" + TextFormatting.NewLine}
    
if ($feature["Trans_Routes"] == 0){
    results += "Transit Route = No (Not within 1/2 mile)" + TextFormatting.NewLine}
else if ($feature["Trans_Routes"] == 1){
    results += "Transit Route = Yes (Within 1/2 mile)" + TextFormatting.NewLine}
    
return results

Arcade #3
Arcade label adjustment
var Submitted = $feature["Department"];

var Deparment = IIF(Submitted != Null, 1,'')

if (Submitted == "PC"){
    return "YCPC"
}
if (Submitted == "RD"){
    return "Recorder of Deeds"
}
if (Submitted == "TA"){
    return "Tax Assessment"
}

