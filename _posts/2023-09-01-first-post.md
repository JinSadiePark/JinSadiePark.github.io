---
layout: post
title:  "The Art of Data Visualization"
author: "Jinkyung Park"
description: "This is a guide to the techniques and best practices for creating stunning graphs in Python."
image: "https://buffml.com/wp-content/uploads/2022/12/plots_python.png"
--- 

Creating visually appealing graphs in Python is a valuable skill for anyone looking to convey data-driven insights effectively. In this tutorial, we will delve into data visualization with Python, exploring Seaborn and Matplotlib. Whether you're a data scientist, analyst, or just someone passionate about presenting data in a compelling way, you'll discover how to craft stunning and informative graphs that bring your data to life.

When we create graphs there are a couple of things to consider.<br>
* Are we using categorical data or numerical data?<br>
* Are we creating the graph based on one feature or multiple features?


## One Categorical Feature
We can use a bar chart for this. The **categories** are typically displayed on the **x-axis** while the height or length of the bars on the **y-axis** represents the **frequency, count, or any other quantitative measure associated with each category**.
<br></br>

Let's start with matplotlib.

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-10-13%20at%201.18.02%20PM.png?raw=true" alt="Resized Image" width="400" height="300">

                plt.figure(figsize=(10, 8))
                penguin_bar = plt.bar(species, counts, width = 0.6)
                plt.xlabel("Penguin Species")
                plt.ylabel("Count")
                plt.title("Penguin Species Distribution")
<br>                
This is the general syntax of a bar chart.
<br>

                plt.bar(x, height, width)             

* _x : The x coordinates of the bars._<br>
* _height : The height(s) of the bars._<br>
* _width : The width(s) of the bars (default: 0.8)._<br>

<br>
If you want to change the color of the bars, you can specify the color inside of your plt.bar().
<br>

              plt.bar(species, counts, width = 0.6, color = 'mistyrose')

In this case, however, you can't have multiple colors. If you want different colors for each bar, you can specify the bar by using the index and .set_color().
<br>

              penguin_bar[0].set_color('mistyrose')
              penguin_bar[1].set_color('salmon')
              penguin_bar[2].set_color('tomato')
              
_You can google for the matplotlib color options._<br>
<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-10-13%20at%205.24.55%20PM.png?raw=true" alt="Resized Image" width="400" height="300">
<br>
<br>
<br>
We can also use seaborn to create graphs.

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-10-13%20at%207.05.23%20PM.png?raw=true" alt="Resized Image" width="400" height="300">
<br>

                sns.barplot(species_counts, x='species', y='count')
                plt.xlabel("Penguin Species")
                plt.ylabel("Count")
                plt.title("Number of Penguins for Each Species")

Here is the general syntax.
<br>

                sns.barplot(data, x, y)
                
* _data : DataFrame, array, or list of arrays_<br>
* _x : The x coordinates of the bars._<br>
* _y : The y coordinates of the bars._<br>
<br>

Seabron will automatically use different colors for different values. If you want to specify a feature to have a different color, you can add a hue argument.
<br>

                sns.barplot(data, 'x', 'y', hue = 'x')

_Note that the hue argument is more useful when you have multiple features._
<br>

## Multiple Categorical Features
We can also use a bar chart but because there is more than one feature, we are going to use a **grouped** bar chart.

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-10-13%20at%208.15.57%20PM.png?raw=true" alt="Resized Image" width="500" height="300">
<br>

                grouped_data = penguins.groupby('species')[['bill_depth_mm', 'bill_length_mm', 'flipper_length_mm']].mean()

                grouped_data.plot(kind='bar', width=0.8, figsize=(10.5, 6))
                plt.xlabel("Penguin Species")
                plt.ylabel("Mean Bill Length (mm)")
                plt.title("Penguin Bill Length by Species and Island")
                
The key is preparing the data for a grouped bar chart by grouping a penguin dataset by species and selecting the columns corresponding to bill depth, bill length, and flipper length. And you'll use _data.plot() and specify the kind of graph you want inside of the parentheses.

<br>

                plt.legend(title="Measurements", loc='upper left')
                plt.xticks(rotation=0)

_legend_ is a key component that provides an explanation or interpretation of the elements, data, or categories represented in the chart.<br>
_xticks_ rotates x-axis labels for better readability. The unit of the value is degree.

<br>
<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-10-13%20at%209.03.46%20PM.png?raw=true" alt="Resized Image" width="500" height="300">
<br>
                
                grouped_data = penguins.groupby('species')[['bill_depth_mm', 'bill_length_mm', 'flipper_length_mm']].mean().reset_index()

                melted_data = pd.melt(grouped_data, id_vars=['species'], value_vars=['bill_depth_mm', 'bill_length_mm', 'flipper_length_mm'], var_name='Measurement')
                
                sns.barplot(data=melted_data, x='species', y='value', hue='Measurement')
                plt.xlabel("Penguin Species")
                plt.ylabel("Mean Measurements (mm)")
                plt.title("Penguin Bill Depth, Bill Length, and Flipper Length by Species")
                plt.legend(title="Measurement", loc='upper left')

Seaborn has one more step for a grouped bar chart. Melt is a data transformation operation in Pandas and other data manipulation libraries that reshapes or transforms a dataset from a wide format to a long format.

<br>
<br>
Data visualization is a powerful tool for gaining insights from your data. Experiment with your own data, and don't hesitate to share your insights and visualizations with others. The best way to become proficient in data visualization is through practice, so start today!
