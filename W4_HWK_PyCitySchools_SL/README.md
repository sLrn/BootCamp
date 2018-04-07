
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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>65.172326</td>
    </tr>
  </tbody>
</table>
</div>




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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
  </tbody>
</table>
</div>



#### Top Performing Schools (By Passing Rate)


```python
#Sort District Summary by Overall Passing Rate (highest).
df_dist_summary = df_dist_summary.sort_values(by="% Overall Passing Rate", ascending=False)
df_dist_summary.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>



#### Bottom Performing Schools (By Passing Rate)


```python
#Sort District Summary by Overall Passing Rate (lowest).
df_dist_summary = df_dist_summary.sort_values(by="% Overall Passing Rate", ascending=True)
df_dist_summary.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>



#### Math Performance (by School/Grade)


```python
#Create a DataFrame that shows By Grade / By School math performance.
math_by_grade = pd.pivot_table(stu_df, values='math_score', index=['school'], columns=['grade'], aggfunc=np.mean)
math_by_grade = math_by_grade[['9th','10th','11th','12th']]
math_by_grade
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



#### Reading Performance (by School/Grade)


```python
#Create a DataFrame that shows By Grade / By School reading performance.
reading_by_grade = pd.pivot_table(stu_df, values='reading_score', index=['school'], columns=['grade'], aggfunc=np.mean)
reading_by_grade = reading_by_grade[['9th','10th','11th','12th']]
reading_by_grade
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>



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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.363065</td>
      <td>83.964039</td>
      <td>93.702889</td>
      <td>96.686558</td>
      <td>95.194724</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.529196</td>
      <td>83.838414</td>
      <td>94.124128</td>
      <td>95.886889</td>
      <td>95.005509</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>78.061635</td>
      <td>81.434088</td>
      <td>71.400428</td>
      <td>83.614770</td>
      <td>77.507599</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>77.049297</td>
      <td>81.005604</td>
      <td>66.230813</td>
      <td>81.109397</td>
      <td>73.670105</td>
    </tr>
  </tbody>
</table>
</div>



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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.828654</td>
      <td>83.974082</td>
      <td>93.952484</td>
      <td>96.040317</td>
      <td>94.996400</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.372682</td>
      <td>83.867989</td>
      <td>93.616522</td>
      <td>96.773058</td>
      <td>95.194790</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.477597</td>
      <td>81.198674</td>
      <td>68.652380</td>
      <td>82.125158</td>
      <td>75.388769</td>
    </tr>
  </tbody>
</table>
</div>



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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.406183</td>
      <td>83.902821</td>
      <td>93.701821</td>
      <td>96.645891</td>
      <td>95.173856</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.987026</td>
      <td>80.962485</td>
      <td>66.518387</td>
      <td>80.905249</td>
      <td>73.711818</td>
    </tr>
  </tbody>
</table>
</div>


