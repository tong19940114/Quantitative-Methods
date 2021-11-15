#### What are the distinctions of the relationship between different proportion of budget in six areas of childhood obesity interventions and changes in childhood obesity rates(consider regional variations)?

**Introduction**

There has been considerable different views of academic research on tackling childhood obesity in the England, such as Mears et al focus on the environment as an intervention(Meghann Mears et al. 2020), Wilkie et al concentrate on the effectiveness of health training(Wilkie, Hannah J et al. 2017). However, few research has paid attention to the different performance of same interventions applied in various regions. Considering the significant differences in life expectancy and economic levels in different regions of England (especially between south England and north England)(Buchan et al. 2017), I will use geographical boundaries as a classification criteria to divide England as four parts(including North, Midlands, South exclude London, London). According to this classification criteria, I will analyse the relationship between different proportion of budget in six areas of childhood obesity interventions and changes in childhood obesity rates over the decade. 

 **1. Data**

This essay uses data from London Datastore, a website created by the Greater London Authority (GLA), providing free data relating to the capital and other zones in England. In this essay, the data used for analysis contains the population and the number of obese children, nine regions of England, five types of local authorities, the annual budget for tackling childhood obesity allocated by local authorities across England over the period 2008 to 2018. Among the budget, local authorities distribute it across six different areas by varying proportions. 

For further analysis, to calculate these original data columns, some extra columns including the amount of change in childhood obesity rates over the decade, each area as a proportion of the total budget were added into the datasets. 

 **2. Methodology**

**2.1 Software and Programming Tools**

The software Excel, the programming language Python and its packages were used to tidy data, establish regression models and visualise results. All data and tools are available in Github: https://github.com/tong19940114/Quantitative-Methods/blob/main/QM_assessment.ipynb.

**2.2 Classification Criteria**

At the stage of initial observation of the datasets,  a distinctive feature relating to geographical divisions was noted. Before London was removed from South, its change in obesity rates affected the whole South part significantly so that the change of childhood obesity rate in South cannot be a normal distribution. But after removed London, rate of South was more similar to a normal distribution, and rate of London as so on (Fig. 1). Thus to facilitate the subsequent construction of the statistical model, England will be divided into four regions.

<img src="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\Density_change_in_rate(10^4)_3parts.png" alt="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\Density_change_in_rate(10^4)_3parts.png" style="zoom:30%;" />

Fig.1: density distribution plot of change of childhood obesity rate(2008 to 2018) in four England parts (To make the degrees of the x-axis easy to identify, the rate here has been scaled up by a factor of 10^4, without affecting the characteristics of the data distribution)    

**2.3 Recognise Outliers** 

Before analysing data, missing data and outliers in datasets need to be detected(Rousseeuw, P.J. and Hubert, M. 2011). By using python to produce boxplots of data, the outliers were observed, and by analysing the causes of outliers, then retention and exclusions were chosen (Fig. 1). In the datasets, the data of Isles of Scilly in South West were recognised as outlier since its local authority spend all budget in single area (Table. 1), values of other budget areas were far removed from the mass of data. Other outliers, due to differences in population size which not directly related to the research, were reserved for next analysis.                           

| <img src="C:\Users\nekopi\AppData\Roaming\Typora\typora-user-images\image-20211113233714108.png" alt="image-20211113233714108" style="zoom:33%;" /> | <img src="C:\Users\nekopi\AppData\Roaming\Typora\typora-user-images\image-20211113233745879.png" alt="image-20211113233745879" style="zoom:45%;" /> | <img src="C:\Users\nekopi\AppData\Roaming\Typora\typora-user-images\image-20211114215739331.png" alt="image-20211114215739331" style="zoom:33%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Fig. 2a: Box-plot of six areas with outliers                 | Fig. 2b: Box-plot of six areas remove outliers               | Fig. 2b: Box-plot of six areas remove outliers(England divided into four parts) |

| **Local authority area** | **……** | **2008-2018_rate**  **_of_fatness** | **total**   **budget** | **clean air** | **……** | **School awareness** | **School_**  **awareness proportion** | **……** |
| ------------------------ | ------ | ----------------------------------- | ---------------------- | ------------- | ------ | -------------------- | ------------------------------------- | ------ |
| Isles of Scilly          | ……     | -0.07%                              | 2000                   | 0             | ……     | 2000                 | 100.00%                               | ……     |

Table. 1: the raw of outlier in datasets

**2.4 Building the Multiple Linear Regression Model**

To investigate that the relationship between the proportion of six areas in total funding and childhood obesity rates over ten years, and how the relation display differently in each part of England, it was required to determine a statistic model to describe the datasets. Considering that the research has one dependent variable (the change of England childhood obesity rates over ten years) and six independent variables, the multiple linear regression could be built to interpret the strength of the relationship between them. 

The formula for a multiple linear regression is:
$$
y 
​
 =β 
0
​
 +β 
1
​
X
1
​
 +β 
2
​
X
2
​
 +...+β 
m
​
X
m
​
 +ϵ
$$
where y is the predicted value of the dependent variable, β0 is the y-intercept, β1X1 is the regression coefficient (B1) of the first independent variable (X1). βmXm means the regression coefficient of the last independent variable(Thomas P. Ryan, 2009) ( in this research, before using VIF to remove some independent variables, n should equal to 6 ). Besides, + or - indicates whether the correlation is positive or negative. ϵ represents model error.

