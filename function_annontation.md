# Annotation of Functions
Corresponds to the sections in the jupyter notebook: ‘IMRAlgorithmShell.py’

## Constants
All constants are defined in the beginning of the jupyter notebook which gives developer freedom to change some values of bin limits and weights upon Tarek’s request
## Validating Input
3 validation functions to ensure that the entered functions are within certain restrictions
* Validate SAT
  * Checks if the entered value is a number and ensures that it is greater than 0 and less/equal to the maximum score of 1600, making it intervals of 10 doesn’t matter because of organization into bins
* Validate ACT
  * Checks if the entered value is a number and ensures that it is greater than 0 and less/equal to the maximum score of 36, intervals of 1 doesn’t matter because of organization into bins
* Validate GPA
  * Checks if the value on the (4.0 scale) is within the bounds of 1 and 4 and is a numerical value.
  * Error may arise with the replacing the ‘.’, not sure what to do there, leaving it up to developer

## Bin Creation
* Sat_bin
  * This function takes in the SAT score from the user input and checks which bin it is in based on the defined bin ranges. It returns a bin-value that is later used to match up with the schools from the database.
    * Use a If/elif statement
* Act_bin
  * Logically same as SAT_bin
* Gpa_bin
 * Logically same as SAT_bin
* Acceptance_rate_bin
  * This function takes in the users desired Acceptance Rate range for schools from the selection slider widget. The ranges are defined based off of the percentiles/bins. This checks the event from the selection slider and returns the bin value for that ACR criteria
    * Automatic update with the on_change functions defined in the main
* Enrollment_bin
  * Logically same as acceptance_rate_bin
  * Automatic update with the on_change functions defined in the main
* Campsize_bin
  * Logically same as acceptance_rate_bin
  * Automatic update with the on_change functions defined in the main
* Pnm_bin
  * Logically same as acceptance_rate_bin
  * Automatic update with the on_change functions defined in the main
* Tuition_bin & check_tuition
  * First selection slider prompts user to select in-state tuition or out of state tuition, then calls the function check_tuition to return a value 1, for in state and 2, for out of state
  * Within the automatic update function, the second widget is available for the user to select their tuition range and that function operates like acceptance_rate_bin
  * The automatic change function within the main automatically updates the tuition type and tuition_bin sequentially
* Division_bin
  * Logically same as acceptance_rate_bin
  * Automatic update with the on_change functions defined in the main
  * By priority ordered Division 1, 3, 2, 4, 5 as Division 3 schools are more desirable
and ranked ahead of division 2 schools

## Organization into bins
* Imported pandas to read the csv file and created an initial dataframe
* Process for each criteria...
  * Created a dataframe with just the columns of ‘name’ and ‘avg_sat_1’ from the imported database
  * Defined lists for each bin so during the loop, the names of schools in each bin would be added to the the corresponding list
  * Iterate over the dataframe by index and add schools to a bin-list if there sat score is within the corresponding bin
     * TUITION IN-STATE v.s. TUITION OUT-OF-STATE IS NOT WORKING...JUST
     LEAVE IT AT IN-STATE DO NOT MOVE SLIDER
  * Create a dictionary with the keys as the schools in the list and the values as the bin-values for each corresponding bin
  * Create one large dictionary for the criteria as a whole with each school and its bin-value
* This is the same process for all statistical criteria

## MATCHING FUNCTIONS
* Sat_match
  * Provides the weights of the school based on user bin-value.
  * The parameter of the function is the user bin-value based on their input and
  return value of the bin-creation section
  * Initializes dictionary of weights where the keys will be the schools and the values
  will be the weights based on the user bin-value match
  * Iterates over the dictionary of the SAT schools and their bin values and checks
  for equality between the user bin-value and the schools bin-value, if they are equal the weight is 100, if they are +/- 1 bin away, the weight is 85, if they are +/- 2 bins away, the weight is 70, +/- 3 bins 50, +/- 4 bins 45, +/- 5 bins 60 and anything else 0
  * Returns the dictionary of the weights
* act_match, gpa_match, acceptance_rate_match, enrollment_match, campsize_match,
tuition_in_match, tuition_out_match, major_match, division_match all follow the same process and logic but with different weights for value differences

## MATCHMAKER
* Function that is used to calculate the percent match based on the all the weights from each statistical criteria
  * The parameters are the dictionaries returned from the matching functions, which contains keys as the school names and values as the weights for that criteria
  * Initialized a dictionary within the function that will be the computed value of the weights of the criteria times the weight of the larger category (1 of the 5 main categories)
  * Iterate over each dictionary and compute the value of the criteria based on the weight, times the overarching weight and add those values to a new dictionary
  * To sum up all the computed values, i created a list of all the dictionaries and used the functools, operator and collections packages to add together the values with matching school names, this will add all the values of the dictionaries with matching names and provide create a dictionary with the school name and the percent match
  * That is returned to the main and printed so the user has a dictionary of the schools and the corresponding percent match in order of highest match percentage 1st.

 
