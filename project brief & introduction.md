# MAVEN AIRLINES 
## Challenge Introduction:
<p class="text-justify">
Maven Airlines is a US-based airline headquartered in Boston. The latest passenger survey results have just come in and it looks like the satisfaction rate dipped under 50% for the first time ever. The task now is to: play the role of a data analyst for Maven Airlines and determine the key areas to focus on for getting back on track. Recommend a data-driven strategy for increasing the Maven Airlines’ satisfaction rate and present a single page report or dashboard.
</p>

### Dataset:
The dataset contains the satisfaction scores for *129,880* passengers. Every record in the data represents the input of a single passenger. 
Each record covers details of passenger demographic, flight distance, travel class and purpose and ratings for factors like cleanliness, comfort and service 
as well as overall satisfaction with the airline.
### Data Exploration:
Except for the **Arrival Delay** column, no other column in the dataset has blank or NA data. 
The dataset contains 3 variables that help us understand the demography of the passengers that took this survey and they are: Gender, Age and Customer Type. 
Let us explore these two columns:
The Gender column has two distinct categories of entries i.e. **Male** and **Female**.

![image](https://user-images.githubusercontent.com/54994083/178721038-9da28f78-13f0-45af-8542-e1ea692593fe.png)

It seems that the survey consisted of almost equal number of male and female respondents with a slightly higher number of female passengers. For the analysis, it shall be assumed that there is negligible difference in the numbers and not enough to introduce bias. 
Let us summarize the variable ‘Age’ and see what the distribution looks like: 
````
Avg	39.43
Min	7
Max	85
Median	40
Mode	39
````
<p class="text-justify">
The customer type is a categorical variable with two distinct values which are: ‘Returning’ and ‘First-time’. This is an important data point as it allows us to segment the data and recognize if we can tie specific sentiments to a specific basket of customers. It also helps to understand our existing customer groups’ sentiments further and develop strategies in the direction of customer retention. Some of the key business questions that this analysis aims to answer are:
</p>

1.  Which percentage of the airline passengers are satisfied ? 
2.  Does it vary by customer type ? What type of travel ?
3.  What is the customer profile for a repeating airline passenger ?
4.  Does flight distance affect customer preferences or flight patterns ? Find the breakdown of the number of customers in different flight distance buckets and for each, find the % of satisfied and dissatisfaction percentage
5.  What factors contribute to customer satisfaction the most ? What about dissatisfaction ?

#### Findings

1.  Out of the total number of passengers who took the survey, 43.45% of them are satisfied with the airline services, and this amounts to 56428 of them. However, when we break this down by customer type, it can be seen that 47.81% of the ‘Returning’ customers are satisfied as against the First-time pool showing a 23.97% of customers satisfied.
2.  Because a large part of the people who took the survey i.e. about 81% of them are *repeating customers*, it would be a good idea to understand the customer profile of a repeating customer. There are several attributes in the data that can help describe the profile of a repeating customer. We will focus on the number of customers in this group,distributions of gender, age , type of travel , class and satisfaction type for different types of customers. All of the above features do not contain any blank or inconsistent entry in the data and therefore we move straight away into the analysis

3.  In order to get an idea of how flight distance travelled by customers from different categories, a conditional column ‘Flight Distance Category’ is created based on ‘Flight Distance’. This column basically categorises the numeric variable into 4 different buckets. This helps to encode the numeric values into labels.
The following is the M code used to create this conditional column.
````
  = Table.AddColumn(#"Changed Type", "Flight Distance Category", each if [Flight Distance] > 4000 then "Greater than 4000" else if [Flight Distance] > 2500 then "Between 2500 & 4000" else if [Flight Distance] > 1000 then "Between 1000 & 2500" else "Less than 1000")
````
4.  To understand what factors contribute to satisfaction of the customers most, likert analysis can be performed. Likert Analysis is used to summarise the answers to survey questions which can be answered with a categorical value that corresponds to one of [Strongly Disagree, Disagree,Neutral,Agree, Strongly Agree]. This is called a 5-point likert analysis. In this dataset, various attributes signify quality of service like Ease of Online Booking, Check-in Service, Online Boarding etc to name a few. 

The customers have responded to these questions with a whole number between 0 to 5 where each value represents a satisfaction level with ‘0’ for ‘not applicable'. This dataset contains 14 different questions as part of the survey that take a categorical value correspondong to the degree of satisfaction. Now, this is quite a high number of attributes. Therefore, we can divide the attributes into two categories: **Boarding experience** and **In flight experience**.

Under 'Boarding Experience' we have: Gate location, departure and arrival time convenience, Check in service, baggage handling, ease of online booking , online boarding
Under 'In Flight Experience' we have: Seat comfort, On board service, In flight entertainment, Leg room service, cleanliness, Food and drink, In flight wifi service, in flight service

From the below average distribution, it is evident that In-flight wifi service, Ease of Online Booking and Gate Location have the least scores among all the survey questions. 

<img width="209" alt="image" src="https://user-images.githubusercontent.com/54994083/178770557-db3e5395-0906-4a2d-8313-b0652ad8c4a6.png">

Some of the overall figures are as follows:

1.  About 129.9k customers participated in the survey. In total 43% of the customers are satisfied with the airline services overall. The question with lowest avearge score is 'In-flight Wifi Service' with 2.73 & the 'In-flight Service' has the highest overall average with 3.64. 

2.  There are various categories of flight distance traveled by the customers & the analysis reveals that the customers traveling between 2500 and 4000 miles have the lowest % of satisfied customers, **16%**, whereas the group traveling between 1000 & 2500 miles have 27% satisfied customers. 

3.  The second part of the analysis segments the customers based on whether they are **returning** or **first time** customers to the business. This way, different campaigns can be designed specifically for the different types of customer base.

The final dashboard was built using Microsoft Power BI and it can be found [here](https://github.com/shsra430/MavenAirlines/blob/main/Maven%20Airlines%20Final%20Dashboard.png). Click [here](https://github.com/shsra430/MavenAirlines/blob/main/MAVEN%20AIRLINES%20Github%20Report%20PDF.pdf) for more visualizations.
### Recommendations for next-steps
1.  **82%** of respondents are returning customers. The average profile of a returning customer is made up of people **between 35 & 60 years** of age. Most of these returning customers also travel by Business & Economy class, with very few traveling Economy Plus. About 53.53% of the returning customers travel **less than 1000 miles** in flight distance with 36% satisfaction rate. Therefore, the first action point could be to focus on **business & economy classes in shorter flights**. 
<img width="331" alt="image" src="https://user-images.githubusercontent.com/54994083/178770762-858f6b6c-e366-4e96-a861-ab93eb3af997.png">
<p text-align="justify">
If we zoom in on Economy fliers, traveling less than 1000 miles among returning customers (refer fig above), we can see that 'Ease of Online Booking' & 'In-flight Wifi Service' and 'Gate Location' have the least values of average score. So,  this would be a good starting point to work on:
  
    - Provide better online booking *instruction manuals* and *reduce the number of overall clicks* to complete a booking transaction
    - Provide a fixed volume of internet wifi in flight per device
    - Gate locations for shorter flights can be placed more strategically, and perhaps a map from the entrance to the gate location with time it takes to reach the           gate can be printed out on boarding passes as well as a online check-in confirmation emails. This way, it helps to plan better in advance.
   
2.  The second focus group would be the first-time customers. This group follows a pattern similar to returning customers, however, 'Departure and Arrival Time Convenience' is among the 3 lowest rated questions. It can be observed that **Cleanliness** is also rated low in both first-time & returning customers, and it could be improved with less cost, giving better returns in terms of customer retention & overall sentiment. 

3.  The decomposition tree for all the **dissatisfied, returning** customers reveals that most of them belong to the 35 to 60 age group , travelling economy for personal reasons. This group shows an approximately equal distribution of male and female passengers. Since the dataset consists of 82% returning customers, who have a high **dissatisfaction rate of close to 52%**, this could be the next focus group to work on. The **Food & Drink** category in this focus group shows low overall average score. Include **2 or 3 snack option** that come with *combo discounts* on **all flights except those longer than 4000 miles**.
