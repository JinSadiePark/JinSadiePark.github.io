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
<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/_posts/Screenshot%202023-10-13%20at%205.24.55%20PM.png?raw=true" alt="Resized Image" width="400" height="300">
<br>

                plt.figure(figsize=(10, 8))
                penguin_bar = plt.bar(species, counts, width = 0.6)
                plt.xlabel("Penguin Species")
                plt.ylabel("Count")
                plt.title("Penguin Species Distribution")
                
<br>
This is a basic code for creating a bar chart. The general syntax for plt.bar is
<br>

                plt.bar(x, height, width, bottom, align)
                
<br>

* x: The x coordinates of the bars._<br>
* height: The height(s) of the bars.<br>
* width: The width(s) of the bars (default: 0.8).<br>
* bottom: The y coordinate(s) of the bases of the bars (default: 0).<br>
* align: Alignment of the bars to the x coordinates (default: 'center').



Right above is the code we used to add Joel Embiid on Team USA. Lets print out the dictionary and see if it has updated! 
<br>
<br>
<strong> Python code Input >>> </strong> <br>

                Team_USA
<br>

<strong> Python code Output >>> </strong> <br>

                'Point Guard' : 'Stephen Curry', 
                'Shooting Guard' : 'Devin Booker', 
                'Small Forward' : 'LeBron James',
                'Power Forward' : 'Kevin Durant', 
                'Center' : 'Joel Embiid'
<br>


