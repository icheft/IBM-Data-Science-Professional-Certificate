# Introduction to Data Visualization

1. For exploratory data analysis
2. communicate data clearly
3. share unbiased representation of data
4. use them to support recommendations to different stakeholders



1. less is more effective
2. less is more attractive
3. less is more impactive

![Image](https://i.imgur.com/vJvc5q0.png)

## Introduction to Matplotlib

3 Layers:
![Image](https://i.imgur.com/NF5vIgM.png)

### Backend Layer
1. FigureCanvas: matplotlib.backend_bases.FigureCanvas
    + encompasses the area onto which the figure is drawn
2. Renderer: `matplotlib.backend_bases.Renderer`
    + knows how to draw on the FigureCanvas
3. Event: `matplotlib.backend_bases.Event`
    + handles user inputs such as keyboard strokes and mouse clicks

### Artist Layer
+ comprised of one main object - `Artist`
    + knows how to use the Renderer to draw on the canvas
+ title, lines, tick labels, and images, all correspond to individual Artist Instances
+ two types of Artist objects:
    1. **Primitive**: Line2D, Rectangle, Circle, and Text
    2. **Composite**: Axis, Tick, Axes, and Figure
+ Each *composite* artist may contain other *composite* artists as well as *primitive* artists.

```py
from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas # Agg = Anti Grain Geometry
from matplotlib.figure import Figure # import Figure artist
import numpy as np

fig = Figure()
canvas = FigureCanvas(fig)

x = np.random.randn(10000)

ax = fig.add_subplot(111) # create an axes artist
ax.hist(x, 100)
ax.set_title('Normal Distribution with $\mu = 0, \sigma = 1$')
fig.savefig('matplotlib_histogram.png')  
```

### Scripting Layer

Developed for scientists.

+ comprised mainly of `pyplot`, a scripting interface that is lighter than the *Artist* layer


<https://www.aosabook.org/en/matplotlib.html>

## Basic Plotting with Matplotlib 
```py
from matplotlib import pyplot as plt
%matplotlib inline # or notebook for interactive figure
import numpy as np
plt.style.use('ggplot') # refined style

plt.plot(5, 5, 'o')
plt.show()
```


### Pandas
```py
df.plot(kind='line') # line chart
df['column_name'].plot(kind='hist')
```

## Dataset on Immigration to Canada

+ The Population Division of the UN compiled data pertaining to 45 countries.
+ For each country, annual data on the flows of international migrants is reported in addition to other metadata.
+ We will be working with a UN data on immigration to Canada

## Line Plots

Displays information as a series   of data points called 'markers' connected by straight line segments.

