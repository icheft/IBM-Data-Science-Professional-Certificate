# Creating Dashboards with Plotly and Dash

## Overview

+ Dash: plotly.js, flask, react.js
+ Panel: matplotlib, etc. --> works in Jupyter Notebook as well
+ Voila: standalone app
+ streamlit: shareable web apps
+ bokeh
+ ipywidgets
+ maplotlib
+ Flask
+ Bowtie


## Plotly

+ Plotly Graph Objects: Low-level interface to figures, traces, and layout
+ Plotly Express: High-level wrapper - more simple

```py
import plotly.graph_objects as go
import plotly.express as px
import numpy as np

np.random.seed(10)
x = np.arange(12)
y = np.random.randint(50, 500, size=12)

fig = go.Figure(data=go.Scatter(x=x, y=y))
fig.update_layout(title='Simple Line Plot', xaxis_title='Month', yaxis_title='Sales')
fig.show()
```
```py
fig = px.line(x=x, y=y, title='Simple Line Plot', labels=dict(x='Month', y='Sales'))
fig.show()
```


## Additional Resources

To learn more about using Plotly to create dashboards, explore

+ [Plotly python](https://plotly.com/python/getting-started/)
+ [Plotly graph objects with example](https://plotly.com/python/graph-objects/)
+ [Plotly express](https://plotly.com/python/plotly-express/)
+ [API reference](https://plotly.com/python-api-reference/)
### Here are additional useful resources:
+ [Plotly cheatsheet](https://images.plot.ly/plotly-documentation/images/plotly_js_cheat_sheet.pdf)
+ [Plotly community](https://community.plotly.com/c/api/5)
+ [Related blogs](https://plotlygraphs.medium.com/)
+ [Open-source datasets ](https://developer.ibm.com/exchanges/data/)

 

## Introduction to Dash
+ core components: 
    ```py
    import dash_core_components as dcc
    ```
    + Examples: creating a slider, input area, check items, datepicker 
+ HTML Components
    ```py
    import dash_html_components as html
    ```

### Additional Resources to Dash

+ [Complete dash user guide](https://dash.plotly.com/)
+ [Dash core components](https://dash.plotly.com/dash-core-components)
+ [Dash HTML components](https://dash.plotly.com/dash-html-components)
+ [Dash community forum](https://community.plotly.com/c/dash/16)
+ [Related blogs](https://medium.com/plotly/tagged/dash)

## Additional Resources for Interactive Dashboards

To learn more about making interactive dashboards in Dash, visit

+ [Python decorators reference 1](https://realpython.com/primer-on-python-decorators/)
+ [Python decorators reference 2](https://www.python.org/dev/peps/pep-0318/#current-syntax)
+ [Callbacks with example](https://dash.plotly.com/basic-callbacks)
+ [Dash app gallery](https://dash-gallery.plotly.host/Portal/)
+ [Dash community components](https://plotly.com/dash-community-components/)