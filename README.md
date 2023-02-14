# CEO-vs-WorkerPay (project in progress)
Details of 3000+ top CEO salaries from Russell 3000 and S&amp;P 500 companies

## Introduction & Objectives

With the rising cost of living in the United States and a struggling financial and job market, compenstation is especially crucial in attracting and retaining employees. 

However, the determination of compensation packages is often based by industry, company size, location, job title, and experience. This dataset gives an insight into the current state of median wages for the average worker at a given company and the current executive compensation. 

By shedding a light into this disparity, we can start to explore and visualize the relationship between CEO and worker pay and evaluate our definition of "fair wages" for our role within a industry. Analyzing this data is the first step toward having a basis on promoting pay equality.

### Q's
1. How much do CEO salaries vary across industries?
2. Is there an industry with higher CEO salaries than others? Median worker pay?
3. Can we find a cluster of companies or industries that practice similar pay practices based on service provided and median worker pay?

## About this Data Set & Initial Cleaning

The initial dataset that I am using (ceo_data_pay_merged_r3000) provides information on the top 3000 companies in the United States, including the Russell 3000 and S&P 500 indices. The data includes 2175 unique values with company name, CEO name and salary, industry, company ticker, median worker pay and pay ratio information. Since this data table is pretty small, I didn't think using R or Python was necessary to perform the initial cleaning, so using Excel, I did a sweep of the data and removed some characters such as "%20" that were in the industry column, $ in median worker pay and salary. The pay_ratio column had contradicting data type formats, so to make the table a lot cleaner, I added a column to the end and remade the pay_ratio column using the provided ceo salary and median worker pay. This addition allowed me to see some worker pay values that were missing for Columbus Mckinnon Corp., CEVA, and Safehold, and I proceeded to eliminate those rows.

Before full analysis, we'll need to import the appropriate python libraries to enhance our ability to manipulate and/or visualize this set. For this data set, I'll rename the columns and check whether the numeric columns are in floats to ensure easy maneuverability. 

## Data Exploration and Visualization

For the exploratory data part of this mini project, I decided to load up Jupyter Notebooks in *Visual Studio Code* and use Python for the entire section. Below you can find the code, but for the Jupyter Notebook file, feel free to go through my repository.

<details><summary>Code</summary>
<p>


```
import matplotlib.pyplot as plt
import seaborn as sb
import numpy as np
import pandas as pd
from mpl_toolkits.axes_grid1.inset_locator import inset_axes

  
  salary = pd.read_csv('ceo_data_pay_merged_r3000.csv')
salary = salary.rename(columns={
    'ticker':'Ticker',
    'company_name': 'Company Name',
    'median_worker_pay': 'Median Salary',
    'pay_ratio': 'Ratio',
    'ceo_name' : 'CEO',
    'salary' : 'CEO Salary',
    'industry' : 'Industry'
})

salary[['Median Salary', 'CEO Salary']] = salary[['Median Salary', 'CEO Salary']].astype('float')
salary['CEO Salary (Thousands)'] = salary['CEO Salary'] / 1000
  
salary.head()
salary.dtypes  

print(salary.corr())
  

dataplot = sb.heatmap(salary.corr(), cmap="YlGnBu", annot = True)
##quick heatmap does not give any useful information due to it being a small data set with mostly non quantifiable data   
  
#setting color palette for seaborn graphs

sb.set_palette('rocket')
sb.set_style('darkgrid')
sb.set_context('notebook')

#setting subplots for a whole data figure to display different data inferences

fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize = (27,15))
fig.suptitle('Exploratory Data Analyis', fontsize='35')

sb.countplot(y='Industry', data=salary, ax=ax1, palette='rocket')
ax1.set_xlabel('Number of Companies')
ax1.set_ylabel(None)
ax1.set_title('Number of Companies by Industry')

sb.barplot(y='Industry', x='Ratio', data=salary, ax=ax2, orient="h", errorbar=None, palette='rocket')
ax2.set_ylabel(None)
ax2.set_title('Pay Ratios by Industries')

sb.stripplot(y='Industry', x='CEO Salary (Thousands)', data=salary, ax=ax3, palette='rocket')
ax3.set_title('CEO Salary by Industry')
ax3.set_ylabel(None)
ax3.set_xlim(0,300000)

#adding an inset to my subplot for Jeff Green's salary which overshadows the distribution of the rest of the salaries
axins = inset_axes(ax3, width=3.5, height=1.5, loc=4, borderpad=3.5)
labels=[5000000,6000000,7000000,8000000,9000000]
sb.stripplot(y='Industry', x='CEO Salary (Thousands)', data=salary, ax=axins)
axins.set_xlim(500000,900000)
for axi in [axins]:
    axi.set_xlabel(None)
    axi.set_ylabel(None)
    axi.get_yaxis().set_visible(False)
axi.annotate(
        'J. Green (Comm. Services)', xy=(834000,2.3), xytext=(350000,6),
        arrowprops=dict(facecolor='black', shrink=0.05)
    )

sb.scatterplot(y='CEO Salary (Thousands)', x='Median Salary', hue='Industry', data=salary, ax=ax4, marker='.', palette='rocket')
ax4.ticklabel_format(useOffset=False, style='plain')
ax4.set_xlim(0,130000)
ax4.set_ylim(0,350000)
ax4.set_title('CEO Salary vs Median Salary')


plt.show()  
  
 ```
![image](https://user-images.githubusercontent.com/72219431/218628703-24a7e275-1b43-4c68-9654-2b85c617a513.png)

```

  
```
</p>
</details>

## Current Conclusions

## Future Work

While this was good practice to examine the inital findings of CEO vs Worker pay, some good additional data to include would be state originiation for each company and figure out if there is any correlation on ceo/worker ratio compared to their operating state and cost of living for the majority of workers.  
