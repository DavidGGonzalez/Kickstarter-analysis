# Kickstarting with Excel

## Overview of Project
Thanks to my previous analysis, Louise's play ***Fever*** came close to its fundraising goal in a very short period of time. Now, she wants to know how other campains have succeded in relation to their launch date and the goal they were set for.
#
## Analysis and Challenges
I need to concentrate my efforts in finding how the launch date had affected other funraising projects, but more specifically within the __Theater__ :performing_arts: category so it better corralate with Louise's needs. The only challenge was to pay attention to the details like selecting filter correctly depending on the request's needs.
#
### Analysis of Outcomes Based on Launch Date
Using the main data set, I have:
- Created a new column called __Year__, then filled this column by applying the following [YEAR()](https://support.microsoft.com/en-us/office/year-function-c64f017a-1354-490d-981f-578e8ec8d3b9) excel formula `=YEAR(CELL)`, were `CELL = S2`.
- Create a Pivot table on a new sheet called ***Theater Outcomes by Launch Date***
    - `Parent Category` and `Years` were set as filters.
    - `Outcomes` were set as columns, but we filtered them leaving `outcome="live"` out so we can evaluate those that were completed already; they were also set as values to obtain the count for each `outcome`.
    - Excel would automatically divide `date` column into `Years`, `Quarters`, and `Months` when dropped as a pivot table row, so I have removed years and quarters to represent our data by month, this will allow me to filter by year and see how projects' outcome was affected by the month they were launched at.
    - I've set `Parent Category="theater"` to see only data for those projects related to theaters.
    - Created a pivot chart, type __Line with Markers__.

*Final Pivot Table, after `Parent Category` was filtered by `theater`*

![The Pivot Table looks like this](/Resources/PivotTable.png)

***Theater Outcomes Based on Launch Date*** chart.

![Theater Outcomes Based on Launch Date Chart](/Resources/Theater_Outcomes_vs_Launch.png)
#
### Analysis of Outcomes Based on Goals
Using the main data set, I have:
- Created a new sheet called __Outcomes Based on Goals__. with the following `columns` in it:
    - Goal
    - Number Successful
    - Number Failed
    - Number Canceled
    - Total Projects
    - Percentage Successful
    - Percentage Failed
    - Percentage Canceled
- To properly group projects based on their goal amount, the following ranges were created as `rows` under the __Goal__:
    - Less Than 1000
    - 1000 to 4999
    - 5000 to 9999
    - 10000 to 14999
    - 15000 to 19999
    - 20000 to 24999
    - 25000 to 29999
    - 30000 to 34999
    - 35000 to 39999
    - 40000 to 44999
    - 45000 to 49999
    - Greater than 50000
- Using the [COUNTIFS()](https://support.microsoft.com/en-us/office/countifs-function-dda3dc6e-f74e-4aee-88bc-aa8c2a866842) function the `Number Successful`, `Number Failed`, and `Number Cancelled` columns were filled, applying differnt criterias to properly accomodate for the evaluated range using the following `columns` from the `Kickstarter` sheet: `D` (__goal__), and `F` (__outcomes__)
    - For a comparison using 2 criterion: `=COUNTIFS(Kickstarter!$D:$D,"<1000",Kickstarter!$F:$F,"successful")`
    - For a comparison using more than 2 criterion: `=COUNTIFS(Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<=4999",Kickstarter!$F:$F,"successful")`
- Finally, a __Line Chart__ was created to properly visualize the results.

*Final Table*

![Outcomes Based on Goals table](/Resources/Outcomes_Based_on_Goals_Table.png)


***Oucomes Based on Goals*** Chart

![Outcomes Based on Goals table](/Resources/Outcomes_vs_Goals.png)

#
### Challenges and Difficulties Encountered
Data Analysis is based on a review and interpretation of a provided data set, the idea is to be able to ask questions to our data, but first we need *clean and re-format* this data so we can properly work with it. Errors may occure while processing our data and we need use certain excel functions like the [IFERROR()](https://support.microsoft.com/en-us/office/iferror-function-c526fd07-caeb-47b8-8bb6-63f3e417f611) to catch them and to properly handle them, i.e.: `#DIV/0!`. Not many challenges were found with the provided data set, just that the __Date Created__ (`launched_at`) and __Date Ended__ (`deadline`) columns came in a __UNIX Timestamp__ and required a special formula to convert them (`=(((CELL/60)/60)/24)+DATE(1970,1,1)`); please visit [UNIX Timestamp](https://www.unixtimestamp.com/) for more information about this UNIX timespamp.
#
## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date? (for `Parent Category="theater"`)

    1. Campains that were launched in May shows the highest number of success.
    2. January, March, September and November shows almost the same number of campains that failed.

- What can you conclude about the Outcomes based on Goals?

    1. Not a single campaing was canceled, they either failed or succeded.
    2. Campains with a `goal` of less than $1,000 were the most successful ones.
    3. The highest number of failed campaings were the ones with a `goal` set between $45,000 and $49,999
    4. The percentage of campaings that succeded and failed were about the same when the `goal` was set between $15,000 and $19,9999, as well as between $30,000 and $39,999.

- What are some limitations of this dataset?

    I did not find any limitation with the dataset.

- What are some other possible tables and/or graphs that we could create?

    It will all depend on the questions we need to ask out data set and based on client's needs, but I would create a pivot table showing Countries as `Rows`, this would provide a comparison by country if required to launch a campaign in different countries, and I could also add months to see, based on outcomes, how they compared through the year.
