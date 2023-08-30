## Effect of Temperature on Crime Severity in Denver, CO

### **Background**
Crime and crime rates are significant societal and political concerns, impacting public safety, policy decisions, and various sectors. Discussions around crime data influence law enforcement assessments, city budgets, and political agendas, with crime statistics playing a pivotal role in elections. Despite national declines in crime, some regions like Denver experience rising crime rates, necessitating an exploration of contributing factors. One potential factor is ambient temperature, as research suggests it can influence human behavior and impulsivity. While a study links temperature and crime in Finland, investigating this relationship in Denver becomes crucial for policymaking aimed at reducing crime rates in the city.

### **Research Question and Hypothesis**
**Research Question:** Does temperature affect crime rates in the Denver area?
**Hypothesis:** As the temperature increases, Denver's crime rates will also increase. 
**Subquestions and Explorations:**
1. Descriptive statistics and plots of the cleaned data set
2. What is the monthly crime rate compared to the monthly average temperature?
3. How does the severity of the crime compare to the temperature?


### Data Overview

**Crime:** The primary data set revolves around the crime rates in Denver from Jan 2017 to Oct 2022. The data was retrieved from [Kaggle](https://www.kaggle.com/datasets/paultimothymooney/denver-crime-data) and openly sourced by [The Denver Open Data Catalog](https://www.denvergov.org/opendata/). It contains information on criminal offenses in the City and County of Denver gathered through the National Incident-Based Reporting System (NIBRS).<br>
**Weather:** Corresponding weather data for the Jan 2017 to Oct 2022 was retrieved and sourced from [The National Weather Service](https://www.weather.gov/wrh/Climate?wfo=bou).


### Data Cleaning

Several columns were removed from the `Crime` dataset, including geographic location, dates with insufficient data, and redundant columns. Column names were standardized, and the "first_occurrence_date" was parsed and renamed for clarity. The data type of "first_occurrence_date" was changed to datetime, and a "month" column was added for aggregation. Crime severity was assessed by categorizing crimes and harm levels. Duplicate "incident_id" values were retained for trend analysis. The `Weather` dataset also underwent column deletions and cleaning, with a focus on air temperature. After cleaning, `Crime` and `Weather` were merged using dates as the joining key.

### Descriptive Statistics and Analytics
The crime dataset has 399,572 offenses from Jan 2017 to Oct 2022. Among them are 14 offense categories (see Figure 1) and 195 offense types. The two most common offense categories are theft from motor vehicles (14.9%) and public disorder (14.8%). For all offenses, 98.7% had one victim, with the maximum number being 19.

<figure>
<img src=pdf/crime_vs_weather/offense_categories_count.png>
<figcaption>Figure 1. Offense Category ID with Total Counts of Offenses.</figcaption>
</figure>

Crime trends increased from 2019 to 2021 (see Figure 2). There was a dip in 2022, but this is due to our lack of data in 2022, with data truncating in October. Because if we visualize the number of monthly crimes in Figure 3, we can see that the number of crimes per month in 2022 was higher than in 2021. Therefore, if the trend continues, the total number of offenses that year will likely be higher than in 2021. This observation agrees with the trends in the Denver news, inciting an urgency to research causes and solutions to decrease the number of crimes.

<figure>
<img src=pdf/crime_vs_weather/total_number_offenses_per_year.png>
<figcaption>Figure 2. The total number of offenses per year from 2017 to 2022. The purpose of the figure is to show the trend of crimes over the five years.</figcaption>
</figure>

<figure>
<img src=pdf/crime_vs_weather/monthly_crime_count.png>
<figcaption>Figure 3. The monthly crime count in Denver from 2017 to 2022.</figcaption>
</figure>

The average temperature in Denver usually peaks around July to August every year and is at its lowest around December to February (see Figure 4). There is no noticeable difference between the temperatures per year. Additionally, they are highly correlated when observing the correlation between average, minimum, and maximum temperatures. Therefore, to analyze our research question, we will look at average temperature rather than at minimum and maximum temperature separately.

<figure>
<img src=pdf/crime_vs_weather/average_temperature_per_month.png>
<figcaption>Figure 4. Average temperature per month in Denver, CO. The graph plots month compared average temperature (F) every month.</figcaption>
</figure>

<figure>
<img src=pdf/crime_vs_weather/correlation_matrix_of_numerical_columns.png>
<figcaption>Figure 5. Correlation plot of temperature variables. There is a high correlation between average temperature with minimum and maximum temperature, warranting the use of average temperature for overall analysis.</figcaption>
</figure>

### Research Question Analysis

Our main question was if temperature affects crime rates in the Denver area. Therefore, we broke this down into two sub-questions.

#### 1. What is the monthly crime rate compared to the monthly average temperature?

The first sub-question examined how the monthly crime rate compared to the monthly average temperature. This was looked at in two different ways. We had incident ID as well as offense ID. Incident ID had duplicates, as one incident can mean a combination of different offenses. When looking at the monthly criminal incidents compared to temperature, there was a strong positive correlation (r = 0.79), meaning as the number of criminal incidents increases, so does temperature. However, January stands out with a crime increase disproportionately more considerable than the temperature change.

Additionally, in the latter half of each year, the relationship between crime and temperature weakens; crime begins to fall faster than temperature (see Figure 6). There was a stronger positive correlation when observing the average number of criminal offenses to the average temperature (r = 0.78). As temperature increases, so do criminal offenses and vice versa. The anomaly in January is still present when comparing the total number of criminal offenses to the average temperature (see Figure 7). Additionally, when observing the number of criminal offenses per incident, there is a weak, negative correlation (r = -0.27), meaning there lacks a relationship between temperature and the number of offenses committed per criminal incident (see Figure 8). So, two of the three correlations support a positive relationship between crime rates with temperature.

<figure>
<img src=pdf/crime_vs_weather/average_number_criminal_incidents.png>
<figcaption>Figure 6. Monthly average of criminal incidents compared to an average monthly temperature between 2017 to 2022. The data is averaged together by month per year.</figcaption>
</figure>

<figure>
<img src=pdf/crime_vs_weather/average_number_criminal_offenses.png>
<figcaption>Figure 7. Monthly average of criminal offenses compared to the average monthly temperature between 2017 to 2022. The data is averaged together by month per year.</figcaption>
</figure>

<figure>
<img src=pdf/crime_vs_weather/average_number_criminal_offenses_per_incident.png>
<figcaption>Figure 8. The monthly average number of criminal offenses per incident compared to the average monthly temperature between 2017 to 2022. The data is averaged together by month per year.</figcaption>
</figure>

#### 2. How does the severity of the crime compare to the temperature?

The second subquestion looked at how the severity of crime compares to temperature. We used two methods to observe severity. The first method was separating the crimes into violent, property, or other crimes. Violent crime in Denver is separated into murder, arson, sexual assault, robbery, aggravated assault, and robbery. Property crimes are theft from motor vehicles, burglary, auto theft, white-collar crimes, and larceny. The others category include public disorder, other crimes against persons, drug, and alcohol, and all other crimes. All crimes had similar average temperatures, but violent crimes did have a slightly higher average temperature of 54.56 degrees F (see Figure 9). When observing the different categories and their correlation to temperature, other crimes correlated 0.67, violent crimes correlated 0.92, and property crimes correlated 0.83. Therefore, violent crimes had the strongest correlation out of the three categories to average temperature, which means as the temperature rises so does the frequency of violent crimes.

<figure>
<img src=pdf/crime_vs_weather/average_temp_by_crime_category.png>
<figcaption>Figure 9. Average temperature grouped by crime category.</figcaption>
</figure>

ChatGPT suggested another way that we assessed severity. Instead of looking at offense category, which only has 14 categories, we looked at offense type, which has 195 unique types. ChatGPT separated them into high, medium, and low harm categories. The top 10 of each severity category are listed in Appendix F. High harm had the strongest correlation of 0.86 with average temperature, medium harm with 0.80, and low harm with 0.75 (see Figure 10). Using these two methods when the severity of the crime is high or the crime is more of a violent nature, there is a higher correlation with the trends of temperature.

<figure>
<img src=pdf/crime_vs_weather/harm_of_criminal_offenses.png>
<figcaption>Figure 10. The harm of criminal offenses compared to average temperature by month. The correlation values per line follow: High Harm: 0.86, Medium Harm: 0.80, Low Harm: 0.75</figcaption>
</figure>

### Conclusion and Future Research
In conclusion, based on the analysis of the crime and weather dataset in Denver from January 2017 to October 2022, the data indicates a positive correlation between crime rates and average temperature. As temperature rises, so does the number of criminal incidents or offenses, especially violent and high-harm crimes. Some data anomalies are observed, such as high incidences and offenses in January. Future research can dig deeper into why we see a drastic increase in January. With temperature becoming more of an issue during the summer months, it may be important for the city of Denver to enforce heat mitigation strategies to decrease the likelihood of crimes during the summer. Therefore, further applications of this initial analysis could be to dig into additional factors and complete statistical analysis to determine the impact of temperature on crime rates.