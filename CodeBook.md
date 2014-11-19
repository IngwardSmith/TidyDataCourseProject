# The Codebook

## Variables

* `features` and `activities` are the lists of columns from the downloaded files for the raw data;
* `x_Train`, `y_Train`, `x_Test`, `y_Test`, `subject_Train` and `subject_Test` contain the raw data from the files;
* `subject_Data`, `x_Data` and `y_Data` is just merged data of raw Train and Test datasets;
* `neededcols` contains list of features that have either "-mean" or "std" sub-string - only the needed columns for the tidy data;
* `allData` is `subject_Data`, `y_Data` and `x_Data` merged by columns into one dataset;
* `tidyData` contains all needed average values that will be written into a file.

## Transformations done on Raw Data

First the script sets the needed working directory (change it to your own!) and loads all raw data into the variables.

Then the script `run_analysis.R` executes next steps:

1. Binds Test and Train data for each of the datasets by using rbind().
2. Using grep() function and the regular expression it searches the second column of `features` list that contains labels of variables and chooses only those of them that contain strings "-mean" and "std". All according to the task set in the project. After that the script leaves only these `neededcols` in the `x_Data`.
3. The script takes each value of the `y_Data`, finds the corresponding row in the `activities` dataset, finds its proper name that is contained in the second column of `activities` and assigns it to the y_Data value, thus replacing the numeric indices with the actual names.
4. Using names() function the columns in the `x_Data` are named by the names of needed variables in the features dataset and the y_Data and subject_Data are named "Activity" and "Subject"
5. Using aggregate() function the script divides the data into the subsets according to activity and subject and calculates the mean value for each measured variable. The resulting `tidyData` dataset is created. As aggregate() function created duplicate columns and could not calculate the mean values for the `Activity` column thus replacing them with NAs, we don't need the `Activity` and `Subject` columns anymore. The script removes them.

Finally all the tidy data is written to `tidyData.txt` file.