# Temporal Variations of Auto Jobs-Accessibility by Time of Day in San Francisco


### Research Questions 


**How does auto jobs-accessibility vary by time of day?**

Jobs-Accessibility is a common transportation metric used in transportation analysis and research. It is a measure of the number of jobs that can be accessed from a certain location. Cevero defined “accessibility” within a regional context as “the opportunities to reach places across the region”. The “places” in jobs-accessibility measures are jobs, or more precisely, locations with jobs.  

Jobs-accessibility measures depend on three factors: the locations of people’s place of residence (origin), the locations of jobs (destination), and the time and cost to reach these jobs from people’s place of residence (impedance). Jobs-accessibility depends on both transportation and land use: the relative location of individuals and jobs matter.

Work on accessibility typically focuses on spatial variations. Spatial variations of accessibility point to the crucial connection between transportation and land use, it also shows disparate access to opportunities. 

A facet of accessibility that is less discussed but that is the impetus for this research is jobs-accessibility’s temporal aspect. The variability in travel conditions suggests that impedance never remains constant across time. Travel conditions change at different times of the day because of congestion. In times when congestion is severe, travel time increases and accessibility decreases.  

The operationalization of accessibility metrics in research and in professional practice often negates the temporal variability of accessibility by the time of day. Accessibility measures often have granularity at the daily level. Even sophisticated activity-based models such as SF-Champ account only for temporal variations of accessibility in 5 time periods per day instead of for all hours of the day. 

This analysis focuses on the time-of-day variations of jobs-accessibility. Ostensibly, people working in shifts that are not the typical 9am-5pm would have different levels of job access. Also, given the increasing hybrid and flexible nature of work, more workers may commute in different hours outside of the traditional peak hours. A more granular understanding of temporal variations can help us better understand travel behavior and access to job opportunities. 
 

**Are there opportunities to use big data to measure jobs-accessibility?** 

The Uber Movement dataset is a publicly available dataset collected and made available by Uber. Unlike traditional travel demand modeling in which travel time is determined from network impedance, the Uber Movement dataset is a form of big data based on actual trips. The Uber Movement dataset provides travel time estimates between census tracts based on their anonymized data on Uber trips. The granularity of the travel time data is at hour of day. 

The use of big data instead of network impedance calculations has a few advantages. First, they reflect actual travel behavior that has occurred and do not rely on assumptions and estimations of travel speed. Second, big data has a much larger sample size compared to the typical travel survey sample sizes used to validate travel demand models 

For my analysis, I will use Uber Movement’s weekday hour-of-day travel time data for the San Francisco Bay Area in 2019. 


### Scope (Specific Research Question) 

How does auto jobs-accessibility vary by time of day in San Francisco? 

### Data and Methodology 

There are a variety of metrics for accessibility. The most commonly used metrics are derived from either the cumulative model, gravity model, or utility-based model (1). Of the three types of models, the cumulative model was selected for this analysis because of its ease of use and interpretability. Specifically, I used a simple cumulative accessibility model that measures the aggregate number of jobs that can be accessed within a certain travel time. The accessibility metric is: 

- For each hour, the number of jobs accessible by car within x minutes, where x is: 15, 30, 45, 60, and 75 minutes 

The methodology of this analysis is tailored to the Uber Movement Data, which provides travel time between census tracts at an hourly granularity. Uber provides the geography of the zones and explicitly states that they are census tracts. However, Uber does not provide the census tract information in the dataset. Therefore, the Uber Movement data is first mapped to the corresponding census tract using census tract shapefiles from the Census Bureau. 

A disadvantage to using Uber Movement data is that data availability for each tract depends on the number of Uber trips that started, ended, or passed through the tract. Uber anonymizes the data and protects privacy by removing tract pairs (origins to destinations) that do not have a lot of Uber trips. As such, the dataset crucially lacks all possible origin-destination pairs within the San Francisco Bay Area. When assessing accessibility, this dataset cannot provide all possible jobs from within a certain travel time of one location but can only provide all jobs available in the dataset from within a certain travel time of one location, which is only a subset of all possible jobs.  

Since the availability of an origin-destination pair in the Uber Movement dataset depends on the number of Uber trips, the dataset is biased towards locations with more uber trips. Locations that have more uber trips will be more represented in this dataset and locations with fewer uber trips will be less represented. 

The origins and the destination tracts in the Uber Movement dataset are contextualized using Census demographic data and jobs projection data from the Metropolitan Transportation Commission (MTC). For the origins, Census demographic data from the 2016-2020 ACS is used to provide population, race/ethnicity, and median household income at the tract level. For the destinations, MTC’s 2020 job projections are used as an estimate for the number of jobs at the tract level. 

