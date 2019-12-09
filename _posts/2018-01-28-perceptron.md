---
title: "Data Wrangling Project"
date: 2018-01-28
tags: [data wrangling, data science, messy data]
header:
  image: "/images/perceptron/percept.jpg"
excerpt: "Rental prices in Vienna"
mathjax: "true"
---

# Rental prices in Vienna

Copied from my [Google Colab](https://colab.research.google.com/drive/1IQlD-ijFpHuK8Mb2NvtLIaCy6Z9_YV9n)

```
import pandas as pd
import matplotlib.pyplot as plt

vienna_df = pd.read_csv('./vienna-rental-prices-data.csv', parse_dates=True)
vienna_df['date'] = pd.to_datetime(vienna_df['date'])

vienna_df['period']= vienna_df['date'].dt.to_period('M')

vienna_fig = plt.figure()
vienna_ax = vienna_fig.subplots()
vienna_df.groupby(['period', 'flat_plz']).median()['flat_price_per_m'].unstack().plot(ax=vienna_ax)

vienna_ax.legend(loc='center left', bbox_to_anchor=(1,0.5), ncol=3)
vienna_ax.set_xlabel('Date')
vienna_ax.set_ylabel('Median flat price per sqm in €')
vienna_ax.set_title('Median rental prices in Vienna')

vienna_filtered = vienna_df[(vienna_df['flat_plz'] == 1010) | 
                            (vienna_df['flat_plz'] == 1080) | 
                            (vienna_df['flat_plz'] == 1130) | 
                            (vienna_df['flat_plz'] == 1160)].groupby(['period', 'flat_plz']).median()

vienna_filtered_fig = plt.figure()
vienna_filtered_ax = vienna_filtered_fig.subplots()
vienna_filtered['flat_price_per_m'].unstack().plot(ax=vienna_filtered_ax)

vienna_filtered_ax.legend(loc='center left', bbox_to_anchor=(1,0.5), ncol=3)
vienna_filtered_ax.set_xlabel('Date')
vienna_filtered_ax.set_ylabel('Median flat price per sqm in €')
vienna_filtered_ax.set_title('Median rental prices for 1010, 1080, 1130 and 1160')

plt.show()
```


![png](vienna_files/vienna_0_0.png)



![png](vienna_files/vienna_0_1.png)



## H2 Heading

### H3 Heading

Here's some basic text.

And here's some *italics*

Here's some **bold** text.



Here's a bulleted list:
* First item
+ Second item
- Third item

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
    import numpy as np

    def test_function(x, y):
      z = np.sum(x,y)
      return z
```

R code block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```

Here's some inline code `x+y`.

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg" alt="linearly separable data">

Here's another image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg)

Here's some math:

$$z=x+y$$

You can also put it inline $$z=x+y$$
