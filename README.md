# The Analysis

## 1. What are the most demanded skills for the most popular  data roles in MENA region?
To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

view my notebook with detailed steps here: [2_Skills_Count.ipynb](3_Project\2_Skills_Count.ipynbb)

### Visualize Data
```python
fig,ax = plt.subplots(3,1)

sns.set_theme(style = 'ticks')

for i,roles in enumerate(job_roles):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == roles]
    sns.barplot(data = df_plot, y= 'job_skills', x= 'skill_percentage', ax = ax[i], hue = 'skill_count', palette = 'dark:b_r')

    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_title(roles)
    ax[i].set_xlim(0,88)

    for n,v in enumerate(df_plot['skill_percentage']):
        ax[i].text(v+1, n , f'{v:.0f}%', va= 'center')
        
    if i != 2 :
        ax[i].set_xticks([])

fig.tight_layout(h_pad=1, rect=[0, 0, 1, 0.95])
fig.suptitle('Likelihood Skills Requested in Job Postings For MENA Region', fontsize = 15)
plt.show()
```
### Results
![Visualization Of The Most Damanded Skills For Top Data Roles In MENA Region](3_Project\Images\Most_Demanded_Skills_Chart.png)

### Insights
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (78%) and Data Engineers (63%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 63% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

## 2. How are in-demand skills trending for Data Analysts in MENA region?

### Visualize Data
```python
sns.lineplot(data = df_plot, dashes = False, palette = 'tab10')
sns.set_theme(style = 'ticks')
sns.despine()

for i in range(5):
    plt.text(11.2,df_plot.iloc[-1,i],df_plot.columns[i])

from matplotlib.ticker import PercentFormatter

ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals= 0))

plt.title('Trending Top Skills For Data Analysts In MENA Region')
plt.legend().remove()
plt.xlabel('2023')
plt.ylabel('Likelihood In Job Posting')
```


### Results
![Trending skills for data analysts in MENA region](3_Project\Images\Skills_Trending.png)


### Insights
• SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.

• Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.

• Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

