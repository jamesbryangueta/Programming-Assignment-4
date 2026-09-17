# **| PROGRAMMING ASSIGNMENT NO.4 |**


 *GUETA, JAMES BRYAN | 2 ECE-C*
#_______________________________________________________________________________

**OBJECTIVES**

1. Filter tabular data using several categorical and numerical conditions;
2. Construct focused DataFrames by selecting relevant features;
3. Summarize the relationship between categorical features and a numerical variable;
4. Communicate a data comparison using clear and correctly labeled plots.

```**Pandas Initiation**``` & ```Matplotlib Initiation```
```import pandas as pd ``` & ```import matplotlib.pyplot as plt```

```**Reading and setting up board2.xlsx**```

```
df = pd.read_excel('board2.xlsx')
displaydf = df[['Math', 'Electronics', 'GEAS', 'Communication']]
means= pd.DataFrame(displaydf.mean(axis=1), columns=['Average'])
df =pd.concat([df, means], axis=1)
df
```

# **A. VISAYAS COMMUNICATION DATAFRAME**

Create a DataFrame named *VisComm* containing students whose Hometown is **Visayas** and whose Track is **Communication**. Retain only these columns, in the stated order:

```Name, Gender, Math, Electronics, Average```
---

Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected


```
Viscomm= df.loc [(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ('Name','Gender','Math','Electronics','Average')]
Viscomm
```

# **VISAYAS FEMALE DATAFRAME**

---

Create a second DataFrame named *VisFemale* containing students whose Hometown is **Visayas** and
whose Gender is **Female**. Retain only:
```Name, Track, GEAS, Electronics, Average```

Display *VisFemale*. Then display only the rows of *VisFemale* whose Average is at least **60**. Do not
overwrite *VisFemale* when performing this second filter.

```
VisFemale= df.loc [(df['Hometown'] == 'Visayas') & (df['Average'] >= 60), ('Name','Track','GEAS','Electronics','Average')]
VisFemale
```

# **C. CATEGORY-AVERAGE VISUALIZATION**

---


Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown.

a. For each feature, compute the mean of Average for every category using Pandas.

b. Display the three summary tables.

c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.

d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.

**Interpretation rule**: Describe the observed dataset only. A difference in group means does not, by
itself, establish that a feature causes a higher board-exam score.
```
Track = df.groupby('Track')['Average'].mean().reset_index()
```
```
Gender = df.groupby('Gender')['Average'].mean().reset_index()
```
```
fig, axes = plt.subplots(1, 3, figsize=(16, 5), sharey=True)

axes[0].bar(Track['Track'], Track['Average'])
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average Score')

axes[1].bar(Gender['Gender'], Gender['Average'])
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')

axes[2].bar(Hometown['Hometown'], Hometown['Average'])
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')

plt.tight_layout()
plt.show()
```

```
TrackS = Track.loc[Track['Average'].idxmax()]
GenderS = Gender.loc[Gender['Average'].idxmax()]
HometownS = Hometown.loc[Hometown['Average'].idxmax()]

TrackS = f"1. Track: The {TrackS['Track']} track recorded the highest sample mean Average score ({TrackS['Average']:.2f})."
GenderS = f"2. Gender: {GenderS['Gender']} students recorded the highest sample mean Average score ({GenderS['Average']:.2f})."
HometownS = f"3. Hometown: Students from {HometownS['Hometown']} recorded the highest sample mean Average score ({HometownS['Average']:.2f})."
```
```
print(TrackS)
1. Track: The Communication track recorded the highest sample mean Average score (67.97).
```
```
print(GenderS)
2. Gender: Male students recorded the highest sample mean Average score (67.18).
```
```
print(HometownS)
3. Hometown: Students from Luzon recorded the highest sample mean Average score (68.08).
```



