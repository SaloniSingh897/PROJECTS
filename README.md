
# Panic Attack -Dashboard


A brief description of what this project does and who it's for:
## Problem Statement

This dashboard has been designed to help healthcare professionals and researchers better understand the patterns and severity of panic attacks among individuals. By analyzing key variables such as age, gender, panic attack frequency, duration, trigger reasons, and physiological symptoms (e.g., heart rate, sweating, dizziness, chest pain, trembling, shortness of breath), the dashboard aims to identify common patterns and contributing factors.

The report also considers lifestyle-related factors like caffeine intake, alcohol consumption, smoking habits, exercise frequency, sleep hours, therapy, and medication use, which may influence the intensity and occurrence of panic attacks.

One of the main objectives is to analyze how these factors impact the panic score and evaluate which demographic groups (e.g., based on age or gender) are more vulnerable. The dashboard also enables a comparison of panic attack severity with individual habits and health conditions, helping to reveal hidden correlations.

For instance, if individuals with lower sleep hours and high caffeine intake consistently show higher panic scores and longer panic durations, this could guide interventions. Similarly, symptoms such as shortness of breath, sweating, or trembling can be tracked to understand their frequency across various age groups and triggers.

By using this dashboard, mental health practitioners can:

*Identify high-risk individuals based on lifestyle and symptom patterns.
*Recommend targeted therapies or behavior changes.
*Monitor the effectiveness of current treatments or preventive strategies.


Ultimately, this report supports data-driven mental health insights, aiming to improve early detection, intervention, and treatment planning for those suffering from panic attacks.


### Steps followed 

Step 1: Data Loading
Loaded the dataset into Snowflake.
Connected Snowflake to Power BI Desktop for reporting.

Step 2: Initial Data Exploration
Used Snowflake SQL for preliminary data understanding and schema validation.


Step 3: Data Profiling in Power BI
Opened Power Query Editor.
Enabled Column Distribution, Column Quality, and Column Profile under the View tab.


Step 4: Data Cleaning & Transformation
Verified and adjusted data types for all columns.
Replaced blank values with 0.
Converted categorical variables into numeric format.

Step 5:
Created a conditional column for Panic Score Category:

< 4 → “Low”,

> 8 → “High”,

else → “Medium”.
Snap of new created column: <img width="164" height="705" alt="Image" src="https://github.com/user-attachments/assets/69917389-cab1-4dd5-9600-0f32373079e8" />
 

Step 6:
Updated the Heart Rate column by reducing each value by 1.

Step 7:
Designed a visual page:
Created and formatted a bar chart showing patients with dizziness.
Duplicated and modified the chart to show patients with:

1. Trembling
2. Sweating
3. Shortness of breath
4. Chest pain
as symptoms they reported during panic attack.
Enhanced visuals using the Format Visuals pane.
Snap short of second report page:<img width="1259" height="786" alt="Image" src="https://github.com/user-attachments/assets/2342e212-af4f-449b-9472-8865739cf5bc" />

Step 8: Report Page Formatting
Created a second report page for symptom analysis.
Applied custom background image and consistent formatting.
Arranged visuals for clear and appealing presentation.


Step 9: Interactive Filters (Slicers) Setup
Renamed the page to “Other Requirements”.
Applied the same page formatting as previous pages.
Added and formatted slicers for interactivity:
1.Panic Score Category (new conditional column)
2.Gender
3.Trigger Reason
4.Medical History
Snap short of third report page:<img width="1289" height="775" alt="Image" src="https://github.com/user-attachments/assets/71ad8b92-57ee-4cb1-a3e9-232ba9cbd980" />



Step 10: Additional Visualizations
On the same page:
Created a line chart showing number of patients by Drinks Per Day and formatted it.
Added two more charts:
Average Sleep Hours per patient
Panic Attack Duration (minutes) per patient
Applied appropriate labels, legends, and titles.


Step 11: DAX-Based Calculations
Created a new column using DAX:

Age Group = IF('Panic_attack_data'[Age] <= 17, "Child",
          IF('Panic_attack_data'[Age] <= 24, "Adolescent",
          IF('Panic_attack_data'[Age] <= 64, "Adult", "Senior")))
Snap shot of newly created column:<img width="97" height="690" alt="Image" src="https://github.com/user-attachments/assets/c171a383-8d8a-4a21-a6b7-ea8189ba24ef" />

Created a DAX measure to calculate the percentage of patients with dizziness during panic attacks:

Percentage Patients Dizziness = 
DIVIDE(
    COUNTROWS(
        FILTER(
            'Panic_attack_data',
            'Panic_attack_data'[dizziness] = TRUE()
        )
    ),
    COUNTROWS('Panic_attack_data'),
    0
) * 100

Placed the measure inside a blank card visual for display.



---

Step 12: Age Group Analysis Page
Created a new report page named “Age Group Analysis”.
Designed a clustered bar chart to compare:
Average Sleep Hours
Average Panic Score
Average Panic Attack Frequency

Visuals segmented by:
Age Group 
Trigger Reason
Applied formatting for clarity and presentation consistency.
Snap shot of last report page:
<img width="1244" height="677" alt="Image" src="https://github.com/user-attachments/assets/c11325db-6e71-449f-a70f-f3cdbd729684" />


