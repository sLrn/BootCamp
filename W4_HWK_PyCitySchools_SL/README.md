
### PyCitySchools Analysis<br/>

Observation 1) Charter schools outperformed district schools in all evaluated categories<br/><br/>
Observation 2) For these examples higher "spending per student" does not correlate to higher performance<br/><br/>
Observation 3) These results suggest a relationship between school size and performance - with smaller schools achieving better outcomes


```python
import pandas as pd
import numpy as np
```


```python
stu_df = pd.read_csv('raw_data/students_complete.csv')
scho_df = pd.read_csv('raw_data/schools_complete.csv')
```


```python
#Create bins for df
bins = [0, 69, 100]
pass_fail = [0 , 1]
```


```python
#Create bins that assign a 1 or 0 to another column for columns "pass_reading" and "pass_math"
stu_df["pass_reading"] = pd.cut(stu_df["reading_score"], bins, labels=pass_fail)
stu_df["pass_math"] = pd.cut(stu_df["math_score"], bins, labels=pass_fail)
```


```python
#Add the bin labels together as a value test for "pass_overall."
stu_df["pass_overall"] = (stu_df["pass_math"]+stu_df["pass_reading"])
```


```python
#Build a dictionary to serve as DataFrame information. 
dist_summary =   {
                    'Total Schools'         : scho_df["name"].count(),
                    'Total Students'        : scho_df["size"].sum(),
                    'Total Budget'          : scho_df["budget"].sum(),
                    'Average Math Score'    : stu_df["math_score"].mean(),
                    'Average Reading Score' : stu_df["reading_score"].mean(),
                    '% Passing Math'        : ((stu_df["pass_math"]).astype('float').sum()/(stu_df["pass_math"]).astype('float').count())*100,
                    '% Passing Reading'     : ((stu_df["pass_reading"]).astype('float').sum()/(stu_df["pass_reading"]).astype('float').count())*100,
                    '% Overall Passing Rate': (stu_df[stu_df["pass_overall"]>1].count()["pass_overall"]/stu_df[stu_df["pass_overall"]>=0].count()["pass_overall"])*100
                    # Note: The example had impossible values for overall passing rate. The correct way to calculate this is above. To be safe, for the rest of the challenge I went with a method that reflected what was shown on the example.
                    }
```

#### District Summary


```python
#Build and display the last DataFrame for Part 1 of PyCitySchools
df = pd.DataFrame([dist_summary], columns=dist_summary.keys())

df
```


```python
#Build District Summary DataFrame and combine data as needed.
x = scho_df[["name","type","size",'budget']].copy()
x.columns = ['School Name', 'School Type', 'Total Students','Total School Budget']
df_dist_summary = x.set_index('School Name')
```

#### School Summary


```python
df_dist_summary['Per Student Budget'] = df_dist_summary['Total School Budget'] / df_dist_summary["Total Students"]

df_dist_summary['Average Math Score'] = pd.pivot_table(stu_df, values = "math_score", index=['school'], aggfunc='sum')
df_dist_summary['Average Math Score'] = df_dist_summary['Average Math Score'] / df_dist_summary["Total Students"]

df_dist_summary['Average Reading Score'] = pd.pivot_table(stu_df, values = "reading_score", index=['school'], aggfunc='sum')
df_dist_summary['Average Reading Score'] = df_dist_summary['Average Reading Score'] / df_dist_summary["Total Students"]

df_dist_summary['% Passing Math'] = pd.pivot_table(stu_df, values = "pass_math", index=['school'], aggfunc='sum') 
df_dist_summary['% Passing Math'] = (df_dist_summary['% Passing Math'] / df_dist_summary["Total Students"]) * 100

df_dist_summary['% Passing Reading'] = pd.pivot_table(stu_df, values = "pass_reading", index=['school'], aggfunc='sum') 
df_dist_summary['% Passing Reading'] = (df_dist_summary['% Passing Reading'] / df_dist_summary["Total Students"]) * 100

df_dist_summary['% Overall Passing Rate'] = ((df_dist_summary['% Passing Reading'] + df_dist_summary['% Passing Math']) / 2)
df_dist_summary
```

#### Top Performing Schools (By Passing Rate)


```python
#Sort District Summary by Overall Passing Rate (highest).
df_dist_summary = df_dist_summary.sort_values(by="% Overall Passing Rate", ascending=False)
df_dist_summary.head(5)
```

