# IMR Matchmaking
Matchmaking Algorithm for IMRecruitable - Summer 2020 Internship

# Matchmaking Algorithm
* Created a matchmaking algorithm to quantify the 'likeness' of a particular school given student input.
* Performed data cleaning processes of college information database
* Ran distributional analysis in R to compute percentiles and distributional information
* Built standard input interface to trial algorithm
* Disclaimer: Algorithm does not include college major information/data because data set was not provided within time constraints of internship.

## Overview/Basic Logic
The algorithm is organized into three sections; the user input, the sorting and organization of the IMR college database ‘IMRCOLLEGEDATA.csv” and the matching.
The user input section is where the user is prompted to enter various criteria such as SAT, ACT, GPA, desired enrollment and desired school size. The input is sorted into a bin based on various percentiles and distribution information computed from initial analysis in R. For example, if a user entered their SAT score of 1230, it would be in the bin that contains 1230 within its range. The value of that bin is returned to the main. It is important to note that all bins are based on percentiles from the distribution, however for skewed data, bin values are adjusted.

## Organization
The IMR database contains the college information for every school that has athletic programs. It was provided to me by IMRecruitbale, and all information gathered was under instruction from Tarek Merchant.
The organization aspect of the program iterates over the database provided to me by IMRecrtuiable and sorts each school into their respective bin based on the value of the specific criteria. For example, for the SAT criteria, the program will iterate over the data frame of each school and their corresponding SAT value. All schools with an avg SAT in the first bin will be sorted into the first bin. All schools with an avg SAT in the following bins will be sorted into their respective bins.
Iteration over the data frame adds the name of the school for which the SAT is in the bin to a list and then creates a dictionary with the corresponding bin-value mentioned in the user input aspect of the program.

## Matching
This aspect of the program matches the bin value from the user input to the bin from the organization and adds the correct weight for all the schools in the database.
This is done by using the bin-value returned from the user input, and running an if/elif statement checking whether the bin value matches and rating the size of discrepancies to weight each list of schools.
For example, if my SAT bin-value is 3, which is between 970 and 1010. All schools in that 970 and 1010 range are in a list, created in the organization aspect of the program. All schools in that same bin will have 100% match for that criteria, all schools +/- 1 bin will have 85% match for that specific criteria.
There was no information provided to me that suggested the weights of each level in the multi-level algorithm. The deciding of the weights was in accordance with Tarek’s original mode. The main factor in deciding the weights was relative assumption ( +/- 1 bin 85% and +/- 2 bins 75% etc.) ​Each matching function for every statistical criteria creates a dictionary of the school and the corresponding weight.
That dictionary contains all schools and their weights. Ex: { School A: 100, School B: 85...} So in the final math equation, that provides the values for the weights of each criteria.
A function is then called that inputs every dictionary returned from each matching function and iterates over each and every one computing the match value for each of the 5 sub sections and then each specific criteria within the sub sections.

## Design
I organized the algorithm into 5 main categories based on the information provided to me from the database and Tarek Merchant.
* Academic Selectivity
* Enrollment/School Size
* Cost/Affordability
* Majors/Student Life
* Athletic Selectivity

Each of these categories is broken down into smaller categories that have their own weights that sum to the full weight of each category's criteria.
* Academic
  * GPA
  * SAT
  * ACT
  * Acceptance Rate
* Enrollment
  * Undergraduate Enrollment
  * Population of Locational City/Town (big city/small city etc)
* Cost Affordability
  * Tuition
  * Percent of Need Met by Institution
* Majors - SL
  * Majors Offered 
* Athletic Selectivity
  * Collegiate division
  

    
