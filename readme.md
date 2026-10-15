# Wine Quality Data


``` python
## Wine Quality: Data Wrangling Final Project
# winequality-red.csv and winequality-white.csv

import pandas as pd
import matplotlib.pyplot as plt


red = pd.read_csv("winequality-red.csv", sep=";")
white = pd.read_csv("winequality-white.csv", sep=";")

# shape 
print("Red wines:", red.shape)
print("White wines:", white.shape)

# new column to tell the wines apart 
red["wine_type"] = "red"
white["wine_type"] = "white"

# stacking red and white wine tables
wine = pd.concat([red, white])
print("Combined:", wine.shape)

# fix column names
wine.columns = wine.columns.str.replace("red", "white")
print(list(wine.columns))


print("Duplicate rows:", wine.duplicated().sum())
# Removing
wine = wine.drop_duplicates()
print("After removing duplicates:", wine.shape)

# grouping wines by quality score, and finding the average alcohol in each group
average_alcohol = wine.groupby("quality")["alcohol"].mean()
print(average_alcohol)

# bar chart
average_alcohol.plot(kind="bar")
plt.title("Average Alcohol by Wine Quality")
plt.xlabel("Quality score")
plt.ylabel("Average alcohol (%)")
plt.savefig("alcohol_vs_quality.png")  
plt.show()                             # chart
```

    Red wines: (1599, 12)
    White wines: (4898, 12)
    Combined: (6497, 13)
    ['fixed acidity', 'volatile acidity', 'citric acid', 'residual sugar', 'chlorides', 'free sulfur dioxide', 'total sulfur dioxide', 'density', 'pH', 'sulphates', 'alcohol', 'quality', 'wine_type']
    Duplicate rows: 1177
    After removing duplicates: (5320, 13)
    quality
    3    10.215000
    4    10.215049
    5     9.872211
    6    10.649060
    7    11.511020
    8    11.912162
    9    12.180000
    Name: alcohol, dtype: float64

![](readme_files/figure-commonmark/cell-2-output-2.png)