#### Bottom Performing Schools (By Passing Rate)


```python
#Sort District Summary by Overall Passing Rate (lowest).
df_dist_summary = df_dist_summary.sort_values(by="% Overall Passing Rate", ascending=True)
df_dist_summary.head(5)
```

#### Math Performance (by School/Grade)


```python
#Create a DataFrame that shows By Grade / By School math performance.
math_by_grade = pd.pivot_table(stu_df, values='math_score', index=['school'], columns=['grade'], aggfunc=np.mean)
math_by_grade = math_by_grade[['9th','10th','11th','12th']]
math_by_grade
```

#### Reading Performance (by School/Grade)


```python
#Create a DataFrame that shows By Grade / By School reading performance.
reading_by_grade = pd.pivot_table(stu_df, values='reading_score', index=['school'], columns=['grade'], aggfunc=np.mean)
reading_by_grade = reading_by_grade[['9th','10th','11th','12th']]
reading_by_grade
```

#### Scores by School Spending


```python
#Create DataFrame that shows performance by bins divided by cost per student.

spending_dict = {'Bailey High School' : df_dist_summary.loc["Bailey High School","Per Student Budget"],
                 'Cabrera High School' : df_dist_summary.loc["Cabrera High School","Per Student Budget"],
                 'Figueroa High School' : df_dist_summary.loc["Figueroa High School","Per Student Budget"],
                 'Ford High School' : df_dist_summary.loc["Ford High School","Per Student Budget"],
                 'Griffin High School' : df_dist_summary.loc["Griffin High School","Per Student Budget"],
                 'Hernandez High School' : df_dist_summary.loc["Hernandez High School","Per Student Budget"],
                 'Holden High School' : df_dist_summary.loc["Holden High School","Per Student Budget"],
                 'Huang High School' : df_dist_summary.loc["Huang High School","Per Student Budget"],
                 'Johnson High School' : df_dist_summary.loc["Johnson High School","Per Student Budget"],
                 'Pena High School' : df_dist_summary.loc["Pena High School","Per Student Budget"],
                 'Rodriguez High School' : df_dist_summary.loc["Rodriguez High School","Per Student Budget"],
                 'Shelton High School' : df_dist_summary.loc["Shelton High School","Per Student Budget"],
                 'Thomas High School' : df_dist_summary.loc["Thomas High School","Per Student Budget"],
                 'Wilson High School' : df_dist_summary.loc["Wilson High School","Per Student Budget"],
                 'Wright High School' : df_dist_summary.loc["Wright High School","Per Student Budget"],
                }
#spending_dict
stu_df["School Spending Spending (Per Student)"] = stu_df["school"].map(spending_dict)


spending_bins = [0, 585, 615, 645, 675]
spending_labels = ['<$585' , '$585-615' , '$615-645' , '$645-675']

stu_df["Spending Ranges (Per Student)"] = pd.cut(stu_df["School Spending Spending (Per Student)"], spending_bins, labels=spending_labels)
stu_df['pass_math'] = stu_df['pass_math'].astype(float)
stu_df['pass_reading'] = stu_df['pass_reading'].astype(float)

per_student_df = pd.pivot_table(stu_df, values=['math_score','reading_score','pass_math','pass_reading'], index=['Spending Ranges (Per Student)'], aggfunc=np.mean)
per_student_df['% Overall Passing Rate'] = (per_student_df['pass_math'] + per_student_df['pass_reading'])*50
per_student_df['pass_math'] = per_student_df['pass_math'] * 100
per_student_df['pass_reading'] = per_student_df['pass_reading'] * 100

per_student_df.rename(columns={'math_score': 'Average Math Score','reading_score': 'Average Reading Score', 'pass_math': '% Passing Math', 'pass_reading': '% Passing Reading'}, inplace=True)

per_student_df = per_student_df[['Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing Rate']]

per_student_df
```

#### Performance by School Size


