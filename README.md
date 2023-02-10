# CEO-vs-WorkerPay (project in progress)
Details of 3000+ top CEO salaries from Russell 3000 and S&amp;P 500 companies

## Introduction & Objectives

With the rising cost of living in the United States and a struggling financial and job market, compenstation is especially crucial in attracting and retaining employees. 

However, the determination of compensation package is often based by industry, company size, location, job title, and experience. This dataset gives an insight into the current state of median wages for the average worker at a given company and the current executive compensation. 

By shedding a light into this disparity, we can start to explore and visualize the relationship between CEO and worker pay and evaluate our definition of "fair wages" for our role within a industry. Analyzing this data is the first step toward having a basis on promoting pay equality.

## About this Data Set & Initial Cleaning

The initial dataset that I am using (ceo_data_pay_merged_r3000) provides information on the top 3000 companies in the United States, including the Russell 3000 and S&P 500 indices. The data includes 2175 unique values with company name, CEO name and salary, industry, company ticker, median worker pay and pay ratio information. Before full analysis, we'll need to import the appropriate python libraries to enhance our ability to manipulate and/or visualize this set. For this data set, I'll rename the columns and check whether the numeric columns are in floats to ensure easy maneuverability. 

Since this data table is pretty small, I didn't think using R or Python was necessary to perform the initial cleaning, so using Excel, I did a sweep of the data and removed some characters such as "%20" that were in the industry column, $ in median worker pay and salary. The pay_ratio column had contradicting data type formats, so to make the table a lot cleaner, I added a column to the end and remade the pay_ratio column using the provided ceo salary and median worker pay. This addition allowed me to see some worker pay values that were missing for Columbus Mckinnon Corp., CEVA, and Safehold, and I proceeded to eliminate those rows.
