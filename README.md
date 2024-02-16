# Alraies-at-al-2024n
ImageJ homemade codes to analyse images for quantification of different protien expresssion. I have added the codes that can be tailored upon user's needs.
Images needs to be in a TIF format, and use ImageJ software.
Code for GFP quantification: 
name=getTitle(); /// work with an open image to correct

offset=80;

MeanBlurradius=15;
TopHatRadius=40;

run("Set Measurements...", "area mean min shape integrated median display redirect=None decimal=3");

run("Clear Results");

/// correction signal camera
run("Subtract...", "value="+offset); // remove offset
run("Duplicate...", "title=tempCorrection");


/// filtering
run("Mean...", "radius="+MeanBlurradius);
run("Minimum...", "radius="+TopHatRadius);
run("Maximum...", "radius="+TopHatRadius);

/// normalisation
run("Measure");
Max=getResult("Max",0);
run("Clear Results");

run("32-bit");
run("Divide...", "value="+Max);

imageCalculator("Divide create 32-bit", name,"tempCorrection");
selectWindow("Result of "+name);
rename("Corrected_"+name);

