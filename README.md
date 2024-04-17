# Using-OpenRefine-to-cluster-and-edit-strings
OpenRefine (previously also known as Google Refine) is a free, open-source software used for data cleaning as well as performing both basic and advanced cell transformations. This can be useful if you are working with large raw data files and need to systematically clean string or numeric variables (say, due to the absence of a unique identifier), or want a quick overview of the data before running further analysis. 

OpenRefine can be a useful complementary tool to other statistical software, as part of the data cleaning process. While other softwares have a variety of string cleaning options, OpenRefine can be a more efficient alternative. 

For example, in the simplest case, if we have multiple observations referring to Coder’s Corner in different ways, such as ‘Coders Corner’, ‘Coder’s Korner’, ‘Corner Coder’s’, and ‘Coder’s Corner’, multiple algorithms can be used in OpenRefine to group them into a cluster. These clusters can be used for subsequent analysis.


### Getting started

The most recent version of OpenRefine (release 3.4.1 at the time of writing), can be downloaded at: https://openrefine.org/download.html. You need only choose the download ‘kit’ corresponding to your operating system and follow the installation prompts.

When working with large datasets, files close to 1GB or above, I recommend increasing the RAM allocated to OpenRefine to ensure the file is processed and uploaded smoothly. Windows users can do this by opening the openrefine.exe file and edit the following lines in the openrefine.l4j.ini file:

#max memory heap size

-Xmx1024M

The last line specifies the memory allocated to OpenRefine in mebibytes (where 1 MiB ~= 1.049 MB).  To increase memory, change ‘1024’ to a larger number, e.g. to allocate 2GB of memory, update the last line to -Xmx2048M. You should also ensure your system is using the 64-bit version of Java. 

If using a Mac, hold down the control key while clicking on the OpenRefine.app file, select ‘show package contents’, click on the ‘Contents’ folder and open ‘Info.plist’ with a text editor to change “-Xmx2048M” to the memory needed.

### Importing the data

To get started, we import a dataset containing manufacturing firm data and firm locations. We can do this by creating a new project on the workspace. 

The software can parse a large variety of file types, not limited to text-based files, with a full list of options listed in the bottom left panel.

![open refine 1](https://github.com/csae-coders-corner/Using-OpenRefine-to-cluster-and-edit-strings/assets/148211163/728fbf9b-e950-4aca-b41c-5c527ca43976)

to customise the data delimiter and choose whether to trim leading and trailing spaces. When satisfied with the options selected, you can go ahead and create your project. One handy feature of OpenRefine is that it has an undo/redo panel that appears on the left-hand side of the workspace once you’ve created your project that allows you to track changes and revert anything done to the dataset. 


### Cluster and Edit

OpenRefine’s ‘cluster and edit’ option is useful for cleaning messy string or numeric variables. You may find yourself working with large, raw data files that contain manually inputted string variables without an identifier for each unique entity. For example, you have firm-level data where a firm’s name has multiple typos across different observations, random capitalizations, different word ordering, and random trailing or leading spaces, but nevertheless, multiple observations refer to the same entity. 

While Stata can perform both basic and advanced string cleaning functions, it falls short where there is no unique identifier for a string column of interest. Accounting for each error type across observations makes it difficult to systematically clean raw data consistently. Although leading or trailing spaces can quickly be mopped up in Stata, different word ordering and/or multiple typos across string observations that refer to the same entity cannot be handled easily in Stata. This makes it difficult to catch all the observations in the dataset that belong to the same entity.

OpenRefine has two solutions for messy strings. For large datasets, with too many unique values to be displayed via the ‘facet’ option, which allows users to apply a particular value to all cells contained in a facet grouping, one can instead use the ‘cluster and edit’ function. Clicking on the drop-down arrow of the column of interest, where here we’d like to clean the ‘exporter_city’ variable, we select the ‘cluster and edit’ option.

![open refine 2](https://github.com/csae-coders-corner/Using-OpenRefine-to-cluster-and-edit-strings/assets/148211163/54c30467-282e-4a59-af47-ab84191799e3)

This takes you to the following page. Here city names have been grouped where, by default, OpenRefine applies the most stringent clustering method of key collision fingerprinting. Key collision operations are very fast when working with large datasets. Fingerprinting is the most stringent clustering method, and so the least likely to cluster observations that refer to different entities. It automatically applies more basic cleaning operations such as removing whitespaces, ignoring punctuation and uppercase/lowercase inconsistencies when clustering strings, removing character accents if working with data in foreign languages, and sorts words alphabetically. The last operation is useful in preventing clustering issues when typos include different rearrangements of the same (or similar) words. 

Depending on the nature of the issue at hand there are alternative clustering methods available, including nearest neighbour matching, Levenshtein distance, and prediction by partial matching.

![open refine 3](https://github.com/csae-coders-corner/Using-OpenRefine-to-cluster-and-edit-strings/assets/148211163/1553c0f1-de9c-4e7b-adb7-b7feb0e011fa)

Users can edit the cluster name that OpenRefine will apply to each observation in a given cluster. The right-hand panel specifies the number of clusters found, as well as useful summary statistics. This provides additional flexibility in adjusting the observations included in a particular cluster along multiple dimensions such as the number of choices in the cluster, the rows in the cluster, the average length of choices etc. 

![open refine 4](https://github.com/csae-coders-corner/Using-OpenRefine-to-cluster-and-edit-strings/assets/148211163/7f2ee142-b7f6-4f2d-a50e-59aae8d31119)

For example, we can see that CHICAGO ILLINOIS and ILLINOIS CHICAGO are grouped into the same cluster. While it may seem simple enough to apply this in statistical packages in this scenario, it becomes exceedingly more complicated when the string column contains multiple words. In this case, a few misspellings or changes in the ordering of the firm’s name (or the absence of certain words that are present in other observation, say), make identifying all observations that belong to the same entity tricky. 

OpenRefine can also be used for a range of other purposes which can be found here: https://docs.openrefine.org/

**Diana Beltekian, PhD Candidate in Economics, University of Nottingham
10 February 2021**
