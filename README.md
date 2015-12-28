# ESPRESSO
R Code to analyse feeding data from custom ESPRESSO rig and CRITTA software output.

## Requirements 
### Mac
* R version 3.2.0 
* RStudio Version 0.99.441
* MacTex 2015 (Required for Tufte-style PDF layout)

The R Markdown file can be knitted in RStudio runnning on Windows as well.

## Description
This is a R Markdown file that processes the CSV output from CRITTA. When the Markdown file is knit in RStudio, a PDF file is produced with the following statistics:

1. Raster Plot of Feed Events
2. Correlation of Feed Duration and Feed Volume
3. Cumulative Volume Drunk Per Fly
4. Time Course (binned by seconds specified in `bw`)

* Proportion of Flies Feeding Preference Index
* Feed Count
* Feed Duration
* Volume Intake
* Feed Count
* Cumulative Volume Intake Feed Size (aka Meal Size) Feed Duration

5. Summary Plots
* Density Distribution
* Summary Histogram
* Summary Table
* Kruskal-Wallis and post-hoc Dunn’s Test