# Insights

A four page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of patients= 1200
Dashboard Insights: Number of Patients by Symptoms

This section of the report provides a summary of key physiological symptoms experienced by patients during panic attacks. Based on a total dataset of 1,200 patients, the following insights have been drawn:

Symptom-Wise Distribution

Symptom	Patients Reporting  Count	      Percentage of Total Patients

Dizziness	                 620 	                51.7%
Trembling	                 590	                49.2%
Sweating	                 836	                69.7%
Chest Pain	               487	                40.6%
Shortness of Breath        746	                62.2%


Key Observations

1. Sweating is the most commonly reported symptom, affecting approximately 69.7% of the patients.


2. Shortness of breath is also highly prevalent, observed in 62.2% of individuals.


3. Dizziness and trembling are experienced by nearly half of the patients (51.7% and 49.2% respectively).


4. Chest pain, while still significant, is the least commonly reported among the five symptoms, with 40.6% of patients experiencing it.


5. The high occurrence of multiple symptoms suggests a strong physiological response during panic attacks, highlighting the need for targeted medical and psychological interventions.

  


 ### Some other insights
 

 This dashboard explores the relationship between various lifestyle factors and panic attack characteristics such as panic score, gender, medical history, and trigger reasons. The visualizations aim to provide an understanding of how different variables may influence panic attack severity and frequency.

1. Sleep Hours vs. Number of Patients

The chart indicates that patients with fewer sleep hours (around 6 hours/week) are more commonly affected.

As sleep hours increase, the number of patients drops significantly, suggesting a negative correlation between sleep duration and the likelihood or severity of panic attacks.

Insight: Lack of sleep may be a contributing factor to higher panic scores.


2. Panic Attack Duration (Minutes)

The number of patients is highest when the panic attack duration is around 30 minutes.

Fewer patients reported panic attacks that lasted for shorter (<20 min) or longer durations (>40 min).

Insight: Panic attacks are most frequently experienced with a moderate duration (~30 minutes), possibly indicating a typical panic episode span.


3. Drinks Per Week

Across all levels of alcohol consumption, the number of patients remains nearly constant and minimal (value = 1 per drink level shown).

This suggests that alcohol consumption may not have a strong or direct relationship with panic attack frequency or severity in this dataset.

Insight: Alcohol intake appears to have a neutral or negligible impact on panic symptoms based on the current data.


4. Slicers for Filtering Insights

The page includes interactive slicers for:

Panic Score (High, Medium, Low)

Gender (Male, Female)

Trigger Reason (e.g., Caffeine, Phobia, PTSD)

Medical History (e.g., Anxiety, Depression, None, PTSD)



These slicers enable deeper filtering and subgroup analysis for targeted comparisons, such as examining panic behavior patterns among patients with PTSD or caffeine-related triggers.


Summary:

Poor sleep hygiene is a strong contributor to panic attack incidence.

Panic attacks most commonly last around 30 minutes.

Alcohol intake shows no strong trend in panic symptoms.

Filters allow tailored insights based on mental health history, gender, and lifestyle triggers.
Snap short of the dashboard:
<img width="1345" height="721" alt="Image" src="https://github.com/user-attachments/assets/10a8a2af-6495-4a62-b8b9-b83602ec2a72" />
 
*Age Group and Trigger-Based Panic Attack Analysis

This clustered bar chart compares adolescents and adults across four different trigger reasons — Caffeine, Phobia, PTSD, and Social Anxiety — analyzing three key metrics:

Average Sleep Hours

Average Panic Score

Average Panic Attack Frequency


Key Conclusions by Trigger Type:


1. Caffeine

Adolescents have higher average sleep hours (6.7) and panic scores (6.4) than adults.

Despite more sleep, adolescents show higher panic attack frequency (6.5).

Insight: Caffeine appears to impact adolescents more severely, even when sleep duration is adequate.



2. Phobia

Adolescents again have higher average sleep hours (6.5) than adults (6.4).

However, adults show a higher panic score (5.4 vs. 4.4) and similar panic frequency (6.4 vs. 6.2).

Insight: Phobia may lead to more intense panic attacks in adults, even with slightly less sleep.


3. PTSD

Adults exhibit both higher panic scores (5.8) and panic frequency (6.6) compared to adolescents.

Adolescents sleep slightly more (5.5 hrs), but have lower panic severity and frequency.

Insight: PTSD-related panic attacks are more severe in adults, highlighting a potential vulnerability with age.


4. Social Anxiety

Adults and adolescents have very close panic frequency (5.9 vs. 5.1), with adults showing a higher panic score (6.6).

Sleep hours are similar between both groups (~6.5).

Insight: Social anxiety seems to trigger more severe attacks in adults, despite comparable sleep and frequency levels.

Across most triggers, adults experience higher panic scores and panic frequency compared to adolescents, despite generally getting slightly less sleep.

Caffeine impacts adolescents more, while PTSD and social anxiety are more intense among adults.

Sleep hours alone do not explain panic severity, suggesting the trigger type and age group play a more dominant role in panic attack characteristics.
