# Udacity Data Scientist Project 1
*Date updated: Apr 5, 2020*

### Project Requirements from Udacity
For this project, you will be creating a blog post and GitHub repository to begin building a data science portfolio of your own.

* Come up with three questions you are interested in answering.
* Extract the necessary data to answer these questions.
* Perform necessary cleaning, analysis, and modeling.
* Evaluate your results.
* Share your insights with stakeholders.

### Where to Start
There are two components that are required for project completion.

* A Github repository for your code.
* A blog post of your findings.

Your Github repository must have the following contents:

* A README.md.
* Your code in a Jupyter notebook, with appropriate comments, analysis, and documentation.

### Data source
**2019 Novel Coronavirus COVID-19 (2019-nCoV) Data Repository by Johns Hopkins CSSE**
https://github.com/CSSEGISandData/COVID-19

For this project, we choose the timeseries dataset in the sub-directory: https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv

## CRISP-DM
#### 1. Business understanding
The goal is to visualize different countries' time series data and to understand when will see a turning point in decreasing growth of confirmed cases. This could be breakdown into three subquestions:
1. Which top 5 countries are having the highest confirmed cases of COVID-19?
3. How long will it take to have closing to 0 daily growth in confirmed cases?
2. How long will it take to have increasing speed first decreased?

#### 2. Data understanding
Data is collected from multiple sources by the Johns Hopkins University Center for Systems Science and Engineering (JHU CSSE). It is well cleaned and structured in country vs. timestamp format.
* There are 258 country/province split in rows by the time of analysis Apr 4, 2020.
* There are 77 days measured in columns by the time of analysis Apr 4, 2020.
* There are 178 missing values in Province/State however no missing data in Country/Region. This means some country only have all numbers and do not have Province/State split numbers.
* There is no missing value in other columns.
* By the date April 3rd, 2020, there are 1,095,917 total confirmed cases worldwide.
* By the date April 3rd, 2020, the top 5 countries with highest confirmed cases are US, Italy, Spain, Germany, China.

#### 3. Data preparation
Preparation steps:

1. To better understand the country level numbers we have aggregated the numbers into country level and sum by total of different province/state numbers.
2. Instead of absolute date time, we have converted them into relative days: days since the first case confirmed.
3. Adjust China starting days: since China reported the first confirmed case with 548, we are missing the growth curve before that. We are then adjust the starting date by using the new report firstly confirmed case as Dec 1st 2019.
4. Besides the daily confirmed cases, we also calculated cases differences from previous day.

#### 4. Modeling
Construct model based on China's curve. Then use other countries development shape mapping to China's curve and estimate when things will get better.
* China Wuhan has ended quarantine by end of March which is nearly 107 days since the first confirmed cases.
![China's end quarantine date](/Plots/confirmed_cases.png)
* China has seen the first decrease in new cases increased from previous day at around 75 days
![China's turning point (slow down of daily increased cases)](/Plots/confirmed_increases.png)
* Modelling conclusion: based on this very simple model, we could potentially infer that 32 days (107 - 35 days) after the flattened daily increase. We could expect the end of quarantine.

#### 5. Evaluation
Based on this very simple model, we could try to understand for other countries, when we will potentially end quarantine. For example:
* **Italy**: looking at the current curve in Italy, we see daily increases has been stable for two weeks. We could expect decreasing based on China's curve. We can add now 35 days to expect the end of quarantine in between May 10 to May 15, 2020.
* **US**: Since we still have not observed any flattened curve. We could still expect the daily increased cases grow in the coming days.
* **Netherlands**: we can observe flattened curve. We could also boldly predict quarantine ending between May 10 to May 15, 2020.

Since we have no way to test our model at this moment (no other countries than China has ended quarantine). We will continue our observation.

#### 6. Deployment
This is a highly experimental study for online courses project. Disclaimer: use on your own risk.