Before calculate the regression formula, it should be confirmed that each independent variable is independent to others (in other words, there is no multicollinearity)(Thomas P. Ryan, 2009). Thus variance inflation factor (VIF) as a measuring tool is used to examine the severity of multicollinearity in the multiple linear regression model. Python provides packages to identify those independent variables with multicollinearity,  ignore them, output a summary including important parameters. In this research, the dropped independent variables are different in different parts ( Table. 2)

| Part                | Dropped Independent Variables   |
| ------------------- | ------------------------------- |
| whole England       | proportion of clean environment |
| North               | proportion of clean environment |
| Midlands            | proportion of clean environment |
| south except London | proportion of school awareness  |
| London              | proportion of clean environment |

Table. 2: the dropped independent variables

**3 Results**

| <img src="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\dropped\north_multi_plot.png" alt="north_multi_plot" style="zoom:33%;" /> | <img src="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\dropped\mid_multi_plot_1.png" alt="mid_multi_plot_1" style="zoom:33%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Fig. 3a: linear regression plot of proportions of six areas and change in obesity rates in North region | Fig. 3b: linear regression plot of proportions of six areas and change in obesity rates in Midlands region |
| <img src="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\dropped\south_ex_ld_multi_plot_1.png" alt="south_ex_ld_multi_plot_1" style="zoom:33%;" /> | <img src="C:\Users\nekopi\OneDrive\CASA\21-22 term 1\0007 quantitative methods\assesment_1\plots\dropped\London_multi_plot.png" alt="London_multi_plot" style="zoom:33%;" /> |
| Fig. 3c: linear regression plot of proportions of six areas and change in obesity rates in South region exclude London | Fig. 3d: linear regression plot of proportions of six areas and change in obesity rates in London region |

| Region              | R-squared | Adjusted R-squared | F-statistic | p-value | coef    | **std err** |
| ------------------- | --------- | ------------------ | ----------- | ------- | ------- | ----------- |
| whole England       | 0.094     | 0.062              | 2.998       | 0.010   | 4.0351  | 1.551       |
| North               | 0.302     | 0.223              | 3.810       | 0.175   | 2.6075  | 1.892       |
| Midlands            | 0.614     | 0.500              | 5.438       | 0.005   | 6.0810  | 1.903       |
| south except London | 0.410     | 0.334              | 5.419       | 0.003   | -0.0005 | 0.000       |
| London              | 0.511     | 0.420              | 5.633       | 0.001   | 8.1784  | 2.259       |

Table. 3: Summary multiple linear regression analysis

According to Table. 3, p-value of North is larger than 0.05, which means  the model does not build successfully, so its result is invalid. Besides, according to Adjusted R-squared, it can be suggested that the model of whole England region is not explain the relationship effectively. 

Therefore, the results for the remaining three regions can explain the relevance between changes of obesity rates and proportions of each areas in funding to a certain extent.

| Region                | Negative Correlation Areas                   | Positive Correlation Areas                                   |
| --------------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Midlands              | Clean Air, Health Training, School Awareness | Media Awareness,  Sub-counselling                            |
| South Excluded London | Sub-counselling                              | Media Awareness, Health Training, Clean Air, Clean Environment |
| London                | Clean Air,  School Awareness                 | Media Awareness, Sub-counselling, Health Training            |

Table. 4: correlations between proportions of each areas and changes of childhood obesity rates in different regions

| Region                | coef of Media Awareness |
| --------------------- | ----------------------- |
| Midlands              | 2.3640                  |
| South Excluded London | 0.0017                  |
| London                | 3.8820                  |

Table. 5: coef of Media Awareness in different regions

As Table. 4 demonstrated, funding invested in Media Awareness is the only one which has positive correlation with obesity rates in all three region. As Table. 5 shows, compared to other regions, each 1% increase in proportion of media awareness has a much smaller impact on obesity rate than the other two regions. Besides, funding invested in Sub-counselling only in South region(excluded London) has negative correlation.

**4 Conclusion and Further Directions**

According to the analysis above, we can confirm that in the different regions in England, the correlation we researched presented different features. However, due to the lack of data, we cannot discuss further what makes these distinctions. In addition, due to the correlation between proportions of each areas and childhood obesity rates is not strong enough, our model is unable to describe the relationship between variables more accurately (as reflected by the lower values of R^2). We also find, if the parts studied narrowed down, the resulting models describe the relationships between the data better (e.g. London and midlands contain fewer cities compared to South(excluded London), and  R^2 in their models is larger). Besides, as a direction for improvement, perhaps we could transform the region information into categorical data to strengthen the correlation between the variables and thus obtain a better model. 

Count: 995



**References**

Mears, M. et al., 2020. Neighbourhood greenspace influences on childhood obesity in Sheffield, UK. Pediatric obesity, 15(7), pp.e12629-n/a.

Wilkie, H.J. et al., 2018. Correlates of intensity-specific physical activity in children aged 9–11 years: a multilevel analysis of UK data from the International Study of Childhood Obesity, Lifestyle and the Environment. BMJ open, 8(2), p.e018373.

Buchan et al (2017). North-South disparities in English mortality 1965–2015: longitudinal population study. Journal of Epidemiology and Community Health 71, 928-936.

London Datastore, Prevalence of Childhood Obesity, Borough, Ward and MSOA. online avaliable at: https://data.london.gov.uk/dataset/prevalence-childhood-obesity-borough, retrived on August 1, 2020.

Rousseeuw, P.J. and Hubert, M. (2011), Robust statistics for outlier detection. WIREs Data Mining Knowl Discov, 1: 73-79.

RYAN, T.P. (2008). Introduction to Multiple Linear Regression. In Modern Regression Methods, T.P. RYAN (Ed.), 146-177.



