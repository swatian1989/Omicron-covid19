# Omicron-covid19
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
# Importing necessary files
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
# Reading Omicron variant in a variable named 'train'
train=pd.read_csv("../input/omicron-covid19-variant-daily-cases/covid-variants.csv")
# Displaying first 5 rows of our data
train.head()
# Checking out null values if any
train.isnull().sum()
# Counting number of values corresponding to each location
train['location'].value_counts()
# Creating separate datasets with respect to OMICRON,DELTA,BETA Variants.
omicron=train[train['variant']=='Omicron']
delta=train[train['variant']=='Delta']
beta=train[train['variant']=='Beta']
# Adding up cases on same date using sum() method
omicron_sum=omicron.groupby("date").sum()
delta_sum=delta.groupby("date").sum()
beta_sum=beta.groupby("date").sum()
CASES AROUND WORLD
# Lineplot Showing Omicron Cases Over World
# Using log as it returns natural logarithm of that particular column
plt.figure(figsize=(15,6))
plt.xticks(rotation=90)
sns.lineplot(x=omicron_sum.index,y=np.log1p(omicron_sum['num_sequences']),color='red',linewidth='3')
plt.title('Omicron Cases All Over World')
# Lineplot Showing Delta Cases Over World
# Using log as it returns natural logarithm of that particular column
plt.figure(figsize=(15,6))
plt.xticks(rotation=90)
sns.lineplot(x=delta_sum.index,y=np.log1p(delta_sum['num_sequences']),color='red',linewidth='3')
plt.title('Delta Cases All Over World')
# Lineplot Showing Beta Cases Over World
# Using log as it returns natural logarithm of that particular column
plt.figure(figsize=(15,6))
plt.xticks(rotation=90)
sns.lineplot(x=beta_sum.index,y=np.log1p(beta_sum['num_sequences']),color='red',linewidth='3')
plt.title('Beta Cases All Over World')
Beta Variant
# Lineplot showing different increase of beta variant around different countries
# Using log as it returns natural logarithm of that particular column
plt.figure(figsize=(15,6))
plt.xticks(rotation=90)
sns.lineplot(x=beta_india['date'],y=np.log1p(beta_india['num_sequences']),label='India',linewidth='3')
sns.lineplot(x=beta_Nepal['date'],y=np.log1p(beta_Nepal['num_sequences']),label='Nepal',linewidth='3')
sns.lineplot(x=beta_Pakistan['date'],y=np.log1p(beta_Pakistan['num_sequences']),label='Pakistan',linewidth='3')
sns.lineplot(x=beta_Bangladesh['date'],y=np.log1p(beta_Bangladesh['num_sequences']),label='Bangladesh',linewidth='3')
plt.title('Beta variant around different countries')