The analysis workflow began by examining the total number of jobs available in the dataset at a county level. This step identifies patterns in data availability. Next, the analysis focused on San Francisco County and examined the variations of jobs-accessibility under different travel time thresholds by hour of day. Lastly, spatial analysis was conducted to examine the coefficient of variation of jobs-accessibility by hour of day at the census tract level for San Francisco County. A coefficient of variation was calculated for each census tract in San Francisco County. The coefficient accounted for the standard deviation of jobs accessibility for each hour of day as a data point and normalized it by the average jobs accessibility for the census tract. The coefficient of variation measures the “volatility” of jobs accessibility from temporal variations at the census tract level. 

### Exploratory Data Analysis on Uber Movement Data Availability  
![Average number of destinations by county](/images/destinations_by_county.png)
![Average number of jobs by county](/images/jobs_by_county.png)

Figure 1 and Figure 2 above show the data availability of the Uber Movement dataset using two different metrics. In Figure 1, the metric used is the average number of destination tracts per origin tract for each Bay Area Counties. If all origin-destination pairs are available in the Uber Movement dataset at all hours of day, the metric should remain constant through the day. The metric is largely stable during the daytime, but dips drastically between 12am and 3am before recovering. The metric also tends to decrease past 6pm. 

These fluctuations were expected and confirm the concern that data availability is unstable by hour of day. More Uber trips occur during the daytime; hence data is relatively stable and available. During the early morning, the drastic reduction in data availability is likely due to the lack of Uber trips during those hours. Lastly, the evening spike that only occurred in San Francisco County may be a reflection of nightlife and nighttime activities in San Francisco. This increase above daytime average may potentially be due to longer trips made during those hours for nightlife and other nighttime activities, which captures more destination tracts.

Figure 2 shows the average number of auto-accessible jobs (at any distance) per tract for each Bay Area Counties. The trends shown in Figure 2 are similar to Figure 1. San Francisco County and San Mateo County have the highest average number of auto-accessible jobs per tract, followed by Alameda County. 

Based on Figure 1 and Figure 2, it is determined that the time period from 7:00am to 9:00pm is a relatively stable timeframe with stable data availability for accessibility analysis. Specifically, data from San Francisco County appears to be the most robust among the Bay Area Counties. Subsequent analyses, therefore, focus on the temporal variations between 7:00am and 9:00pm within San Francisco County.  

### Findings 
![Access by Time](/images/access_by_time.png)
![Percentage of Access by Time](/images/access_by_time_percent.png)

Figure 3 shows at the aggregate number of auto accessible jobs under different travel time thresholds for census tracts in San Francisco County. Since the top line is limited by data availability, Figure 4 normalizes the thresholds by the top line and shows the percentage of jobs reachable under different travel time thresholds for census tracts in San Francisco County. 

For both Figure 3 and Figure 4, travel time thresholds are shown at 15, 30, 45, 60, and 75 minutes. The gaps between the lines represent the jobs reachable between the travel time thresholds. Consistently throughout the day, the largest gaps are between 15 to 30 minutes, and between 30 to 45 minutes. Consistent with expectation, this means that most jobs are auto-reachable between 15 to 45 minutes. 

Two noticeable dips, representing a drop in the number of reachable jobs within a certain travel time threshold, are shown in the morning peak period at around 8am and in the afternoon peak period at around 3pm to 7pm. These are periods when congestion would increase travel time and therefore reduce jobs-accessibility. The drops appear to be larger in the afternoon peak period, suggesting that jobs-accessibility is most affected by traffic in the afternoon peak period. 
By comparing the travel time thresholds, the figures show two additional trends. First, the effect of the PM peak hour appears to cascade from higher travel time thresholds to lower travel time thresholds. The telltale sign of this phenomenon is the trough of the PM peak period for different periods. The first trough for the 75-minute threshold occurs at around 4pm, whereas the final trough for the 15-minute threshold occurs at around 5pm. Traffic congestion first affects access to jobs from far away, then gradually affect access to jobs closer to the origin. 

Second, the variability of jobs accessibility is more pronounced for the thresholds in the middle, compared to the lowest threshold (15 minutes) and the highest threshold (anytime). The variability for jobs accessible under 15 minutes is comparatively low, reflecting the limiting impact of traffic and roadway conditions on reaching jobs that are near the origin. On the other end, the variability for jobs accessible at any time is likely limited by data availability. For the 30-, 45-, and 60-minute thresholds, the variability appears to increase as the travel time threshold increases. This finding suggests that jobs that take longer to reach are more exposed to traffic congestion and are more impacted by it. 

**Geographic Distribution (A Tale of Three Cities) **