```python
#Create DataFrame that shows performance by bins divided by size of school.

size_dict = {'Bailey High School' : df_dist_summary.loc["Bailey High School","Total Students"],
                 'Cabrera High School' : df_dist_summary.loc["Cabrera High School","Total Students"],
                 'Figueroa High School' : df_dist_summary.loc["Figueroa High School","Total Students"],
                 'Ford High School' : df_dist_summary.loc["Ford High School","Total Students"],
                 'Griffin High School' : df_dist_summary.loc["Griffin High School","Total Students"],
                 'Hernandez High School' : df_dist_summary.loc["Hernandez High School","Total Students"],
                 'Holden High School' : df_dist_summary.loc["Holden High School","Total Students"],
                 'Huang High School' : df_dist_summary.loc["Huang High School","Total Students"],
                 'Johnson High School' : df_dist_summary.loc["Johnson High School","Total Students"],
                 'Pena High School' : df_dist_summary.loc["Pena High School","Total Students"],
                 'Rodriguez High School' : df_dist_summary.loc["Rodriguez High School","Total Students"],
                 'Shelton High School' : df_dist_summary.loc["Shelton High School","Total Students"],
                 'Thomas High School' : df_dist_summary.loc["Thomas High School","Total Students"],
                 'Wilson High School' : df_dist_summary.loc["Wilson High School","Total Students"],
                 'Wright High School' : df_dist_summary.loc["Wright High School","Total Students"],
                }

stu_df["Size of School"] = stu_df["school"].map(size_dict)
size_bins = [0, 1000, 2000, 5000]
size_labels = ['Small (<1000)' , 'Medium (1000-2000)' , 'Large (2000-5000)']
stu_df["School Size"] = pd.cut(stu_df["Size of School"], size_bins, labels=size_labels)

school_size_df = pd.pivot_table(stu_df, values=['math_score','reading_score','pass_math','pass_reading'], index=['School Size'], aggfunc=np.mean)
school_size_df['% Overall Passing Rate'] = (school_size_df['pass_math'] + school_size_df['pass_reading'])*50
school_size_df['pass_math'] = school_size_df['pass_math'] * 100
school_size_df['pass_reading'] = school_size_df['pass_reading'] * 100


school_size_df.rename(columns={'math_score': 'Average Math Score','reading_score': 'Average Reading Score', 'pass_math': '% Passing Math', 'pass_reading': '% Passing Reading'}, inplace=True)

school_size_df = school_size_df[['Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing Rate']]
school_size_df
```

#### Performance by School Type


```python
#Build DataFrame that displays performance by School Type.
type_dict = {'Bailey High School' : df_dist_summary.loc["Bailey High School","School Type"],
                 'Cabrera High School' : df_dist_summary.loc["Cabrera High School","School Type"],
                 'Figueroa High School' : df_dist_summary.loc["Figueroa High School","School Type"],
                 'Ford High School' : df_dist_summary.loc["Ford High School","School Type"],
                 'Griffin High School' : df_dist_summary.loc["Griffin High School","School Type"],
                 'Hernandez High School' : df_dist_summary.loc["Hernandez High School","School Type"],
                 'Holden High School' : df_dist_summary.loc["Holden High School","School Type"],
                 'Huang High School' : df_dist_summary.loc["Huang High School","School Type"],
                 'Johnson High School' : df_dist_summary.loc["Johnson High School","School Type"],
                 'Pena High School' : df_dist_summary.loc["Pena High School","School Type"],
                 'Rodriguez High School' : df_dist_summary.loc["Rodriguez High School","School Type"],
                 'Shelton High School' : df_dist_summary.loc["Shelton High School","School Type"],
                 'Thomas High School' : df_dist_summary.loc["Thomas High School","School Type"],
                 'Wilson High School' : df_dist_summary.loc["Wilson High School","School Type"],
                 'Wright High School' : df_dist_summary.loc["Wright High School","School Type"],
                }

stu_df["School Type"] = stu_df["school"].map(type_dict)

school_type_df = pd.pivot_table(stu_df, values=['math_score','reading_score','pass_math','pass_reading'], index=['School Type'], aggfunc=np.mean)
school_type_df['% Overall Passing Rate'] = (school_type_df['pass_math'] + school_type_df['pass_reading'])*50
school_type_df['pass_math'] = school_type_df['pass_math'] * 100
school_type_df['pass_reading'] = school_type_df['pass_reading'] * 100

school_type_df.rename(columns={'math_score': 'Average Math Score','reading_score': 'Average Reading Score', 'pass_math': '% Passing Math', 'pass_reading': '% Passing Reading'}, inplace=True)
school_type_df = school_type_df[['Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing Rate']]

school_type_df

```
