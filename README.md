# ESPRESSO
An R Markdown file to analyse feeding data from custom ESPRESSO rig and CRITTA software output. A document is produced with several summary plots and statistical comparisons.

## Requirements 
#### Mac OS X
* R version 3.2.0
    - You should have installed the lastest versions of the ggplot2 (2.0.0) and cowplot (0.6.0) libraries.
    - To do this, run the command `update.packages()` in the console.
* RStudio Version 0.99.441
* MacTex 2015 <http://www.mactex.org> (Required for Tufte-style PDF layout)

The R Markdown file can be knitted in RStudio runnning on Windows as well, but you must install MikTeX <http://miktex.org> for PDF output.

## Usage
1. Create a new folder with 2 sub-folders: `metadata` and `feedlog`.
2. Place the metadata output from CRITTA into the `metadata` folder. 
3. Place the feedlog output from CRITTA into the `feedlog` folder.
    - Note that paired feedlog and metadata files from the same experiment **must have exactly the same filename format, listed below**.
    - `FeedLog <underscore> Date <underscore> Time <underscore> ExtraInformation.csv`
        - *There should be no spaces in the filename; spaces are placed above to enhance readability.*
4. In the main folder, create a text file titled `reference_levels.txt`.
5. This text file is in comma-seperated value (CSV) format. It contains the levels for each contrast in your experiment. 
    - This file has a header line `Factor,Levels`.
    - Each line after that is a contrast factor, with the levels listed and separated by commas.
    ```
    Factor,Levels
    Genotype, W111;Driver-Gal4, W111;UAS-TrpA1, Driver-Gal4>UAS-TrpA1
    FoodType, Sucrose_Only, Arabinose_Only, Sucrose_and_Arabinose
    Temperature, 22, 29
    ```
    - **There cannot be any spaces in any of the contrast factor names, or levels.** The spaces after the commas should not be there; they are shown for readibility purposes. 
    - In the above example, there are 3 contrasts: Genotype, FoodType, and Temperature. 
    - There are 3 levels for Genotype, 3 levels for Foodtype, and 2 levels for Temperature.
    - **The first level listed for each contrast is the reference level.**
        - The levels should be listed in "descending order". This means that the "true" experimental levels should go last, while the control experimental levels should be listed first. This will allow relevant effect sizes to be calculated, with appropriate reference levels.

6. With the exception of “FoodType”, the other contrasts **must be columns** in the metadata file (i.e. the factor names must also be column names in the metadata file, and the levels stated in `reference_levels.txt` should match exactly those in the metadata file.)
    ```
    ID,Genotype,Sex,Minimum Age,Maximum Age,Food 1,Food 2,Temperature
    1,W111;Driver-Gal4,M,5,7,Sucrose_Only,Sucrose_and_Arabinose,22
    2,W111;Driver-Gal4,M,5,7,Sucrose_Only,Sucrose_and_Arabinose,22
    3,W111;Driver-Gal4,M,5,7,Sucrose_Only,Sucrose_and_Arabinose,22
    4,W111;Driver-Gal4,M,5,7,Sucrose_Only,Sucrose_and_Arabinose,22
    ```
7. Set the working directory in R to this new folder you have created with:
    ```r
    setwd("path/to/directory")
    ```
8. Open the R Markdown file and edit the chunk titled `setVariables` (lines 11 to 18).
    ```r
    h <- 7 # Duration of experiment, IN HOURS. Change this if you just want to analyse, say, the first 3 hours.
    bs <- 300 # Bin size of combined density raster plot, in seconds. Anywhere between 5 min (300s) and 10 min (600s) seems to be good.
    bw <- 600 # Bin-sizes of time-course in seconds (s). Change here to change the bin size. (600s = 10 min)

    file.path <- c("path/to/directory")
    # Local file directory path name where data files are stored.
    ```
    Whilst the default values for `h`, `bs` and `bw` should be appropriate for most purposes, you need to check that `file.path` is correctly listed.
9. If this is your first time running the R Markdown file, you will need to install several R packages. To do this you simply need to run the chunk titled `installPackages`. 
    - This is done by placing the cursor anywhere within the chunk and hitting `Command-Enter` (`Control-Enter` on Windows).
10. Knit a PDF file by clicking the Knit button (alternatively, `File > Knit` or `Shift-Command-K`). 

## Troubleshooting
This section will be completed in the near future.
  