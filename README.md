# Introduction
Intel, the semiconductor manufacturing powerhouse, is planning on building a new data center. Energy availability and usage are some of the key considerations Intel weighs when deciding where to construct a new data center. For example, which regions produce a surplus of energy, and are therefore more likely to provide energy at cheaper prices?  Which regions rely more on renewable energy sources?

In this project, co-designed with Intel's Sustainability Team, I was tasked with building dashboards and visualizations that provided the team at Intel with the best data-driven recommendations for where the optimal location for a new data center was. 

Before getting started, lets familiarize oursleves with some important terms in the data.

Links to Dashboards? Check them out on my Tableau Public Profile: [Data Center Sustainability Project 1](https://public.tableau.com/app/profile/thomas.eastin/viz/DataCenterSustainabilityProjectIntel/Dashboard), [Data Center Sustainability Project 2](https://public.tableau.com/app/profile/thomas.eastin/viz/DataCenterSustainabilityProjectIntel2/Dashboard2)

### Data Terms

***Balancing Authority*** - A Balancing Authority is responsible for maintaining the electricity balance within its region. This is a company that makes sure electricity is being exchanged between electric providers and regions so that no region runs out of electricity due to high demand.

***Data Date*** - The date the energy was produced.

***Local Time at End of Hour*** - The time after energy was generated, .e.g., energy generated between 1pm-2pm will show up as 2pm in this field.

***Demand*** - The energy demand on the grid (what the houses/business are using).

***Net Generation*** - The energy produced in the region by all sources e.g., wind, coal, nuclear, etc.

***All Petroleum Products*** - Energy generated from petroleum sources.

***Energy Source*** - The source of the energy produced, e.g., petroleum, solar, wind, etc.

***Percent Difference*** - A calculated field, created for you by the Intel team, that shows the change in energy based on the fields in the visualization.

***Region*** - The electric service area within a geographic area of the USA. e.g. California, Midwest, etc.

*NW* - Northwest<br />
*CENT* - Central<br />
*CAL* - California<br />
*TEX* - Texas<br />
*NY* - New York<br />
*MIDW* - Midwest<br />
*SW* - South West<br />
*TEN* - Tennessee<br />
*NE* - North East<br />
*SE* - South East<br />
*MIDA* - Mid-Atlantic<br />
*CAR* - Central America Region

# Background
Embarking on a data visualization project focused on locating the most environmentally sustainable location for an Intel data center aligns with both environmental stewardship and strategic business goals. Intel, as a global leader in technology, has a significant environmental footprint. By choosing to locate its data centers in the most environmentally sustainable locations, Intel can reduce its carbon emissions, water usage, and energy consumption. This aligns with the company's commitment to sustainability and corporate responsibility, enhancing its reputation as an environmentally conscious corporation.

The project supports global sustainability goals, such as those outlined in the United Nations Sustainable Development Goals (SDGs), particularly Goal 7 (Affordable and Clean Energy) and Goal 13 (Climate Action). By contributing to these goals, Intel reinforces its commitment to global sustainability initiatives, which can enhance its corporate image and appeal to environmentally conscious consumers and investors.

A data visualization project aimed at identifying the most environmentally sustainable location for a new Intel data center is a strategic initiative that supports environmental sustainability, cost efficiency, stakeholder engagement, and corporate innovation.

### Questions I am seeking to answer:

1. Which regions are net energy producers?
2. During which month is there the greatest energy surplus in the Mid Atlantic region?
3. What are the top 3 regions in the percentage of renewable energy generated?
4. What two regions have some form of renewable energy as the top source?
5. During what time of the day is California generating the most wind energy (what hours of the day is the percent difference > 0)?
6. What Region would you recommend Intel build their next data center?


### Tools I Used:
To successfully execute this project, I leveraged a combination of powerful tools that are integral to the field of data analytics. 

- **Tableau** was my primary tool for data visualizations construction, creating calculated fields, joining tables and minor data cleaning.
- For more thorough data transformation I used **Excel** formulas in order to optimize the data for more efficient and accurate visualizations.
- Version control was managed through **GitHub**, allowing for systematic tracking of changes, collaboration, and ensuring the integrity of the project's codebase.

These tools, when combined, enabled a smooth and efficient workflow, contributing to the project's overall success.

# My Analysis

### 1. Locate Net Energy Producers

My first task was to identify which regions were actual producers of net energy. Not all regions generate enough energy to meet the local demand. Some regions purchase power from other regions in order to supplement their energy requirememnts, while others sell their surplus to other regions in need.

I chose to create a bar chart of net energy producing regions in my first visualization (Net Production). In order to do this I first had to create a calculated feild called "Net Generation" to accurately visualize the comparisons:

```
SUM([Net Generation])-SUM([Demand])
```
I placed the bar chart in descending order based on regional net production of energy:

<img width="1676" alt="net_production" src="https://github.com/user-attachments/assets/0df0eafa-f71e-4855-9b35-7e0e5e58102d">

Here is a brief breakdown of my findings:

*Q*: Which regions are net energy producers? 

*A*: After creating the necassary calculated field to better visulaize the data, we can demonstrate that the only net producers of energy by region are the mid-atlantic, northwest, sowthwest, central and  southeast regions.

### 2.  Enegy Demand vs. Generation over Time

In my second visualization (Supply and Demand by Region) I chose to create a dual axis plot of Demand and Net Generation per a given time period. This would allow me to visualize the fluctuations in both energy production and demand over a specified time period (day, week, or month). Intel is primarily interested in regions with stable electricity demand and generation. Too much fluctuation will increase the cost of energy at certain time periods.

I first had to filter for regions and made sure to show the filter as a dropdown. In order to be able to specify the time period of the chart, I created a string parameter called "Select Period", which has the following parameters: day, week, month:

<img width="559" alt="select_period" src="https://github.com/user-attachments/assets/3df13b64-1ce1-42cd-bdca-e8e2a4c275f8">

I then created another calculated field called "Period" which included my string parameter:

```
DATETRUNC([Select Period], [Local Time at End of Hour])
```

I then created a dual axis plot with Demand and Net Generation pills, as well as Period. I was sure to use “Exact Date” for the Period field and to synchronize the axes:

<img width="1680" alt="supply_demand_region" src="https://github.com/user-attachments/assets/0bbde9a0-6b35-48fc-954d-cb7fd9e36c38">

Here is a brief breakdown of my findings:

*Q*: During which month is there the greatest energy surplus in the Mid Atlantic region?

*A*: August of 2022 saw the largest surplus in energy produced, achieving just under 4 million watts of energy production relative to what was needed that month.

**Note**: *After creating this visualization, you will see a dip in January 2023. This is because there is no data for that time period and not a sign that energy production fell dramatically.*

### 3. Greatest Percentage of Renewable Energy

For my third visualization (Renewable Energy), I created a bar chart showing which regions generated the greatest *percentage* of renewable energy.

**Note**: *Renewable energy is defined as any energy coming from solar, wind, and hydropower and pumped storage sources. All other sources do not count as renewable energy.*

For this I created a calculated field called "Renewable Energy", which is the sum of Wind, Solar, and Hydropower and Pumped Storage fields:

```
SUM([Solar]) + SUM([Wind]) + SUM([Hydropower and Pumped Storage])
```

I then created another calculated field called "Renewable Percentage" to obtain the percentage of renewable energy sources within Net Generation:

```
100 * ([Renewable Energy])/SUM([Net Generation])
```

Finally I visualized a bar chart in descending order of regions with the most renewable energy percentage.

<img width="1680" alt="renewable_energy" src="https://github.com/user-attachments/assets/49dcd24c-b487-43a1-b098-6f6b42b5a71f">

Here is a breif breakdown of my findings:

*Q*: What are the top 3 regions in the percentage of renewable energy generated?

*A*: In order, the top three regions with the highest percentages of renewable energy resources are the northwest, central and California regions.

### 4. Energy Compostition by Region

For the next visualization (Utility Power Source Breakdown), I thought a tree map would be the best way to summarize the mixture of different energy sources based upon different regions and balancing authorities. This tree map shows the energy breakdown of a region meaning that for each specified region, it demonstrates the composition of its energy sources.

I went about createing a tree map by first creating a bar chart of Energy Source and Energy Generated (MW). Afterwards I simply converted it to a Tree Map via the "Show Me" pane feature within Tableau. Finally, I made sure to filter by Region and show the dropdown menu on the Dashboard:

<img width="1680" alt="energy_source_region" src="https://github.com/user-attachments/assets/00fc6379-d054-40c5-aff9-07615f0ea03b">

Here is a breif breakdown of my findings:

*Q*: What two regions have some form of renewable energy as the top source? Cycle through the different regions to find your answer.

*A*: Out of all of the regions being analyzed, only two have proven to be successfully at establishing a form of renewable energy as their primary energy resource. Those regions are central America (wind) and the northwest (hydropower).

### 5. Hourly Difference in Generation

My fifth visualization (Hourly Difference in Generation) is composed of a line chart showing the percentage difference in energy generation from the previous hour. This type of chart helps identify trends such as sudden spikes or dips in energy generation, which in turn can help plan when to perform power-intensive operations at the data center.

Given that this line chart relied on specific times of day, I decided to create two seperate calculated fields called "Period" and "Percentage Difference" which both allowed me to ensure that the correct times were being adjusted when filtering through different regions:

Period
```
DATETRUNC([Select Period], [Local Time at End of Hour])
```

Percentage Change
```
ABS(LOOKUP(ZN(SUM([Energy Generated (MW)])), -1))
```

I made sure to aggregate the local time down to the hour of day and filter the data by both region and energy source:

<img width="1680" alt="hourly_difference_generation" src="https://github.com/user-attachments/assets/ca7fbe1c-5234-43cb-979a-9262904f0d98">

Here is a breif breakdown of my findings:

*Q*: During what time of the day is California generating the most wind energy (what hours of the day is percent difference > 0)?

*A*: Wind energy production within California reaches above the 0% threshold around 11:30am and achieves peak production by 3pm. It then falls underneath the 0% threshold by 10pm.

### 6. Data Center Regional Recommendation

For my final visualization (Energy Source By Region) I chose to create a line chart of *all* sources of energy per region during a selected period. I made sure to assign each energy source with their own respective color, allowing the user to compare the relative proportions of each energy source in the selected region over the selected period. I made sure to use the same "Select Period" parameter as before in order to select between the day, week, or month:

<img width="1680" alt="energy_source_region_period" src="https://github.com/user-attachments/assets/55bb4b30-2ab5-4fcf-9162-022df8ade2b3">

## Final Recommendation

*Q*: Given what you have created with your visualizations, what region would you recommend the next Intel data center be built?

*A*: To better make the appropriate data-driven recommendations as percise as possible, I will be keeping in the forefront of my decision-making the overall objectives of Intel's substainability team. That goal being to build a new data center within a region that has the highest net energy production, at the lowest cost and with the most amount of diverse renewable energy resources. As the Net Production chart shows, Intel has at the most, five seperate regions that are able to achieve some level of positive energy production. Meaining that the amount of energy demanded is not offsetting the amount of energy being produced. We can see that the mid-atlantic region is number one on this list which would make one think the MIDA would be the number one candidate for the spot. However, when looking at the Renewable Energy bar chart we can clearly see that the mid-atlantic region ranks among the *lowest* regarding the overall percentage of renwable energy produciton.

Eliminating the mid-atlantic from the running the only other region that has proven to meet all of the desired metrics of sustainability is that of the northwest. Eventhough the northwest ranks slightly below the mid-atlantic in terms of overall net production, they far exceed most other regions in terms of renewable energy percentages. On top of this, the northwest is able to achieve this amount of energy production from renewable energy resources; primarily hydropower. Digging into the data a little further we can recommend further insights as to the best time of day to place an optimal load on the future data center to be at both 7am and 5pm, given the trend in energy production throughout the day in the overall northwest. 

# What I Learned

Deciding to embark upon this analytical endeavor I've successfully integrated Tableau visualizations within my data analytical toolbelt:

***Data Connectivity and Preparation***: Tableau enables you to connect to multiple data sources, including spreadsheets, databases, cloud services, and more. Throughout this project I was able to learn how to clean, blend, and aggregate data from multiple sources to demonstrate a unified data set ready for analysis. This includes mastering features like data joins, unions, and data blending.

***Calculation and Scripting***: Tableau includes a powerful formula language that lets you create calculated fields for custom metrics, ratios, and other derived data points. I was able to master these calculations by performing custom analytics within this project that ensured my visualizations reflected the specific needs of my analysis.

***Dashboard and Storytelling***: Designing interactive dashboards and telling data-driven stories is the primary reason why many data professionals utilize Tableau as their go-to visualization software. While completing this project I was able to learn how to design dashboards that guide users through a narrative, using filters, actions, and drill-down features to create a dynamic and compelling story that highlights key business insights.

***Establishing Parameters within Visualizations*** I was able to leverage parameters as a powerful tool which enhanced the interactivity, flexibility, and depth of my data visualizations. They will enable the users of these dashboards to explore different scenarios, dynamically adjust views, and conduct more nuanced analyses.
