#CodeBook.md used in the run_analysis.R script

This codebook complements the README.txt,features_info.txt,features.txt and README.md files relative to this script.

Processing version:

R-version    3.1.3 (2015-03-09) -- "Smooth Sidewalk"
Copyright (C) 2015 The R Foundation for Statistical Computing
Platform: x86_64-w64-mingw32/x64 (64-bit)

packages used:

package name   Purpose                                                 version
RCurl           General network (HTTP/FTP/...) client interface for R   1.95-4.5
plyr            Tools for splitting, applyingg and combining data       1.8.1
dplyr           A Grammar of Data manipulation                          0.4.1

The variables are categorized by type (chr, numeric, factor) and (atomic,vector,data.frame) and the corresponding use (parameter,variable).

a) parameter variables type used for Input:

variable name	type		purpose					value
datadir		chr		sub-directory to save data		"./data" 
SSLurl		chr		data source location			"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
querytext	chr		query mean() and std() from chr list 	"[Mm][Ee][Aa][Nn]\\(\\)|[Ss][Tt][Dd]\\(\\)"

b) functions defined in script:

name                            input                                   output
secondElement	function (x)    chr list x                              x[[2]]
translateElement function (x,...) chr list x                            chr list x translated
                                function builds a ch 2-col dict df
                                from chr list (RegEx)
                                to   chr list (English)
                                translates each element of x
zapDuplicate	function (x)	list x                                  list x without duplicate
                                unlists x, strsplit at " ",
                                paste unique chunks and " "

c) variables used to process script
name		type		purpose					content				more.info in
filename	chr		filename parameter in download.file()	ex:"./data/Dataset.zip",
filepath	chr		complete filepath			ex:"./data/UCI HAR Dataset/train/y_train.txt"
datasetdir	chr list	directory				ex:"./data/UCI HAR Dataset/train"
group		factor		group_by test and train			Factor w/ 2 levels "test","train":1 2
selected	num vector	vector of indexes to populate df.sel	num[1:66] 4 5 6 7 8 9 44 45 46 47...
cv		chr vector	column headers vector for df.sel	chr[1:68] "subject" "activity"...
df		    dataframe	tidy dataset goal of step 1		10299 obs. of 564 var		df_structure.txt
df.X_test	    dataframe	561 num data vectors for test group	2497 obs. of 561 var		df_X_structure.txt
df.X_train	    dataframe	561 num data vectors for test group	7352 obs. of 561 var		df_X_test_structure.txt
df.activity	    dataframe	activity table				6 obs. of 2 var			df.activity_structure.txt
df.features	    dataframe	features table				561 obs. of 2 var		df.features_structure.txt
df.mean		    dataframe	tidy data set goal of step 5		180 obs of 68 var		df.mean_structure.txt
df.sel		    dataframe	tidy data set goal of step 4		10299 obs. of 68 var		df.sel_structure.txt
df.subject_test	    dataframe	subject table for test group		2497 obs. of 1 var		df.subject_test_structure.txt
df.subject_train    dataframe	subject table for train group		7352 obs. of 1 var		df.subject_train_structure.txt
df.test		    dataframe	aggregated test data			2497 obs. of 564 var		df.test_structure.txt
df.train	    dataframe	aggregated train data			7352 obs. of 564 var		df.train_structure.txt
df.y_test	    dataframe	1 activity index vector for test group	2497 obs. of 1 var		df.y_test_structure.txt	
df.y_train	    dataframe	1 activity index vector for test group	7352 obs. of 1 var		df.y_train_structure.txt	

All dataframes structures are provided by running str() and attached for documentation purpose. 
note that the script performs cleanup and does only retain the df, df.sel and df.mean dataframes at end of step 5.

df		    dataframe	tidy data set aggregating test and
				train groups saved as df.txt in step 1	10299 obs. of 564 var		df_structure.txt
df.sel		    dataframe   tidy data set queried with querytext
			 	completed in step 4			10299 obs. of 68 var		df.sel_structure.txt
df.mean		    dataframe	tidy data set averaging by suject and
				activity df.sel data 
				saved as dfmean.tx in step 5		180 obs. of 68 var		df.mean_structure.txt

Notes: 
All numeric data saved in the data sets is normalized and bound to [-1,1] as specified in original dataset README.txt
group is factor variable is a factor variable w/ 2 levels "test","train": 1:2
activity is a factor variable w/ 6 levels "WALKING","WALKING_UPSTAIRS","WALKING_DOWNSTAIRS","SITTING","STANDING","LAYING":1:6
subject is a factor variable w/30 levels "1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19",
"20","21","22","23","24","25","26","27","28","29","30":1:30

In the data subdirectory, the complete data frame structures is described in the corresponding .txt files. Also, the complete column names for the three important dataframes are provided as df_colnames.txt, dfsel_colnames.txt and dfmean_colnames.txt and are also supplied to complement the codebook.
