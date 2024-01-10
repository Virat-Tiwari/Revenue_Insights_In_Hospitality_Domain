# Business problem:
AtliQ Grands is the proud owner of numerous opulent hotels throughout India. Yet, AtliQ Grands finds itself experiencing a decline in both market share and revenue within the luxurious/business hotel sector. I, as a data analyst, figure out the key problem of declining revenue using data analytics.

# Preprocessing:
## Data modeling:

Data modeling plays a pivotal role and serves as the foundation for generating meaningful reports. The entire framework of visualizations is constructed upon a well-designed data model. Neglecting proper data modeling can have adverse effects on the overall performance of the generated reports.

In the context of this project, we have meticulously followed the Snowflake data modeling method. This approach involves structuring data into normalized forms, resulting in reduced redundancy and improved query performance. This methodology enhances the way we organize and process data, ensuring optimal results for our analysis.

Remember, a robust data model is the cornerstone of effective data analysis and reporting. By employing sound data modeling practices, we can confidently generate insightful visualizations that empower data-driven decision-making

![2024-01-10 (5)](https://github.com/Virat-Tiwari/Revenue_Insights_In_Hospitality_Domain/assets/66154941/ed1b658e-544b-4dbe-9ac2-a573db2a1114)


## Creating calculated measures

ADR Calculate the ADR(Average Daily rate). It is the ratio of revenue to the total rooms booked/sold. It is the measure of the average paid for rooms sold in a given time period

            ADR = DIVIDE( [Revenue], [Total Bookings],0)

Realisation % calculates the realisation percentage. It is nothing but the successful “checked out” percentage of overall bookings happened.

            Realisation % = 1- ([Cancellation %]+[No Show rate %])

RevPAR Calculate the RevPAR(Revenue Per Available Room)
RevPAR represents the revenue generated per available room, whether or not they are occupied. RevPAR helps hotels measure their revenue-generating performance to accurately price rooms. RevPAR can help hotels measure themselves against other properties or brands.

            RevPAR = DIVIDE([Revenue],[Total Capacity])

DBRN calculates DBRN(Daily Booked Room Nights). This metric tells on average how many rooms are booked for a day considering a time period

            DBRN = DIVIDE([Total Bookings], [No of days])

DSRN calculates DSRN(Daily Sellable Room Nights). This metric tells on average how many rooms are ready to sell for a day considering a time period

            DSRN = DIVIDE([Total Capacity], [No of days])

DURN calculate DURN(Daily Utilized Room Nights). This metric tells on average how many rooms are successfully utilized by customers for a day considering a time period

            DURN = DIVIDE([Total Checked Out],[No of days])

Revenue WoW change % indicates revenue change percentage week over week.

            Revenue WoW change % = 
            Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
            var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
            var revpw = CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
            
            return
            
            
            DIVIDE(revcw,revpw,0)-1

Occupancy WoW change % indicates occupancy change percentage week over week.

            Occupancy WoW change % = 
            Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
            var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
            var revpw = CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
            
            return
            
            
            DIVIDE(revcw,revpw,0)-1

ADR WoW change % helps To find the ADR(Average Daily rate) change percentage week over week.

            ADR WoW change % = 
            Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
            var revcw = CALCULATE([ADR],dim_date[wn]= selv)
            var revpw = CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
            
            return
            DIVIDE(revcw,revpw,0)-1

Cancellation % calculating the cancellation percentage.

            Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])


