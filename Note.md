
```py
print('hello world')
``` 
# e-Book
- [GitBook_notebook](https://app.gitbook.com/@yo-sarawut/s/workspace/)
- [Knowledge Base : GitHub](https://yosarawut.github.io/knowledge-base/)
- [e-Library](https://dragon_e-library.gitlab.io/knowledge_base/)
- [e-Import](https://app.gitbook.com/@e-import/s/e-import/)
- [e-Customs](https://ecs_knowledge_center.gitlab.io/e-customs/)
- [e-Tax Inv&Rceipt]()
- [==Setup Jupyternotebook for markdown==](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)
# Color :
- [https://www.w3schools.com/colors/colors_2019.asp](https://www.w3schools.com/colors/colors_2019.asp)
- 
Galaxy Blue
HEX: #2A4B7C
PANTONE 19-4055

![enter image description here](https://github.com/yosarawut/knowledge-base/raw/master/img/galaxy_blue.jpg)

HEX: #34558b

![enter image description here](https://simpledits.com/wp-content/uploads/2019/09/20190927_2020-PANTONE-19-4052-Classic-Blue.png)


#  Tutorials

- [Python Tutorial by w3resource](https://www.w3resource.com/python/python-tutorial.php)
- [PYTHON TUTORIAL & Example](https://www.programiz.com/python-programming/time/sleep)
- [ตัวอย่างการทำ Project ด้วย Python](https://pythonprogramming.net)
- [pythontesting.net](https://pythontesting.net/start-here/)

## e-Book Free


# ==ควรศึกษา==

- [ Let’s get started with ==**GitHub!**==](https://guides.github.com/activities/hello-world/)
- [A gellery of interesting IPython Notebooks](https://github.com/ipython/ipython/wiki)

# Packages

- [Reliably download historical market data from Yahoo! Finance with Python : ==**yfinance**==](https://aroussi.com/post/python-yahoo-finance)
- [Popular Python 3 Packages](https://code.activestate.com/pypm/tag:python3/?page=1)
- [Fast Data Store for Pandas Time-Series Data using PyStore](https://aroussi.com/post/fast-datastore-for-pandas-time-series-data)
- [Python.HotExamplesFunction](https://python.hotexamples.com/)
- [The Future of QTPyLib](https://aroussi.com/post/the-future-of-qtpylib) , [GitHub](https://github.com/ranaroussi/qtpylib)

![enter image description here](https://aroussi.com//assets/img/qtpylib-ui.png)

# Article

- [รวมบทความเกี่ยวกับ Pandas](https://blog.hedaro.com/)
- [มาหาค่า Correlation ของ CRYPTOCURRENCY ด้วย PYTHON ](https://medium.com/@suttipongsrimangmat/%E0%B8%A1%E0%B8%B2%E0%B8%AB%E0%B8%B2%E0%B8%84%E0%B9%88%E0%B8%B2-correlation-%E0%B8%82%E0%B8%AD%E0%B8%87-cryptocurrency-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-python-%E0%B8%81%E0%B8%B1%E0%B8%99%E0%B9%86%E0%B9%86%E0%B9%86-2733fa3f8987)



# ==Example==

- [Hands-On-Data-Science-and-Python-Machine-Learning](https://github.com/prasertcbs/Hands-On-Data-Science-and-Python-Machine-Learning)
- [BUILD A LIVE DASHBOARD WITH PYTHON](https://pusher.com/tutorials/live-dashboard-python) , [==GitHub==](https://github.com/neoighodaro/pusher-python-realtime-dashboard)
-  [Vanguard 500 Index Fund Investor Shares](https://dash-gallery.plotly.host/dash-vanguard-report/full-view)
- [DataCamp-Projects](https://github.com/prasertcbs/DataCamp-Projects)
-  [Trading with Python Webinar Series](https://github.com/ranaroussi/futuresio-webinars)
- [plotlyjs-flask-example](https://github.com/plotly/plotlyjs-flask-example)
- [minimal-flask-example](https://github.com/ericmjl/minimal-flask-example)
- [Cryptocurrency_Investment_Analysis_and_Modeling](https://github.com/jieyima/Cryptocurrency_Investment_Analysis_and_Modeling)
- [How to Build a Reporting Dashboard using Dash and Plotly](https://towardsdatascience.com/how-to-build-a-complex-reporting-dashboard-using-dash-and-plotl-4f4257c18a7f#4711)
- [Digital Clock : JavaScript](https://bl.ocks.org/mbostock/10685278)
- [PyTables examples](https://github.com/PyTables/PyTables/tree/master/examples)
- [TimeandDate.com เกี่ยวกับวัน + เวลา ศึกษาไว้เป็นแนวทางมีข้อมูลหลากหลาย](https://www.timeanddate.com/worldclock/)


 ## Dash ดึงข้อมูลจาก Yahoo พร้อมแสดงกราฟ  **==แสดงผลสวยงาม==**

```python
import dash
from dash.dependencies import Input, Output
import dash_core_components as dcc
import dash_html_components as html

from pandas_datareader import data as web
from datetime import datetime as dt

app = dash.Dash('Hello World')

app.layout = html.Div([
    dcc.Dropdown(
        id='my-dropdown',
        options=[
            {'label': 'Coke', 'value': 'COKE'},
            {'label': 'Tesla', 'value': 'TSLA'},
            {'label': 'Apple', 'value': 'AAPL'}
        ],
        value='COKE'
    ),
    dcc.Graph(id='my-graph')
], style={'width': '500'})

@app.callback(Output('my-graph', 'figure'), [Input('my-dropdown', 'value')])
def update_graph(selected_dropdown_value):
    df = web.DataReader(
        selected_dropdown_value,
        'yahoo',
        dt(2017, 1, 1),
        dt.now()
    )
    return {
        'data': [{
            'x': df.index,
            'y': df.Close
        }],
        'layout': {'margin': {'l': 40, 'r': 0, 't': 20, 'b': 30}}
    }

app.css.append_css({'external_url': 'https://codepen.io/chriddyp/pen/bWLwgP.css'})

if __name__ == '__main__':
    app.run_server()
  ```

### Bitbucket

Token : 7jC9C8Ar613bOLx5wpeY2C17

### แทรกรูป Gitbook



```
<img src="![](https://miro.medium.com/max/1280/1*41oEHeq_kwMWNX9KQGMtIQ.jpeg)" alt="" border="0";>
```
### Youtube
```
<iframe width="560" height="315"
src="https://www.youtube.com/embed/VBRKLUyi3mw" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe>


<embed  width="800"  height="500"

src="https://www.youtube.com/v/VBRKLUyi3mw">

```

[https://ecs_knowledge_center.gitlab.io/e-customs/e-Import/Manual/data-structure.html#import-declaration-control](https://ecs_knowledge_center.gitlab.io/e-customs/e-Import/Manual/data-structure.html#import-declaration-control)


![enter image description here](https://blog.skooldio.com/wp-content/uploads/2018/02/metrix.gif)



[e-Library by GitLab](https://dragon_e-library.gitlab.io/knowledge_base/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3MDY2MTE0MywtMTY5NDE4NDQ4Miw5NT
UwMTUzMDYsNjg3MjQ1NTE3LC02Mjc5ODI0NDEsLTg2MDgwMjIy
OCwtNTEwMzM0NTY2LDk4NTY5ODM1OSwtNjU2ODUwMTY5LDcyOD
I5MDY0OCwtMjAyNDIzNzg3LC0yNjQ2NzMxNjcsMTg0ODU2MTI2
MywxMjkwNzk2NDcxLDE5MTk0MzU0MjEsMTc4OTgzMjU3NSwtMT
cwMTkzNDY0OSwtMzA1ODY5Njg5LDc5OTkyNTU4NCwxNTQ4NjE1
Nzg1XX0=
-->