# Multi-dimensional data visualization
```py
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D 
import matplotlib as mpl
import numpy as np 
import seaborn as sns 
import warnings
warnings.filterwarnings('ignore')
get_ipython().run_line_magic('matplotlib', 'inline')
path1='C:/Users/griet/Desktop/423/task 9/winequality-red.csv'
path2='C:/Users/griet/Desktop/423/task 9/winequality-white.csv'
red_wine=pd.read_csv(path1,sep=';') 
white_wine=pd.read_csv(path2,sep=';')
red_wine['wine_type'] = 'red' 
white_wine['wine_type'] = 'white'
red_wine['quality_label'] = red_wine['quality'].apply(lambda value: 'low'
if value <= 5 else 'medium' 
if value <= 7 else 'high')
red_wine['quality_label'] = pd.Categorical(red_wine['quality_label'], categories=['low', 'medium', 'high']) 
white_wine['quality_label'] = white_wine['quality'].apply(lambda value: 'low'
if value <= 5 else 'medium' 
if value <= 7 else 'high')
white_wine['quality_label'] = pd.Categorical(white_wine['quality_label'], categories=['low', 'medium', 'high'])
wines = pd.concat([red_wine, white_wine])
wines = wines.sample(frac=1, random_state=42).reset_index(drop=True)
wines.head()
subset_attributes = ['residual sugar', 'total sulfur dioxide', 'sulphates', 
'alcohol', 'volatile acidity', 'quality']
rs = round(red_wine[subset_attributes].describe(),2) 
ws = round(white_wine[subset_attributes].describe(),2)
pd.concat([rs, ws], axis=1, keys=['Red Wine Statistics', 'White Wine Statistics'])
#------1D-------
wines.hist(bins=15, color='steelblue', edgecolor='black', linewidth=1.0, 
xlabelsize=8, ylabelsize=8, grid=False) 
plt.tight_layout(rect=(0, 0, 1.2, 1.2))
#---HISTOGRAM---
fig = plt.figure(figsize = (6,4)) 
title = fig.suptitle("Sulphates Content in Wine", fontsize=14) 
fig.subplots_adjust(top=0.85, wspace=0.3) 
ax = fig.add_subplot(1,1, 1) 
ax.set_xlabel("Sulphates") 
ax.set_ylabel("Frequency") 
ax.text(1.2, 800, r'$\mu$='+str(round(wines['sulphates'].mean(),2)), 
fontsize=12) 
freq, bins, patches = ax.hist(wines['sulphates'], color='steelblue', bins=15, 
edgecolor='black', linewidth=1) 
#---DENSITY PLOT---
fig = plt.figure(figsize = (6, 4)) 
title = fig.suptitle("Sulphates Content in Wine", fontsize=14) 
fig.subplots_adjust(top=0.85, wspace=0.3) 
ax1 = fig.add_subplot(1,1, 1) 
ax1.set_xlabel("Sulphates") 
ax1.set_ylabel("Frequency") 
sns.kdeplot(wines['sulphates'], ax=ax1, shade=True, color='steelblue')
#-------- 2D ---------
#---MATRIX HEATMAP---
f, ax = plt.subplots(figsize=(10, 6)) 
corr = wines.corr() 
hm = sns.heatmap(round(corr,2), annot=True, ax=ax, cmap="coolwarm",fmt='.2f', 
linewidths=.05) 
f.subplots_adjust(top=0.93) 
t= f.suptitle('Wine Attributes Correlation Heatmap', fontsize=14) 
#---PAIR WISE SCATTER PLOT---
cols = ['density', 'residual sugar', 'total sulfur dioxide', 'fixed acidity']
pp = sns.pairplot(wines[cols], size=1.8, aspect=1.8, 
plot_kws=dict(edgecolor="k", linewidth=0.5), 
diag_kind="kde", diag_kws=dict(shade=True))
fig = pp.fig
fig.subplots_adjust(top=0.93, wspace=0.3)
t = fig.suptitle('Wine Attributes Pairwise Plots', fontsize=14)
#---SCALING ATTRIBUTES---
cols = ['density', 'residual sugar', 'total sulfur dioxide', 'fixed acidity'] 
subset_df = wines[cols]
from sklearn.preprocessing import StandardScaler 
ss = StandardScaler()
scaled_df = ss.fit_transform(subset_df)
scaled_df = pd.DataFrame(scaled_df, columns=cols) 
final_df = pd.concat([scaled_df, wines['wine_type']], axis=1) 
final_df.head()
#---PARALLEL CORDS---
from pandas.plotting import parallel_coordinates
pc = parallel_coordinates(final_df, 'wine_type', color=('#FFE888', '#FF9999'))
#------ 3D -------
#---SCATTER PLOT---
cols = ['density', 'residual sugar', 'total sulfur dioxide', 'fixed acidity', 'wine_type'] 
pp = sns.pairplot(wines[cols], hue='wine_type', size=1.8, aspect=1.8,palette={"red": "#FF9999", "white": "#FFE888"}, plot_kws=dict(edgecolor="black", linewidth=0.5))
fig = pp.fig
fig.subplots_adjust(top=0.93, wspace=0.3)
t = fig.suptitle('Wine Attributes Pairwise Plots', fontsize=14)
#----- SCATTER PLOT WITH L,B,H-------
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
xs = wines['residual sugar'] 
ys = wines['fixed acidity'] 
zs = wines['alcohol']
ax.scatter(xs, ys, zs, s=50, alpha=0.6, edgecolors='w')
ax.set_xlabel('Residual Sugar')
ax.set_ylabel('Fixed Acidity') 
ax.set_zlabel('Alcohol')
#---FACETING----
quantile_list = [0, .25, .5, .75, 1.]
quantile_labels = ['0', '25', '50', '75'] 
wines['res_sugar_labels'] = pd.qcut(wines['residual sugar'], q=quantile_list, labels=quantile_labels) 
wines['alcohol_levels'] = pd.qcut(wines['alcohol'], q=quantile_list, labels=quantile_labels) 
g = sns.FacetGrid(wines, col="res_sugar_labels", hue='alcohol_levels')
g.map(plt.scatter, "fixed acidity", "alcohol", alpha=.7) 
g.add_legend();
#--- KERNEL DENSITY PLOT ---
ax = sns.kdeplot(white_wine['sulphates'], white_wine['alcohol'], 
cmap="YlOrBr", shade=True, shade_lowest=False)
ax = sns.kdeplot(red_wine['sulphates'], red_wine['alcohol'], 
cmap="Reds", shade=True, shade_lowest=False)
#--- violin plots ---
f, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 4))
f.suptitle('Wine Type - Quality - Acidity', fontsize=14)
sns.violinplot(x="quality", y="volatile acidity", 
data=wines, inner="quart", linewidth=1.3,ax=ax1)
ax1.set_xlabel("Wine Quality",size = 12,alpha=0.8) 
ax1.set_ylabel("Wine Volatile Acidity",size = 12,alpha=0.8)
sns.violinplot(x="quality", y="volatile acidity", hue="wine_type", 
data=wines, split=True, inner="quart", linewidth=1.3, 
palette={"red": "#FF9999", "white": "white"}, ax=ax2)
ax2.set_xlabel("Wine Quality",size = 12,alpha=0.8) 
ax2.set_ylabel("Wine Volatile Acidity",size = 12,alpha=0.8)
l = plt.legend(loc='upper right', title='Wine Type')
#-------- 4D --------
#--- SCATTER PLOT ----
fig = plt.figure(figsize=(8, 6))
t = fig.suptitle('Wine Residual Sugar - Alcohol Content - Acidity - Type', fontsize=14) 
ax = fig.add_subplot(111, projection='3d')
xs = list(wines['residual sugar']) 
ys = list(wines['alcohol'])
zs = list(wines['fixed acidity'])
data_points = [(x, y, z) for x, y, z in zip(xs, ys, zs)]
colors = ['red' if wt == 'red' else 'yellow' for wt in list(wines['wine_type'])]
for data, color in zip(data_points, colors):
    x, y, z = data
    ax.scatter(x, y, z, alpha=0.4, c=color, edgecolors='none', s=30)
ax.set_xlabel('Residual Sugar') 
ax.set_ylabel('Alcohol') 
ax.set_zlabel('Fixed Acidity')
#------ 5D ------
#--- BUBBLE CHART ---
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
t = fig.suptitle('Wine Residual Sugar - Alcohol Content - Acidity - Total Sulfur Dioxide - Type', fontsize=14)
xs = list(wines['residual sugar']) 
ys = list(wines['alcohol'])
zs = list(wines['fixed acidity'])
data_points = [(x, y, z) for x, y, z in zip(xs, ys, zs)]
ss = list(wines['total sulfur dioxide'])
colors = ['red' if wt == 'red' else 'yellow' for wt in list(wines['wine_type'])]
for data, color, size in zip(data_points, colors, ss):
    x, y, z = data
    ax.scatter(x, y, z, alpha=0.4, c=color, edgecolors='none', s=size)
ax.set_xlabel('Residual Sugar') 
ax.set_ylabel('Alcohol') 
ax.set_zlabel('Fixed Acidity')
#------ 6D ------
#--- SCATTER PLOT ---
fig = plt.figure(figsize=(8, 6))
t = fig.suptitle('Wine Residual Sugar - Alcohol Content - Acidity - Total Sulfur Dioxide - Type - Quality', 
fontsize=14)
ax = fig.add_subplot(111, projection='3d') 
xs = list(wines['residual sugar'])
ys = list(wines['alcohol'])
zs = list(wines['fixed acidity'])
data_points = [(x, y, z) for x, y, z in zip(xs, ys, zs)] 
ss = list(wines['total sulfur dioxide'])
colors = ['red' if wt == 'red' else 'yellow' for wt in list(wines['wine_type'])]
markers = [',' if q == 'high' else 'x' if q == 'medium' else 'o' for q in list(wines['quality_label'])] 
for data, color, size, mark in zip(data_points, colors, ss, markers):
    x, y, z = data
    ax.scatter(x, y, z, alpha=0.4, c=color, edgecolors='none', s=size, marker=mark)
ax.set_xlabel('Residual Sugar')
ax.set_ylabel('Alcohol') 
ax.set_zlabel('Fixed Acidity')
```