![Maximum number of jobs accessible by auto within 30 minutes](/images/sf_max.png)
![Coefficient of variation of auto jobs-accessibility under 30 minutes by time of day](/images/sf_var_norm.png)

Figure 5 shows the maximum number of jobs accessible by auto within 30 minutes for every census tract in San Francisco County. This represents jobs-accessibility under free-flowing traffic conditions. Figure 6 shows the coefficient of variation of auto jobs-accessibility under 30 minutes by time of day. For each census tract in San Francisco County, the time-of-day variation is normalized by the average number of jobs-accessible under 30 minutes by auto between 7:00am and 9:00pm. 

In unison, Figure 5 and Figure 6 tell a story of how many jobs can one reach within 30 minutes and how much variability exist in that level of job access. In San Francisco, jobs are concentrated in the downtown area of the city, which is located in the eastern portion of the city. The far western portion of the city, therefore, has a low number of jobs accessible. The far western portion of the city also has high variability in jobs-accessibility. This may be because their jobs-accessible relies on accessing the jobs in downtown San Francisco, and those jobs are not accessible within 30 minutes when traffic is congested. 

The central portion of the city has medium levels of job accessibility. However, it has also the lowest variability in jobs-accessibility. These areas of the city are close enough to downtown San Francisco that they can reliably access jobs in downtown San Francisco. However, those are also most of the jobs available to them because jobs in the East Bay and in San Mateo County are too far for them in 30 minutes. Therefore, they have low variability in jobs-accessibility. 

The eastern portion of the city and census tracts near freeways have a higher number of jobs accessible. Not only are they close to downtown San Francisco, but they also have easy freeway access to reach jobs in the East Bay and San Mateo County. Although they can reliably reach jobs in downtown San Francisco, their ability to access jobs in the East Bay and San Mateo County is dependent on traffic congestion. As such, they have a high number of jobs accessible and medium level of variability in job access, with the source of variability being access to jobs outside of San Francisco County. 

**Household Median Income and the Coefficient of Variation in Auto Jobs-Accessibility  **

![Coefficient of variation in job accessibility under 30 minutes and the household median income](/images/cov_income.png)

Figure 7 shows a plot of the coefficient of variation in job accessibility under 30 minutes and the household median income for all census tracts in San Francisco County. The plot shows a negative trend between the two variables. Census tracts with higher household median income tend to have lower variability in job access, and census tracts with lower household median income tend to have higher variability in job access. This correlation suggests that wealthier neighborhoods benefit from more stability in jobs-access throughout the day. The significance and implications of this finding remain to be further investigated. 


### Conclusion, Limitations, and Future Research 

The analyses above identified the following findings: 

1. Auto jobs-accessibility is most affected by traffic in the afternoon peak period.
2. Traffic congestion first affects access to jobs from far away, then gradually affect access to jobs closer to the origin, jobs that take longer to reach are more exposed to traffic congestion and are more impacted by it. 
3. The time-of-day variation of auto jobs-accessibility in San Francisco can be geographically divided into three parts of the city, with the westside having low auto jobs-accessibility and high variability, the center having medium auto jobs-accessibility and low variability, and the eastside having high auto jobs-accessibility and medium variability. 
4. There is a correlation between the time-of-day variability and median household income in San Francisco. Wealthier neighborhoods benefit from more stability in jobs-access throughout the day. 

These findings also show large temporal variations in accessibility and point to the importance of studying it. Temporal variations are an important component of accessibility and complement geographical variations. A better understanding of temporal variations in accessibility can allow us to better understand travel behaviors and equitable access to opportunities. 

The analysis also shows the limitations associated with using Uber Movement data. The instability in data availability and lack of all possible origin-destination pairs strongly limits the accessibility analysis that can be conducted and the findings that can be derived from it. In part because of these limitations, the analysis was only conducted for San Francisco County and for specific times of day. The Uber Movement data is also biased because it is based on past Uber trips, which is a subset of all trips that are not representative of the population. Therefore, the dataset is more robust for populations that more frequently use Uber and at locations that have more Uber trips. A different or more comprehensive dataset may produce different results and findings. 

Aside from data limitations, the methodology also has room for improvement. The use of cumulative accessibility metrics creates artificial boundaries in travel time and negates the differences in the ease of access within the travel time threshold. Gravity-based accessibility metrics may produce richer results. 

Accessibility matters not only for jobs. Future research can shed light on other access needs, such as access to food, access to recreational facilities and open space, and access to cultural resources. The diversity of the human experience is reflected in the diversity of travel; the opportunities to capture and understand diverse and complex access needs remain endless. 


### References 


Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/matthui1/access_variability/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
