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

### Tools I Used:
To successfully execute this project, I leveraged a combination of powerful tools that are integral to the field of data analytics. 

- **Tableau** was my primary tool for data visualizations construction, creating calculated fields, joining tables and minor data cleaning.
- For more thorough data transformation I used **Excel** formulas in order to optimize the data for more efficient and accurate visualizations.
- Version control was managed through **GitHub**, allowing for systematic tracking of changes, collaboration, and ensuring the integrity of the project's codebase.

These tools, when combined, enabled a smooth and efficient workflow, contributing to the project's overall success.

# My Analysis