## Dashboard 1:
![Revenue Insights In Hospitality Domain By Virat Tiwari_page-0001](https://github.com/Virat-Tiwari/Revenue_Insights_In_Hospitality_Domain/assets/66154941/79f0e75a-6ea2-4288-9ed8-e486c7cd0e7d)


## Dashboard use as tooltip 2:
![Revenue Insights In Hospitality Domain By Virat Tiwari_page-0002](https://github.com/Virat-Tiwari/Revenue_Insights_In_Hospitality_Domain/assets/66154941/f8b126e1-d283-4be2-9d05-beff5ece7251)


### This dashboard has interactive features and tooltips.

# Key Findings from this dashboard:

The dashboard was utilized in an attempt to observe all the significant key metrics on a weekly basis. The metrics of Realisation, ADR, and RevPar remained constant, with only a slight fluctuation in occupancy ranging from 50% to 60% when filtering the data according to the week. Throughout the entirety of the period, both occupancy and cancellation rate remained in close proximity to the benchmark set by the industry.

Furthermore, Realisation, ADR, and RevPar also sustained a similar consistency when comparing weekdays to weekends.

Upon arranging the occupancy rate in descending order within the key metrics table, it becomes evident that there exists a correlation between the rating and occupancy.

## Note : 
Pareto Principle: Using the Pareto Principle, also known as the 80/20 rule, can be a useful approach in addressing declining revenue in chain hotels. The principle suggests that roughly 80% of the effects come from 20% of the causes. In this context, it means that a small number of factors or hotels may be contributing significantly to the decline in revenue. Here , We used the Pareto Principle as a guide to initially focus on the lowest-performing hotels can be an effective way to address revenue decline Here’s how we apply it:

- Identify Key Metrics: already identified key metrics such as rating, occupancy, ADR (Average Daily Rate), dsrn (Daily sellable room night), and durn (Daily useable room night. These are important metrics for the hotel industry etc.

- Analyze Data: Started by analyzing the data for all hotels. Calculated the performance of each hotel in terms of these metrics.

- Sort by Performance: Sort the hotels based on their performance in each metric. For example, sort them by occupancy rate from lowest to highest.

# Insights and suggestions:

## ADR Remains Stable
Upon analyzing the dashboard, it's evident that the Average Daily Rate (ADR) for AtliQ Hotels has remained relatively stable over the given time frame. This stability in pricing indicates a consistent pricing strategy.

Notably, AtliQ Hotels currently do not employ dynamic pricing based on weekdays and weekends. This presents an opportunity to consider adjusting the pricing strategy. Dynamic pricing can help optimize revenue by offering different rates for weekdays and weekends, aligning pricing more closely with demand fluctuations.

This insight suggests that exploring dynamic pricing strategies could be a valuable initiative to consider, potentially leading to increased revenue and better revenue management.

## Overall Occupancy Rate
The overall occupancy rate for AtliQ Grands' properties currently stands at a solid 57%. This figure reflects the percentage of available rooms that are being utilized by guests. A 57% occupancy rate indicates a substantial portion of rooms are booked, contributing positively to revenue.

Maintaining a healthy occupancy rate is crucial for optimizing revenue and resource management. This insight suggests that AtliQ Grands has been successful in attracting guests and efficiently filling available rooms.

As part of ongoing strategies, it may be worthwhile to explore avenues to further increase occupancy, especially during off-peak periods, to maximize revenue potential.

Overall, the 57% occupancy rate provides a foundational understanding of AtliQ Grands' performance and can serve as a basis for further revenue optimization efforts.

## Average Rating
The average guest rating for AtliQ Grands' properties is a commendable 3.62. This rating, derived from guest reviews and surveys, reflects the overall satisfaction of guests who have experienced our hospitality.

A rating of 3.62 signifies a positive guest experience, with the majority of guests expressing satisfaction with their stays. Guest ratings are a vital indicator of our service quality and the guest experience we provide.

As we continue to prioritize guest satisfaction, it's important to maintain and improve upon this rating. By consistently delivering exceptional service, addressing guest feedback, and enhancing guest experiences, we can aim for even higher ratings in the future.

The 3.62 average rating underscores our commitment to offering outstanding hospitality and ensuring our guests have memorable stays.


![2024-01-10 (7)](https://github.com/Virat-Tiwari/Revenue_Insights_In_Hospitality_Domain/assets/66154941/f845f82c-059b-453e-ba83-c773af3bce5b)


- when the hotel is sorted by its occupancy rate, we observe a relationship that exists between ratings and occupancy. Consequently, we recommend examining the reviews provided by customers on all booking platforms, addressing and resolving any issues raised by them.


![2024-01-10 (6)](https://github.com/Virat-Tiwari/Revenue_Insights_In_Hospitality_Domain/assets/66154941/8a667d98-ee5b-42d7-ae9f-5f2c5d3ffe9a)

As we can see realisation% and ADR trends by booking platform remained similar and the average difference of $150. we checked the weeks, the trend has no significant difference. Even direct offline and direct online have similar realisation and ADR. offering coupons and cashback incentives directly to customers who book rooms through the hotel’s website or offline at checkout can be an effective strategy to increase revenue realization, even without discouraging the use of third-party booking platforms.
“realization” in the context of the hospitality industry, refers to the percentage of revenue retained after accounting for cancellations and no-shows.

# Suggestions:
- Fixed the issue highlighted by the customer in low-rated hotels to Increase occupancy rate.
- Dynamic pricing strategy
- Offering coupons and cashback incentives directly to customers who book rooms through the hotel’s website or offline at checkout THUS INCREASE realization.
