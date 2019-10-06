
How to Build a Reporting Dashboard using Dash and Plotly
===

> Written with [StackEdit](https://towardsdatascience.com/how-to-build-a-complex-reporting-dashboard-using-dash-and-plotl-4f4257c18a7f).

In this blog post, I will provide a step-by-step tutorial on how to build a reporting [dashboard](https://davidcomfort-dash-app1.herokuapp.com/cc-travel-report/paid-search/) using [Dash](https://medium.com/@plotlygraphs), a Python framework for building analytical web applications.  Rather than go over the basics of building a Dash app, I provide a detailed guide to building a multi-page dashboard with data tables and graphs.

I built the reporting dashboard as a multi-page app in order to break up the dashboard into different pages so it less overwhelming and to present data in an organized fashion. On each dashboard page, there are two data tables, a date range selector, a data download link, as well as a set of graphs below the two dashboards. I ran into several technical challenges while building the dashboard and I describe in detail how I overcame these challenges.

The completed Dashboard can be viewed at  [https://davidcomfort-dash-app1.herokuapp.com/cc-travel-report/paid-search/](https://davidcomfort-dash-app1.herokuapp.com/cc-travel-report/paid-search/)  and the code is provided in  [Github](https://github.com/davidcomfort/dash_sample_dashboard). (The data used in the app is random data and the names for the products are “dummy” names.)

----------

![](https://miro.medium.com/max/29/1*izIFUYyYhIi8qahMLIsHRg.png?q=20)

![](https://miro.medium.com/max/2234/1*izIFUYyYhIi8qahMLIsHRg.png)

Figure 1: Dashboard built using Dash

![](https://miro.medium.com/max/21/1*7vFIZxM1K4oHE861ahdqVg.png?q=20)

![](https://miro.medium.com/max/1702/1*7vFIZxM1K4oHE861ahdqVg.png)

Figure 2: Second Part of Dashboard

# Table of Contents

-   [**1. Introduction**](https://medium.com/p/4f4257c18a7f#4711)
-   [**2. What am I Trying to Achieve with a Dashboard?**](https://medium.com/p/4f4257c18a7f#a5c5)
-   [**3. Challenges Building the Dashboard**](https://medium.com/p/4f4257c18a7f#05bf)
-   [**4. Creating a New Environment and Installing Dash**](https://medium.com/p/4f4257c18a7f#0bad)
-   [**5. Getting Started with Dash**](https://medium.com/p/4f4257c18a7f#319e)
-   [**6. Building a Multi-page Application**](https://medium.com/p/4f4257c18a7f#eda6)
-   [_Building the Index Page_](https://medium.com/p/4f4257c18a7f#9afd)
-   [_Customizing the Page Title and Favicon_](https://medium.com/p/4f4257c18a7f#f232)
-   [_Overview of the Page Layout_](https://medium.com/p/4f4257c18a7f#906f)
-   [_Local Testing of the App_](https://medium.com/p/4f4257c18a7f#0bbb)
-   [**7. Building the Date Selector Element**](https://medium.com/p/4f4257c18a7f#0d3f)
-   [_Adding a correction to CSS so that the Date Picker is not hidden behind the data tables_](https://medium.com/p/4f4257c18a7f#ed95)
-   [**8. Building the First Data Table**](https://medium.com/p/4f4257c18a7f#63bc)
-   [_Changing the Dates Presented in the Data Table based upon the Date Selection_](https://medium.com/p/4f4257c18a7f#d574)
-   [_Calculating Changes in the Metrics, as well as the calculating cost-per-session, conversion rate, and cost-per-acquisition._](https://medium.com/p/4f4257c18a7f#4b8c)
-   [_A method to select either a condensed data table or the complete data table._](https://medium.com/p/4f4257c18a7f#58a3)
-   [_Conditionally Color-Code Different Data Table cells_](https://medium.com/p/4f4257c18a7f#f5d2)
-   [_Conditional Formatting of Cells using Doppelganger Columns_](https://medium.com/p/4f4257c18a7f#4476)
-   [**9. Building the Download Data link**](https://medium.com/p/4f4257c18a7f#37f2)
-   [**10. Building the Second Data Table**](https://medium.com/p/4f4257c18a7f#ec15)
-   [**11. Updating Graphs by Selecting Rows in a Dash Data table**](https://medium.com/p/4f4257c18a7f#b125)
-   [_Step 1_](https://medium.com/p/4f4257c18a7f#2d4a)
-   [_Step 2_](https://medium.com/p/4f4257c18a7f#672c)
-   [_Step 3_](https://medium.com/p/4f4257c18a7f#5506)
-   [**12. Updating the Graphs and Calculating metrics on the fly**](https://medium.com/p/4f4257c18a7f#7fea)
-   [**13. Plotly Graph Tools**](https://medium.com/p/4f4257c18a7f#7a84)
-   [**14. Deploying the Dashboard**](https://medium.com/p/4f4257c18a7f#33e7)
-   [_Resolving an Issue with Custom.css File and Authentication_](https://medium.com/p/4f4257c18a7f#8520)
-   [_Dash Deployment Server_](https://medium.com/p/4f4257c18a7f#d025)
-   [**15. Wrapping up**](https://medium.com/p/4f4257c18a7f#44e2)
-   [**16. Resources for Dash**](https://medium.com/p/4f4257c18a7f#b300)

----------

# 1. Introduction

In January of this year, I went to my first PyData conference,  [PyData Miami](https://pydata.org/miami2019/), and sat in on a great  [presentation](https://www.youtube.com/watch?v=eusglTlW4OA)  by Chelsea Douglas about  [Dash](https://plot.ly/products/dash/).

Embedded Video 1: Dash: data exploration web apps in pure Python — Chelsea Douglas

It quickly became apparent how powerful Dash was and how I easily I could build web apps and dashboards using Python.

From my perspective, there was a real need in my company to automate reporting, replace Microsoft Excel pivot tables and spreadsheets, and provide an alternative to Business Intelligence tools. Even though various stakeholders in my company have relied upon Excel spreadsheets for regular reporting, their usage becomes unwieldy, they are prone to error, they are not platform independent, and they do not lend themselves to automation.

Therefore, I endeavored to build a multi-page web application using Dash. This article goes into the nitty, gritty details of my efforts and how I overcame several technical challenges. I should note that I come from a data scientist perspective and make no claims to be a software developer. Hence, there certainly is room for improvement in my code and I would welcome the reader’s suggestions. At the same time, I hope the reader can benefit from my efforts if they need to build complex dashboards and data tables.

----------

# 2. What am I Trying to Achieve with a Dashboard?

At my present company, a lot of periodic reporting is done either with Excel spreadsheets and pivot tables, or using business intelligence tools such as  [Birst](https://www.birst.com/)  or  [Qlikview](https://www.qlik.com/us/products/qlikview). Hence, I wanted to build a reporting dashboard as a proof-of-concept that could replace and enhance our reporting. Specifically, I wanted to build a reporting web application for one of brands, which could report out on different marketing channel metrics, enable automation and provide ease of access.

The requirements for the  **E-commerce Marketing Dashboard**  included:

-   Break out the different marketing channels into different pages so that the amount of data presented in the dashboard would not be overwhelming.
-   A date selector so a user can select a date range to filter the data.
-   A data table to present basic metrics (spend, sessions, number of transactions, and revenue) for each digital marketing channel or product type for the date range selected, as well as for the same period last year and a corresponding period prior to the date range selected.*
-   Another data table to present calculated metrics for the date range selected (as well as for the same period last year and prior period). These metrics include cost-per-session (CPS), conversion rate (CVR), and CPA (cost-per-acquisition).
-   A link to download the data (in Excel format) that is displayed in each data table.
-   Graphs of the metrics on a weekly basis are to be depicted below the data tables.
-   _An example of a corresponding prior period would be if a user selected week numbers 5 and 6 of 2019, then the corresponding prior period would be week numbers 3 and 4 of 2019._

----------

# 3. Challenges Building the Dashboard

There were multiple challenges that cropped up when I was building the dashboard app. Some of the main challenges included:

-   Figuring out a method to display either a condensed data table or a complete data table.
-   Having the ability to color code cells in the data tables, based upon the value in that cell.
-   Having the ability to select multiple products to include in a graphical representation of the data.
-   Having the ability to update the metrics in the data tables on-the-fly, depending upon the date range a user selects.
-   Having the ability to download the data presented in the data tables without any added formatting.
-   Depicting year-to-year changes in metrics on the same x-axis as a given metric.
-   Being able to zoom in on all graphs at the same time.

----------

# 4. Creating a New Environment and Installing Dash

There is a  [Dash User Guide](https://dash.plot.ly/), which provides a fairly thorough introduction to Dash and I encourage the reader to go through the user guide and build some simple Dash apps prior to tackling a full fledged dashboard. In addition, there is a  [Dash Community Forum](https://community.plot.ly/c/dash), a  [show-and-tell](https://community.plot.ly/t/show-and-tell-community-thread/7554)  section of the forum highlighting work by the Dash community, a  [gallery](https://dash.plot.ly/gallery)  of Dash projects, a curated list of  [awesome Dash](https://github.com/ucg8j/awesome-dash)  resources, and an introductory essay about Dash:

> [Dash](https://plot.ly/products/dash)  is a Open Source Python library for creating reactive, Web-based applications. Dash started as a public proof-of-concept on GitHub 2 years ago. We kept this prototype online, but subsequent work on Dash occurred behind closed doors. We used feedback from private trials at banks, labs, and data science teams to guide the product forward.  **Today, we’re excited to announce the first public release of Dash that is both enterprise-ready and a first-class member of Plotly’s open-source tools.**  Dash can be downloaded today from Python’s package manager with  `pip install dash`  — it’s entirely open-source and MIT licensed. You’ll find a  [getting started guide here](https://plot.ly/dash)  and the  [Dash code on GitHub here](https://github.com/plotly/dash).
> 
> Dash is a user interface library for creating analytical web applications. Those who use Python for data analysis, data exploration, visualization, modelling, instrument control, and reporting will find immediate use for Dash.
> 
> Dash makes it dead-simple to build a GUI around your data analysis code.

Prior to installing Dash, as is the usual practice, I created a new environment using  [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html):  `conda create --name dash`  and then activated that environment,  `conda activate dash`. I then simply followed the  [Dash installation protocol](https://dash.plot.ly/installation)  provided in the user guide:
``` py
pip install dash==0.39.0  # The core dash backend
pip install dash-html-components==0.14.0  # HTML components
pip install dash-core-components==0.44.0  # Supercharged components
pip install dash-table==3.6.0  # Interactive DataTable component (new!)
pip install dash-daq==0.1.0  # DAQ components (newly open-sourced!)
``` 
I should note that the versions for Dash and its components will change from above and you should refer to the  [User Guide](https://dash.plot.ly/installation).

----------

# 5. Getting Started with Dash

There are already quite a few tutorials for Dash, so I will focus on how to build a multi-page dashboard with data tables and graphs in this tutorial, rather than go over the basics of building a Dash app.

If you are just getting started in Dash, I would encourage the reader to go through at least the first three sections of the excellent  [Dash User Guide](https://dash.plot.ly/). There is also a section on the  [Dash Data Table](https://dash.plot.ly/datatable). There are several tutorials to get you started*****:

-   [Introducing Plotly Dash](https://medium.com/@plotlygraphs/introducing-dash-5ecf7191b503)  — A high level introduction to Dash by Chris Parmer, the author of Dash. This essay was released as part of Dash’s official launch (June 21, 2017).
-   [Plotly’s tutorials — Part 1: App Layout](https://plot.ly/dash/getting-started)
-   [Plotly’s tutorials — Part 2: Interactivity](https://plot.ly/dash/getting-started-part-2)
-   [Plotly’s tutorials — Part 3: Interactive Graphing](https://plot.ly/dash/interactive-graphing)
-   [Plotly’s tutorials — Part 4: Callbacks With State](https://plot.ly/dash/state)
-   [Interactive Web-Based Dashboards in Python](https://alysivji.github.io/reactive-dashboards-with-dash.html)  — How the MVC model pertains to Dash and a walkthrough of building an app.
-   [Using Plotly’s Dash to deliver public sector decision support dashboards](https://medium.com/a-r-g-o/using-plotlys-dash-to-deliver-public-sector-decision-support-dashboards-ac863fa829fb)  — Building a complex dashboard step-by-step.
-   [OPS CodeDay: Dash Plotly Map + Graph](https://radumas.info/blog/tutorial/2017/08/10/codeday.html)  — How to use Jupyter notebooks in tandem with Dash to create mapping viz.
-   [Creating Interactive Visualizations with Plotly’s Dash Framework](http://pbpython.com/plotly-dash-intro.html)  — High level overview of how to get started with Dash.
-   [Finding Bigfoot with Dash, Part 1](https://timothyrenner.github.io/datascience/2017/08/08/finding-bigfoot-with-dash-part-1.html)  — Walkthrough of building a dashboard of Bigfoot sightings.  [Part 2](https://timothyrenner.github.io/datascience/2017/08/09/finding-bigfoot-with-dash-part-2.html),  [Part 3](https://timothyrenner.github.io/datascience/2017/08/10/finding-bigfoot-with-dash-part-3.html).
-   [Visualize Earthquakes with Plotly Dash](https://www.giacomodebidda.com/visualize-earthquakes-with-plotly-dash/)  — Environmental scan of alternatives to Dash followed with a tutorial.
-   [ARGO Labs — Plotly Dash Tutorial (Video)](https://www.youtube.com/watch?v=yfWJXkySfe0)  — Detailed introduction to creating interactive dashboards.
-   [Data Visualization GUIs with Dash and Python (Video playlist)](https://www.youtube.com/watch?v=J_Cy_QjG6NE&list=PLQVvvaa0QuDfsGImWNt1eUEveHOepkjqt)  — Five-part series exploring Dash features.

*****_From the_ [_Awesome Dash Github_](https://github.com/ucg8j/awesome-dash) _page._

Essentially, Dash apps are composed of two parts: (1) the “_layout_” of the app that describes the look and feel of the app, and (2) the “_callbacks_” that enable the apps to be interactive. A simple Dash App Layout is presented in the user guide and reproduced below:
``` py
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

app.layout = html.Div([
    dcc.Input(id='my-id', value='initial value', type='text'),
    html.Div(id='my-div')
])


@app.callback(
    Output(component_id='my-div', component_property='children'),
    [Input(component_id='my-id', component_property='value')]
)
def update_output_div(input_value):
    return 'You\'ve entered "{}"'.format(input_value)


if __name__ == '__main__':
    app.run_server(debug=True)
``` 

The dashboard which I describe in this tutorial splits up the Dash app into different files and enables one to build a multi-page app.

There is an “index” page which renders different pages, or layouts, depending the URL. Each individual layout consists of several different Dash components, including a date range picker, data tables, a download link, and several graphs. Each of these components is related to one or more “callbacks” that enable the dashboard to be interactive.

A user can interact with one of the Dash components (e.g., change the date range) and the other components reflect this change (e.g., cause the data presented in the data tables to change).

A schematic of this approach is in the following diagram:

![](https://miro.medium.com/max/30/1*2xze0C6T3SQweRhRQwbOzg.png?q=20)

![](https://miro.medium.com/max/2152/1*2xze0C6T3SQweRhRQwbOzg.png)

Figure 3: Schematic of Dashboard files

----------

# 6. Building a Multi-page Application

The structure of multi-page Dash application, based upon the Dash documentation at  [https://dash.plot.ly/urls](https://dash.plot.ly/urls), with slight tweaks, is presented below:
```py
- __init__.py
- app.py
- assets
    |-- logo.jpeg
    |-- custom.css
    |-- favicon.ico
- callbacks.py
- components
    |-- __init__.py
    |-- functions.py
    |-- header.py
    |-- printButton.py
- data
    |-- datafile.csv
- index.py
- layouts.py
- Procfile
- requirements.txt
```
The file  `app.py` simply has the following:

```py
import dash
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']
app = dash.Dash(__name__, external_stylesheets=external_stylesheets, url_base_pathname='/cc-travel-report/paid-search/')
server = app.server
app.config.suppress_callback_exceptions = True
import dash_auth
# Keep this out of source code repository - save in a file or a database
VALID_USERNAME_PASSWORD_PAIRS = [
    ['[username]', '[password']
]
auth = dash_auth.BasicAuth(
    app,
    VALID_USERNAME_PASSWORD_PAIRS
)
```

Note that I am using the dash authentication module ([https://dash.plot.ly/authentication](https://dash.plot.ly/authentication)). This has some implications which I will go into below.

## Building the Index Page

The  `index.py`  file essentially defines the URL page structure of the app by defining a function  `display_page`, which determines what page layout should be rendered depending upon the app URL.

```py
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output

# see https://community.plot.ly/t/nolayoutexception-on-deployment-of-multi-page-dash-app-example-code/12463/2?u=dcomfort
from app import server
from app import app
from layouts import layout_birst_category, layout_ga_category, layout_paid_search, noPage, layout_display, layout_publishing, layout_metasearch
import callbacks

# see https://dash.plot.ly/external-resources to alter header, footer and favicon
app.index_string = ''' 
<!DOCTYPE html>
<html>
    <head>
        {%metas%}
        <title>CC Performance Marketing Report</title>
        {%favicon%}
        {%css%}
    </head>
    <body>
        {%app_entry%}
        <footer>
            {%config%}
            {%scripts%}
        </footer>
        <div>CC Performance Marketing Report</div>
    </body>
</html>
'''

app.layout = html.Div([
    dcc.Location(id='url', refresh=False),
    html.Div(id='page-content')
])

# Update page
# # # # # # # # #
@app.callback(Output('page-content', 'children'),
              [Input('url', 'pathname')])
def display_page(pathname):
    if pathname == '/cc-travel-report' or pathname == '/cc-travel-report/overview-birst/':
        return layout_birst_category
    elif pathname == '/cc-travel-report/overview-ga/':
        return layout_ga_category
    elif pathname == '/cc-travel-report/paid-search/':
        return layout_paid_search
    elif pathname == '/cc-travel-report/display/':
        return layout_display
    elif pathname == '/cc-travel-report/publishing/':
        return layout_publishing
    elif pathname == '/cc-travel-report/metasearch-and-travel-ads/':
        return layout_metasearch
    else:
        return noPage

# # # # # # # # #
external_css = ["https://cdnjs.cloudflare.com/ajax/libs/normalize/7.0.0/normalize.min.css",
                "https://cdnjs.cloudflare.com/ajax/libs/skeleton/2.0.4/skeleton.min.css",
                "//fonts.googleapis.com/css?family=Raleway:400,300,600",
                "https://codepen.io/bcd/pen/KQrXdb.css",
                "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css",
                "https://codepen.io/dmcomfort/pen/JzdzEZ.css"]

for css in external_css:
    app.css.append_css({"external_url": css})

external_js = ["https://code.jquery.com/jquery-3.2.1.min.js",
               "https://codepen.io/bcd/pen/YaXojL.js"]

for js in external_js:
    app.scripts.append_script({"external_url": js})

if __name__ == '__main__':
    app.run_server(debug=True)
```

This is very similar to the  `index.py`  page in the Dash Vanguard eport at  [https://github.com/plotly/dash-vanguard-report](https://github.com/plotly/dash-vanguard-report), with a demo at ([https://dash-gallery.plotly.host/dash-vanguard-report/portfolio-management](https://dash-gallery.plotly.host/dash-vanguard-report/portfolio-management)).

However, I had to include the line  `from app import server`, in order to overcome an issue when I deployed the app on Heroku (see  [https://community.plot.ly/t/nolayoutexception-on-deployment-of-multi-page-dash-app-example-code/12463](https://community.plot.ly/t/nolayoutexception-on-deployment-of-multi-page-dash-app-example-code/12463)  for details).

## Customizing the Page Title and Favicon

In addition, I wanted to customize the app’s HTML index template, specifically, the page title and the favicon. In order to do so, I added the following  `index_string:`  to  `index.py`:

```py
# see https://dash.plot.ly/external-resources to alter header, footer and favicon
app.index_string = ''' 
<!DOCTYPE html>
<html>
    <head>
        {%metas%}
        <title>CC Performance Marketing Report</title>
        {%favicon%}
        {%css%}
    </head>
    <body>
        {%app_entry%}
        <footer>
            {%config%}
            {%scripts%}
        </footer>
        <div>CC Performance Marketing Report</div>
    </body>
</html>
'''
```

In order to order to customize the favicon, the  `favicon.ico`  image can be placed in the assets directory.

## Overview of the Page Layout

The callback in the  `index.py`  file takes as input the app URL and outputs different layouts depending upon the layout:

```py
# Update page
# # # # # # # # #
@app.callback(Output('page-content', 'children'),
              [Input('url', 'pathname')])
def display_page(pathname):
    if pathname == '/cc-travel-report' or pathname == '/cc-travel-report/overview-birst/':
        return layout_birst_category
    elif pathname == '/cc-travel-report/overview-ga/':
        return layout_ga_category
    elif pathname == '/cc-travel-report/paid-search/':
        return layout_paid_search
    elif pathname == '/cc-travel-report/display/':
        return layout_display
    elif pathname == '/cc-travel-report/publishing/':
        return layout_publishing
    elif pathname == '/cc-travel-report/metasearch-and-travel-ads/':
        return layout_metasearch
    else:
        return noPage
```

The  `layouts.py`  file contains the following:

-   Normal python import statements
-   Statement to read in the data CSV file into pandas data frame
-   Definition of the data table columns needed in the different variations of the layouts
-   Definition of each page layout section
-   Definition of the`noPage` layout

The beginning of the  `layouts.py`  file is as follows:

```py
import dash_core_components as dcc
import dash_html_components as html
import dash_table
from components import Header, print_button
from datetime import datetime as dt
from datetime import date, timedelta
import pandas as pd


# Read in Travel Report Data
df = pd.read_csv('data/performance_analytics_cost_and_ga_metrics.csv')

df.rename(columns={
 'Travel Product': 'Placement type', 
  'Spend - This Year': 'Spend TY', 
  'Spend - Last Year': 'Spend LY', 
  'Sessions - This Year': 'Sessions - TY',
  'Sessions - Last Year': 'Sessions - LY',
  'Bookings - This Year': 'Bookings - TY',
  'Bookings - Last Year': 'Bookings - LY',
  'Revenue - This Year': 'Revenue - TY',
  'Revenue - Last Year': 'Revenue - LY',
  }, inplace=True)


df['Date'] = pd.to_datetime(df['Date'])
current_year = df['Year'].max()

dt_columns = ['Placement type', 'Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)', \
                        'Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 'Sessions YoY (%)', \
                        'Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)', \
                        'Revenue - TY', 'Revenue - LP', 'Revenue PoP (Abs)', 'Revenue PoP (%)', 'Revenue - LY', 'Revenue YoY (%)', 'Revenue YoY (Abs)',]

conditional_columns = ['Spend_PoP_abs_conditional', 'Spend_PoP_percent_conditional', 'Spend_YoY_percent_conditional',
'Sessions_PoP_percent_conditional', 'Sessions_YoY_percent_conditional', 
'Bookings_PoP_abs_conditional', 'Bookings_YoY_abs_conditional', 'Bookings_PoP_percent_conditional', 'Bookings_YoY_percent_conditional',
'Revenue_PoP_abs_conditional', 'Revenue_YoY_abs_conditional', 'Revenue_PoP_percent_conditional', 'Revenue_YoY_percent_conditional',]

dt_columns_total = ['Placement type', 'Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)', \
                        'Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 'Sessions YoY (%)', \
                        'Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)', \
                        'Revenue - TY', 'Revenue - LP', 'Revenue PoP (Abs)', 'Revenue PoP (%)', 'Revenue - LY', 'Revenue YoY (%)', 'Revenue YoY (Abs)',
                        'Spend_PoP_abs_conditional', 'Spend_PoP_percent_conditional', 'Spend_YoY_percent_conditional',
'Sessions_PoP_percent_conditional', 'Sessions_YoY_percent_conditional', 
'Bookings_PoP_abs_conditional', 'Bookings_YoY_abs_conditional', 'Bookings_PoP_percent_conditional', 'Bookings_YoY_percent_conditional',
'Revenue_PoP_abs_conditional', 'Revenue_YoY_abs_conditional', 'Revenue_PoP_percent_conditional', 'Revenue_YoY_percent_conditional',]

df_columns_calculated = ['Placement type', 'CPS - TY', 
                        'CPS - LP', 'CPS PoP (Abs)', 'CPS PoP (%)',
                        'CPS - LY',  'CPS YoY (Abs)',  'CPS YoY (%)', 
                        'CVR - TY', 
                        'CVR - LP', 'CVR PoP (Abs)', 'CVR PoP (%)',
                        'CVR - LY',  'CVR YoY (Abs)',  'CVR YoY (%)',
                        'CPA - TY', 
                        'CPA - LP', 'CPA PoP (Abs)', 'CPA PoP (%)',
                        'CPA - LY', 'CPA YoY (Abs)',  'CPA YoY (%)']

conditional_columns_calculated_calculated = ['CPS_PoP_abs_conditional', 'CPS_PoP_percent_conditional', 'CPS_YoY_abs_conditional', 'CPS_PoP_percent_conditional', 
'CVR_PoP_abs_conditional', 'CVR_PoP_percent_conditional', 'CVR_YoY_abs_conditional', 'CVR_YoY_percent_conditional',
'CPA_PoP_abs_conditional', 'CPA_PoP_percent_conditional', 'CPA_YoY_abs_conditional', 'CPA_YoY_percent_conditional']
```

Each page layout section contains the following elements:

-   Call to  `Header()`  which is imported, so one can have common elements (logo, brand name, etc.) across multiple apps.
-   Data Range element
-   Header Bar
-   Radio Button to select condensed vs. complete data frame
-   First data table
-   Download button
-   Second data table
-   Graphs

A simplified code block for one layout section in the  `layouts.py`  is below:

```py
######################## START Paid Search Layout ########################
layout_paid_search =  html.Div([
    html.Div([
        # CC Header
        Header(),
        # Date Picker
        html.Div([
            dcc.DatePickerRange(
              id='my-date-picker-range-paid-search',
              min_date_allowed=dt(2018, 1, 1),
              max_date_allowed=df['Date'].max().to_pydatetime(),
              initial_visible_month=dt(current_year,df['Date'].max().to_pydatetime().month, 1),
              start_date=(df['Date'].max() - timedelta(6)).to_pydatetime(),
              end_date=df['Date'].max().to_pydatetime(),
            ),
            html.Div(id='output-container-date-picker-range-paid-search')
            ], className="row ", style={'marginTop': 30, 'marginBottom': 15}),
        # Header Bar
        html.Div([
          html.H6(["Paid Search"], className="gs-header gs-text-header padded",style={'marginTop': 15})
          ]),
        # Radio Button
        html.Div([
          dcc.RadioItems(
            options=[
                {'label': 'Condensed Data Table', 'value': 'Condensed'},
                {'label': 'Complete Data Table', 'value': 'Complete'},
            ], value='Condensed',
            labelStyle={'display': 'inline-block', 'width': '20%', 'margin':'auto', 'marginTop': 15, 'paddingLeft': 15},
            id='radio-button-paid-search'
            )]),
        # First Data Table
        html.Div([
            dash_table.DataTable(
                id='datatable-paid-search',
                columns=[{"name": i, "id": i, 'deletable': True} for i in dt_columns] 
                + [{"name": j, "id": j, 'hidden': 'True'} for j in conditional_columns], 
                editable=True,
                n_fixed_columns=2,
                style_table={'maxWidth': '1500px'},
                row_selectable="multi",
                selected_rows=[0],
                ),
            ], className=" twelve columns"),
        # Download Button
        html.Div([
          html.A(html.Button('Download Data', id='download-button'), id='download-link-paid-search-1')
          ]),
        # Second Data Table
        html.Div([
            dash_table.DataTable(
              id='datatable-paid-search-2',
              columns=[{"name": i, "id": i} for i in df_columns_calculated] + 
              [{"name": k, "id": k, 'hidden': 'True'} for k in conditional_columns_calculated_calculated],
              editable=True,
              n_fixed_columns=1,
              css=[{'selector': '.dash-cell div.dash-cell-value', 'rule': 'display: inline; white-space: inherit; overflow: inherit; text-overflow: inherit;'}],
              style_table={'maxWidth': '1500px'}, 
                ),
            ], className=" twelve columns"),
        # GRAPHS
        html.Div([
            html.Div([
              dcc.Graph(id='paid-search'),
              ], className=" twelve columns"
              )
            ], className="row ")
        ], className="subpage")
    ], className="page")
```

The above code does not include conditional formatting, which I will go into below.

## Local Testing of the App

Following the user guide, after one has created the  `index.py`  and  `app.py`  files, one invokes the app with
```py
$ python app.py  
```
...Running on http://127.0.0.1:8050/ (Press CTRL+C to quit)

and visit  [```http:127.0.0.1:8050/cc-travel-report/paid-search/](http://127.0.0.1:8050/cc-travel-report/paid-search/)  in your web browser.

----------

# 7. Building the Date Selector Element

![](https://miro.medium.com/max/30/1*EFUNX2eoDCBmDKQxGzEeAA.png?q=20)

![](https://miro.medium.com/max/1882/1*EFUNX2eoDCBmDKQxGzEeAA.png)

Figure 4: Date Selector Element

The date selector element provided a means to update the data presented in both data tables, as well as the downloaded data link. I also wanted the date selector to provide feedback on the dates selected by the user.

I simply chose January 1, 2018 as the minimum date allowed (`min_date_allowed`); The maximum date allowed was based upon the maximum date in the CSV data file (`max_date_allowed`); the initial month presented in the date selected was based upon the maximum date in the CSV data file (`initial_visible_month`); the initial start date was the maximum date minus 6 days (`start_date`); and the initial end date was the maximum date.

The following code is located in the  `layouts.py`  file and needs to be repeated for each “page” of the Dashboard app.

```py
# Date Picker
html.Div([
    dcc.DatePickerRange(
      id='my-date-picker-range-paid-search',
      min_date_allowed=dt(2018, 1, 1),
      max_date_allowed=df['Date'].max().to_pydatetime(),
      initial_visible_month=dt(current_year,df['Date'].max().to_pydatetime().month, 1),
      start_date=(df['Date'].max() - timedelta(6)).to_pydatetime(),
      end_date=df['Date'].max().to_pydatetime(),
    ),
    html.Div(id='output-container-date-picker-range-paid-search')
    ], className="row ", style={'marginTop': 30, 'marginBottom': 15}),
```
I used a callback and a function,  `update_output`  to provide feedback to the user. Specifically, I wanted to provide text feedback on the dates selected, the number of days selected, as well as the dates in the corresponding previous period. For instance, if a user had selected week numbers 5 and 6 of 2019 using the date range selector, then the corresponding past period would be week numbers 3 and 4 of 2019. The  `update_output`  function below provides this functionality.

```py
#### Date Picker Callback
@app.callback(Output('output-container-date-picker-range-paid-search', 'children'),
	[Input('my-date-picker-range-paid-search', 'start_date'),
	 Input('my-date-picker-range-paid-search', 'end_date')])
def update_output(start_date, end_date):
	string_prefix = 'You have selected '
	if start_date is not None:
		start_date = dt.strptime(start_date, '%Y-%m-%d')
		start_date_string = start_date.strftime('%B %d, %Y')
		string_prefix = string_prefix + 'a Start Date of ' + start_date_string + ' | '
	if end_date is not None:
		end_date = dt.strptime(end_date, '%Y-%m-%d')
		end_date_string = end_date.strftime('%B %d, %Y')
		days_selected = (end_date - start_date).days
		prior_start_date = start_date - timedelta(days_selected + 1)
		prior_start_date_string = datetime.strftime(prior_start_date, '%B %d, %Y')
		prior_end_date = end_date - timedelta(days_selected + 1)
		prior_end_date_string = datetime.strftime(prior_end_date, '%B %d, %Y')
		string_prefix = string_prefix + 'End Date of ' + end_date_string + ', for a total of ' + str(days_selected + 1) + ' Days. The prior period Start Date was ' + \
		prior_start_date_string + ' | End Date: ' + prior_end_date_string + '.'
	if len(string_prefix) == len('You have selected: '):
		return 'Select a date to see it displayed here'
	else:
		return string_prefix
```

The date picker element provides input to the callbacks for the first data table, the second data table, the download link, as well as the set of graphs below the data tables. I will go into detail how each of these callbacks work, with their associated outputs.

## Adding a correction to CSS so that the Date Picker is not hidden behind the data tables

One issue I had to correct was that the data tables obscured the date picker element, so I had to correct the CSS accordingly.

```py
#datatable-paid-search > div > div > div.row.row-1 > div.cell.cell-1-0.dash-fixed-column {
    flex: 0 0 auto;
    left: 0;
    position: sticky;
    z-index: 0;
}
```

----------

# 8. Building the First Data Table

![](https://miro.medium.com/max/30/1*9UpPeoKW37MEFAjetTA4Iw.png?q=20)

![](https://miro.medium.com/max/2242/1*9UpPeoKW37MEFAjetTA4Iw.png)

Figure 5: First Data Table with a Condensed View

The first data table in the dashboard presents metrics such as spend (the cost associated with a given advertising product), website sessions, bookings (transactions), and revenue. These metrics are aggregated depending upon the dates selected in the date selected and typically present data for the current year for the date range selected, data for the previous corresponding period, data for last year, as well as percent and absolute differences between these periods.

## Changing the Dates Presented in the Data Table based upon the Date Selection

The main functionality I wanted for the first data table is making it interactive, whereby the data presented changes according in the date selected. To start with, the data table element needs to be included in the  `layouts.py`  file as in the (simplified) code below:

```py
# First Data Table
html.Div([
    dash_table.DataTable(
        id='datatable-paid-search',
        columns=[{"name": i, "id": i, 'deletable': True} for i in dt_columns], 
        editable=True,
        n_fixed_columns=2,
        style_table={'maxWidth': '1500px'},
        row_selectable="multi",
        selected_rows=[0],
        style_cell = {"fontFamily": "Arial", "size": 10, 'textAlign': 'left'}
        )
    ], className=" twelve columns")
```

The different parameters for the data table include:

-   `id`  : identifier so that the data table can be referenced by the callbacks.
-   `columns`  : the columns presented in the table;  `deletable`  gives the ability of the user to delete the column while using the app.
-   `editable=True`  gives the user the ability to change the data in the table while using the app.
-   `n_fixed_columns=2`  freezes the first two columns (the checkboxes and the placement type in our case), so when a user scrolls across the complete data table, the user can still view the check boxes and the placement type.
-   `style_table`  allows CSS styles to be applied to the table.
-   `row_selectable='multi'`  allows the user to select multiple rows via the checkboxes. This will enable updating of the graphs below based upon the selection.
-   `selected_rows=0`  contains the index of the rows that are selected initially (and presented in the graphs below).
-   `style_cell`  allows CSS styles to be applied to the table cells.

I will add additional parameters in a subsequent step so we can have conditional style formatting. Number formatting such as dollar signs, commas, and percent signs are added in pandas and defined as a series of formatters.

I should note that I do not specify the  `data`  parameter for the data table in the  `layouts.py`  file. Rather, the  `data`  parameter for the data table will come from the callback:

```py
# Callback and update first data table
@app.callback(Output('datatable-paid-search', 'data'),
	[Input('my-date-picker-range-paid-search', 'start_date'),
	 Input('my-date-picker-range-paid-search', 'end_date')])
def update_data_1(start_date, end_date):
	data_1 = update_first_datatable(start_date, end_date, 'Paid Search', 'Placement type')
	return data_1
```

## Calculating Changes in the Metrics, as well as the calculating cost-per-session, conversion rate, and cost-per-acquisition.

Since we need to calculate changes in the metrics, as well as CPA, CPS, and conversion rate depending upon the dates selected “on-the-fly,” I push these calculations into a separate file,  `functions.py`. I can then re-use these functions for the different Dashboard pages. I also define formatting functions in this file:

```py

# Define Formatters
def formatter_currency(x):
	return "${:,.0f}".format(x) if x >= 0 else "(${:,.0f})".format(abs(x))

def formatter_currency_with_cents(x):
	return "${:,.2f}".format(x) if x >= 0 else "(${:,.2f})".format(abs(x))

def formatter_percent(x):
	return "{:,.1f}%".format(x) if x >= 0 else "({:,.1f}%)".format(abs(x))

def formatter_percent_2_digits(x):
	return "{:,.2f}%".format(x) if x >= 0 else "({:,.2f}%)".format(abs(x))

def formatter_number(x):
	return "{:,.0f}".format(x) if x >= 0 else "({:,.0f})".format(abs(x))
```

The functions for both the first data table and the second data table are similar so I only present one here:

```py
# First Data Table Update Function
def update_first_datatable(start_date, end_date, category, aggregation):
	if start_date is not None:
		start_date = dt.strptime(start_date, '%Y-%m-%d')
		start_date_string = start_date.strftime('%Y-%m-%d')
	if end_date is not None:
		end_date = dt.strptime(end_date, '%Y-%m-%d')
		end_date_string = end_date.strftime('%Y-%m-%d')
	days_selected = (end_date - start_date).days

	prior_start_date = start_date - timedelta(days_selected + 1)
	prior_start_date_string = datetime.strftime(prior_start_date, '%Y-%m-%d')
	prior_end_date = end_date - timedelta(days_selected + 1)
	prior_end_date_string = datetime.strftime(prior_end_date, '%Y-%m-%d')

	if aggregation == 'Placement type':
		df1 = df[(df['Category'] == category)].groupby(['Date', aggregation]).sum()[columns].reset_index()
		df_by_date = df1[(df1['Date'] >= start_date_string) & (df1['Date'] <= end_date_string)].groupby([aggregation]).sum()[columns].reset_index()
		df_by_date_prior = df1[(df1['Date'] >= prior_start_date_string) & (df1['Date'] <= prior_end_date_string)].groupby([aggregation]).sum()[['Spend TY', 'Sessions - TY', 'Bookings - TY', 'Revenue - TY']].reset_index()
		df_by_date_prior.rename(columns={'Spend TY' : 'Spend - LP', 'Sessions - TY' : 'Sessions - LP',  'Bookings - TY' : 'Bookings - LP','Revenue - TY' : 'Revenue - LP'}, inplace=True)
		df_by_date_combined =  pd.merge(df_by_date, df_by_date_prior, on=[aggregation])
	elif aggregation == 'GA Category':
		df1 = df.groupby(['Date', aggregation]).sum()[columns].reset_index()
		df_by_date = df1[(df1['Date'] >= start_date_string) & (df1['Date'] <= end_date_string)].groupby([aggregation]).sum()[columns].reset_index()
		df_by_date_prior = df1[(df1['Date'] >= prior_start_date_string) & (df1['Date'] <= prior_end_date_string)].groupby([aggregation]).sum()[['Spend TY', 'Sessions - TY', 'Bookings - TY', 'Revenue - TY']].reset_index()
		df_by_date_prior.rename(columns={'Spend TY' : 'Spend - LP', 'Sessions - TY' : 'Sessions - LP',  'Bookings - TY' : 'Bookings - LP','Revenue - TY' : 'Revenue - LP'}, inplace=True)
		df_by_date_combined =  pd.merge(df_by_date, df_by_date_prior, on=[aggregation])
		df_by_date_combined.rename(columns={'GA Category':'Placement type'}, inplace=True)
	elif aggregation == 'Birst Category':
		df1 = df.groupby(['Date', aggregation]).sum()[columns].reset_index()
		df_by_date = df1[(df1['Date'] >= start_date_string) & (df1['Date'] <= end_date_string)].groupby([aggregation]).sum()[columns].reset_index()
		df_by_date_prior = df1[(df1['Date'] >= prior_start_date_string) & (df1['Date'] <= prior_end_date_string)].groupby([aggregation]).sum()[['Spend TY', 'Sessions - TY', 'Bookings - TY', 'Revenue - TY']].reset_index()
		df_by_date_prior.rename(columns={'Spend TY' : 'Spend - LP', 'Sessions - TY' : 'Sessions - LP',  'Bookings - TY' : 'Bookings - LP','Revenue - TY' : 'Revenue - LP'}, inplace=True)
		df_by_date_combined =  pd.merge(df_by_date, df_by_date_prior, on=[aggregation])
		df_by_date_combined.rename(columns={'Birst Category':'Placement type'}, inplace=True)

	# Calculate Differences on-the-fly
	df_by_date_combined['Spend PoP (%)'] = np.nan
	df_by_date_combined['Spend YoY (%)'] = np.nan
	df_by_date_combined['Sessions PoP (%)'] = np.nan
	df_by_date_combined['Sessions YoY (%)'] = np.nan
	df_by_date_combined['Bookings PoP (%)'] = np.nan
	df_by_date_combined['Bookings YoY (%)'] = np.nan
	df_by_date_combined['Revenue PoP (%)'] = np.nan
	df_by_date_combined['Revenue YoY (%)'] = np.nan

	df_by_date_combined['Spend_PoP_abs_conditional'] = df_by_date_combined['Spend PoP (Abs)'] = ((df_by_date_combined['Spend TY'] - df_by_date_combined['Spend - LP']))
	# Formatter
	df_by_date_combined['Spend PoP (Abs)'] = df_by_date_combined['Spend PoP (Abs)'].apply(formatter_currency)

	df_by_date_combined['Spend_PoP_percent_conditional'] = df_by_date_combined['Spend PoP (%)'] = np.where((df_by_date_combined['Spend TY'] != 0) &  (df_by_date_combined['Spend - LP'] != 0),\
		(((df_by_date_combined['Spend TY'] - df_by_date_combined['Spend - LP'])/df_by_date_combined['Spend - LP']) * 100), df_by_date_combined['Spend PoP (%)'])
	# Formatter
	df_by_date_combined['Spend PoP (%)'] = np.where((df_by_date_combined['Spend TY'] != 0) &  (df_by_date_combined['Spend - LP'] != 0),\
		df_by_date_combined['Spend PoP (%)'].apply(formatter_percent), df_by_date_combined['Spend PoP (%)'])

	df_by_date_combined['Spend_YoY_percent_conditional'] = df_by_date_combined['Spend YoY (%)'] = np.where((df_by_date_combined['Spend TY'] != 0) &  (df_by_date_combined['Spend LY'] != 0),\
		((df_by_date_combined['Spend TY'] - df_by_date_combined['Spend LY'])/df_by_date_combined['Spend LY']) * 100, df_by_date_combined['Spend YoY (%)'])
	# Formatter
	df_by_date_combined['Spend YoY (%)'] = np.where((df_by_date_combined['Spend TY'] != 0) &  (df_by_date_combined['Spend LY'] != 0),\
		df_by_date_combined['Spend YoY (%)'].apply(formatter_percent), df_by_date_combined['Spend YoY (%)'])


	df_by_date_combined['Sessions_PoP_percent_conditional'] = df_by_date_combined['Sessions PoP (%)'] = np.where((df_by_date_combined['Sessions - TY'] != 0) &  (df_by_date_combined['Sessions - LP'] != 0),\
		((df_by_date_combined['Sessions - TY'] - df_by_date_combined['Sessions - LP'])/df_by_date_combined['Sessions - LP']) * 100, df_by_date_combined['Sessions PoP (%)'])
	# Formatter
	df_by_date_combined['Sessions PoP (%)'] = np.where((df_by_date_combined['Sessions - TY'] != 0) &  (df_by_date_combined['Sessions - LP'] != 0),\
		df_by_date_combined['Sessions PoP (%)'].apply(formatter_percent), df_by_date_combined['Sessions PoP (%)'])

	df_by_date_combined['Sessions_YoY_percent_conditional'] = df_by_date_combined['Sessions YoY (%)'] = np.where((df_by_date_combined['Sessions - TY'] != 0) &  (df_by_date_combined['Sessions - LY'] != 0),\
		((df_by_date_combined['Sessions - TY'] - df_by_date_combined['Sessions - LY'])/df_by_date_combined['Sessions - LY']) * 100, df_by_date_combined['Sessions YoY (%)'])
	# Formatter
	df_by_date_combined['Sessions YoY (%)'] = np.where((df_by_date_combined['Sessions - TY'] != 0) &  (df_by_date_combined['Sessions - LY'] != 0),\
		df_by_date_combined['Sessions YoY (%)'].apply(formatter_percent), df_by_date_combined['Sessions YoY (%)'])


	df_by_date_combined['Bookings_PoP_abs_conditional'] = df_by_date_combined['Bookings PoP (Abs)'] = (df_by_date_combined['Bookings - TY'] - df_by_date_combined['Bookings - LP'])
	# Formatter
	df_by_date_combined['Bookings PoP (Abs)'] = df_by_date_combined['Bookings PoP (Abs)'].apply(formatter_number)

	df_by_date_combined['Bookings_YoY_abs_conditional'] = df_by_date_combined['Bookings YoY (Abs)'] = (df_by_date_combined['Bookings - TY'] - df_by_date_combined['Bookings - LY'])
	# Formatter
	df_by_date_combined['Bookings YoY (Abs)'] = df_by_date_combined['Bookings YoY (Abs)'].apply(formatter_number)

	df_by_date_combined['Bookings_PoP_percent_conditional'] = df_by_date_combined['Bookings PoP (%)'] = np.where((df_by_date_combined['Bookings - TY'] != 0) &  (df_by_date_combined['Bookings - LP'] != 0),\
		(df_by_date_combined['Bookings - TY'] - df_by_date_combined['Bookings - LP'])/df_by_date_combined['Bookings - LP'] * 100, df_by_date_combined['Bookings PoP (%)'])
	# Formatter
	df_by_date_combined['Bookings PoP (%)'] = np.where((df_by_date_combined['Bookings - TY'] != 0) &  (df_by_date_combined['Bookings - LP'] != 0),\
		df_by_date_combined['Bookings PoP (%)'].apply(formatter_percent), df_by_date_combined['Bookings PoP (%)'])

	df_by_date_combined['Bookings_YoY_percent_conditional'] = df_by_date_combined['Bookings YoY (%)'] = np.where((df_by_date_combined['Bookings - TY'] != 0) &  (df_by_date_combined['Bookings - LY'] != 0),\
		(df_by_date_combined['Bookings - TY'] - df_by_date_combined['Bookings - LY'])/df_by_date_combined['Bookings - LY'] * 100, df_by_date_combined['Bookings YoY (%)'])
	# Formatter
	df_by_date_combined['Bookings YoY (%)'] = np.where((df_by_date_combined['Bookings - TY'] != 0) &  (df_by_date_combined['Bookings - LY'] != 0),\
		df_by_date_combined['Bookings YoY (%)'].apply(formatter_percent), df_by_date_combined['Bookings YoY (%)'])


	df_by_date_combined['Revenue_PoP_abs_conditional'] = df_by_date_combined['Revenue PoP (Abs)'] = (df_by_date_combined['Revenue - TY'] - df_by_date_combined['Revenue - LP'])
	# Formatter
	df_by_date_combined['Revenue PoP (Abs)'] = df_by_date_combined['Revenue PoP (Abs)'].apply(formatter_currency)

	df_by_date_combined['Revenue_YoY_abs_conditional'] = df_by_date_combined['Revenue YoY (Abs)'] = (df_by_date_combined['Revenue - TY'] - df_by_date_combined['Revenue - LY'])
	# Formatter
	df_by_date_combined['Revenue YoY (Abs)'] = df_by_date_combined['Revenue YoY (Abs)'].apply(formatter_currency)

	df_by_date_combined['Revenue_PoP_percent_conditional'] = df_by_date_combined['Revenue PoP (%)'] = np.where((df_by_date_combined['Revenue - LP'] != 0) &  (df_by_date_combined['Revenue - LP'] != 0),\
		(df_by_date_combined['Revenue - TY'] - df_by_date_combined['Revenue - LP'])/df_by_date_combined['Revenue - LP'] * 100, df_by_date_combined['Revenue PoP (%)'])
	# Formatter
	df_by_date_combined['Revenue PoP (%)'] = np.where((df_by_date_combined['Revenue - LP'] != 0) &  (df_by_date_combined['Revenue - LP'] != 0),\
		df_by_date_combined['Revenue PoP (%)'].apply(formatter_percent), df_by_date_combined['Revenue PoP (%)'])

	df_by_date_combined['Revenue_YoY_percent_conditional'] = df_by_date_combined['Revenue YoY (%)'] = np.where((df_by_date_combined['Revenue - TY'] != 0) &  (df_by_date_combined['Revenue - LY'] != 0),\
		(df_by_date_combined['Revenue - TY'] - df_by_date_combined['Revenue - LY'])/df_by_date_combined['Revenue - LY'] * 100, df_by_date_combined['Revenue YoY (%)'])
	# Formatter
	df_by_date_combined['Revenue YoY (%)'] = np.where((df_by_date_combined['Revenue - TY'] != 0) &  (df_by_date_combined['Revenue - LY'] != 0),\
		df_by_date_combined['Revenue YoY (%)'].apply(formatter_percent), df_by_date_combined['Revenue YoY (%)'])

	# Format Numbers
	df_by_date_combined['Spend TY'] = df_by_date_combined['Spend TY'].apply(formatter_currency) 
	df_by_date_combined['Spend - LP'] = df_by_date_combined['Spend - LP'].apply(formatter_currency) 
	df_by_date_combined['Spend LY'] = df_by_date_combined['Spend LY'].apply(formatter_currency) 

	df_by_date_combined['Sessions - TY'] = df_by_date_combined['Sessions - TY'].apply(formatter_number)
	df_by_date_combined['Sessions - LP'] = df_by_date_combined['Sessions - LP'].apply(formatter_number)
	df_by_date_combined['Sessions - LY'] = df_by_date_combined['Sessions - LY'].apply(formatter_number)
	df_by_date_combined['Bookings - TY'] = df_by_date_combined['Bookings - TY'].apply(formatter_number)
	df_by_date_combined['Bookings - LP'] = df_by_date_combined['Bookings - LP'].apply(formatter_number)
	df_by_date_combined['Bookings - LY'] = df_by_date_combined['Bookings - LY'].apply(formatter_number)

	df_by_date_combined['Revenue - TY'] = df_by_date_combined['Revenue - TY'].apply(formatter_currency) 
	df_by_date_combined['Revenue - LP'] = df_by_date_combined['Revenue - LP'].apply(formatter_currency) 
	df_by_date_combined['Revenue - LY'] = df_by_date_combined['Revenue - LY'].apply(formatter_currency)
	# Rearrange the columns
	df_by_date_combined_dt = df_by_date_combined[[
		 'Placement type', 
		 'Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)',
		 'Sessions - TY', 'Sessions - LP', 'Sessions PoP (%)', 'Sessions - LY', 'Sessions YoY (%)',
		 'Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)', 
		 'Revenue - TY', 'Revenue - LP', 'Revenue PoP (Abs)', 'Revenue PoP (%)', 'Revenue - LY', 'Revenue YoY (%)', 'Revenue YoY (Abs)', 
		 # 'Spend_PoP_percent_conditional', 
		 ]]

	data_df = df_by_date_combined.to_dict("rows")
	return data_df
```

The flow between the data table element, the callback and the function can be portrayed as:

![](https://miro.medium.com/max/30/1*9_7J0kgJSj-fOj47OwTkQA.png?q=20)

![](https://miro.medium.com/max/2172/1*9_7J0kgJSj-fOj47OwTkQA.png)

Figure 6: Flow for the first data table

## A method to select either a condensed data table or the complete data table.

One of the features that I wanted for the data table was the ability to show a “condensed” version of the table as well as the complete data table. Therefore, I included a radio button in the  `layouts.py`  file to select which version of the table to present:

```py
# Radio Button
html.Div([
  dcc.RadioItems(
    options=[
        {'label': 'Condensed Data Table', 'value': 'Condensed'},
        {'label': 'Complete Data Table', 'value': 'Complete'},
    ], value='Condensed',
    labelStyle={'display': 'inline-block', 'width': '20%', 'margin':'auto', 'marginTop': 15, 'paddingLeft': 15},
    id='radio-button-paid-search'
    )]),
```

The callback for this functionality takes input from the radio button and outputs the columns to render in the data table:

```py

# Callback and update data table columns
@app.callback(Output('datatable-paid-search', 'columns'),
    [Input('radio-button-paid-search', 'value')])
def update_columns(value):
    if value == 'Complete':
    	column_set=[{"name": i, "id": i, 'deletable': True} for i in columns_complete] + [{"name": j, "id": j, 'hidden': 'True'} for j in conditional_columns]
    elif value == 'Condensed':
        column_set=[{"name": i, "id": i, "deletable": True} for i in columns_condensed]
    return column_set
```

This callback is a little bit more complicated since I am adding columns for conditional formatting (which I will go into below). Essentially, just as the callback below is changing the data presented in the data table based upon the dates selected using the callback statement,`Output('datatable-paid-search', 'data'`, this callback is changing the columns presented in the data table based upon the radio button selection using the callback statement,  `Output('datatable-paid-search', 'columns'`.

## Conditionally Color-Code Different Data Table cells

One of the features which the stakeholders wanted for the data table was the ability to have certain numbers or cells in the data table to be highlighted based upon a metric’s value; red for negative numbers for instance. However, conditional formatting of data table cells has three main issues.

-   There is lack of formatting functionality in Dash Data Tables at this time.
-   If a number is formatted prior to inclusion in a Dash Data Table (in pandas for instance), then data table functionality such as sorting and filtering does not work properly.
-   There is a bug in the Dash data table code in which conditional formatting does not work properly.

I ended up formatting the numbers in the data table in pandas despite the above limitations. I discovered that conditional formatting in Dash does not work properly for formatted numbers (numbers with commas, dollar signs, percent signs, etc.). Indeed, I found out that there is a bug with the method described in the  [Conditional Formatting — Highlighting Cells](https://dash.plot.ly/datatable/style)  section of the Dash Data Table User Guide:

```py
dash_table.DataTable(
    data=df.to_dict('rows'),
    columns=[
        {'name': i, 'id': i} for i in df.columns
    ],
    style_data_conditional=[
        {
            'if': {
                'column_id': 'Region',
                'filter': 'Region eq "Montreal"'
            },
            'backgroundColor': '#3D9970',
            'color': 'white',
        },
        {
            'if': {
                'column_id': 'Humidity',
                'filter': 'Humidity eq num(20)'
            },
            'backgroundColor': '#3D9970',
            'color': 'white',
        },
        {
            'if': {
                'column_id': 'Temperature',
                'filter': 'Temperature > num(3.9)'
            },
            'backgroundColor': '#3D9970',
            'color': 'white',
        },
    ]
)
```

The cell for New York City temperature shows up as green even though the value is less than 3.9.* I’ve tested this in other scenarios and it seems like the conditional formatting for numbers only uses the integer part of the condition (“3” but not “3.9”). The filter for Temperature used for conditional formatting somehow truncates the significant digits and only considers the integer part of a number. I posted to the Dash  [community forum](https://community.plot.ly/t/numerical-conditional-formatting-for-datatable-doesnt-work-properly/20289/2)  about this bug, and it has since been fixed in a recent version of Dash.

_*This has since been corrected in the Dash Documentation._

## Conditional Formatting of Cells using Doppelganger Columns

Due to the above limitations with conditional formatting of cells, I came up with an alternative method in which I add “doppelganger” columns to both the pandas data frame and Dash data table. These doppelganger columns had either the value of the original column, or the value of the original column multiplied by 100 (to overcome the bug when the decimal portion of a value is not considered by conditional filtering). Then, the doppelganger columns can be added to the data table but are hidden from view with the following statements:

```py
dt_columns = ['Placement type', 'Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)', \
                        'Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 'Sessions YoY (%)', \
                        'Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)', \
                        'Revenue - TY', 'Revenue - LP', 'Revenue PoP (Abs)', 'Revenue PoP (%)', 'Revenue - LY', 'Revenue YoY (%)', 'Revenue YoY (Abs)',]

conditional_columns = ['Spend_PoP_abs_conditional', 'Spend_PoP_percent_conditional', 'Spend_YoY_percent_conditional',
'Sessions_PoP_percent_conditional', 'Sessions_YoY_percent_conditional', 
'Bookings_PoP_abs_conditional', 'Bookings_YoY_abs_conditional', 'Bookings_PoP_percent_conditional', 'Bookings_YoY_percent_conditional',
'Revenue_PoP_abs_conditional', 'Revenue_YoY_abs_conditional', 'Revenue_PoP_percent_conditional', 'Revenue_YoY_percent_conditional',]

# Below is placed in definition of data table
columns=[{"name": i, "id": i, 'deletable': True} for i in dt_columns] 
                + [{"name": j, "id": j, 'hidden': 'True'} for j in conditional_columns], 
```

Then, the conditional cell formatting can be implemented using the following syntax:

```py
style_cell_conditional=[{'if': {'column_id': 'Revenue YoY (%)', 
                         'filter': 'Revenue_YoY_percent_conditional < num(0)'}, 
                         'color': 'red'}]
```

Essentially, the filter is applied on the “doppelganger” column,  `Revenue_YoY_percent_conditional`  (filtering cells in which the value is less than 0). However, the formatting is applied on the corresponding “real” column,  `Revenue YoY (%)`. One can imagine other usages for this method of conditional formatting; for instance, highlighting outlier values.

The complete statement for the data table is below (with conditional formatting for odd and even rows, as well highlighting cells that are above a certain threshold using the doppelganger method):

```py

html.Div([
    dash_table.DataTable(
        id='datatable-paid-search',
        columns=[{"name": i, "id": i, 'deletable': True} for i in dt_columns] 
        + [{"name": j, "id": j, 'hidden': 'True'} for j in conditional_columns], 
        editable=True,
        n_fixed_columns=2,
        style_table={'maxWidth': '1500px'},
        row_selectable="multi",
        selected_rows=[0],
        style_cell = {"fontFamily": "Arial", "size": 10, 'textAlign': 'left'},
        css=[{'selector': '.dash-cell div.dash-cell-value', 'rule': 'display: inline; white-space: inherit; overflow: inherit; text-overflow: inherit;'}],
        style_cell_conditional=[{'if': {'row_index': 'odd'}, 'backgroundColor': '#D5DBDB'}]  
              + [{'if': {'column_id': c}, 'backgroundColor': '#EAFAF1'} for c in ['Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)',]] 
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#D5F5E3'} for c in ['Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)',]] 
              + [{'if': {'column_id': c}, 'backgroundColor': '#FEF9E7'} for c in ['Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 'Sessions YoY (%)',]] 
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#FCF3CF'} for c in ['Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 'Sessions YoY (%)',]]
              + [{'if': {'column_id': c}, 'backgroundColor': '#EBF5FB'} for c in ['Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)',]]
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#D6EAF8'} for c in ['Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)',]]
              + [{'if': {'column_id': c},'backgroundColor': '#F4ECF7'} for c in ['CVR - TY', 'CVR - LP', 'CVR PoP (Abs)','CVR - LY',  'CVR YoY (Abs)', 'CVR PoP (%)', 'CVR YoY (%)']]
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#E8DAEF' } for c in ['CVR - TY', 'CVR - LP', 'CVR PoP (Abs)','CVR - LY',  'CVR YoY (Abs)', 'CVR PoP (%)', 'CVR YoY (%)']]
              + [{'if': {'column_id': c}, 'backgroundColor': '#FDEDEC' } for c in ['CPA - TY', 'CPA - LP', 'CPA PoP (Abs)', 'CPA - LY', 'CPA YoY (Abs)','CPA PoP (%)', 'CPA YoY (%)' ]]
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#FADBD8' } for c in ['CPA - TY', 'CPA - LP', 'CPA PoP (Abs)', 'CPA - LY', 'CPA YoY (Abs)', 'CPA PoP (%)', 'CPA YoY (%)']]
              + [{'if': {'column_id': c},'backgroundColor': '#F6DDCC'} for c in ['CPS - TY', 'CPS - LP', 'CPS PoP (Abs)', 'CPS - LY',  'CPS YoY (Abs)', 'CPS PoP (%)', 'CPA YoY (%)']]
              + [{'if': {'column_id': c, 'row_index': 'odd'}, 'backgroundColor': '#E59866' } for c in ['CPS - TY', 'CPS - LP', 'CPS PoP (Abs)', 'CPS - LY',  'CPS YoY (Abs)', 'CPS PoP (%)', 'CPA YoY (%)']]
              + [{'if': {'column_id': c}, 'minWidth': '0px', 'maxWidth': '80px', 'whiteSpace': 'normal'} for c in ['Spend TY', 'Spend - LP', 'Spend PoP (Abs)', 'Spend PoP (%)', 'Spend LY', 'Spend YoY (%)', 'Sessions - TY', 'Sessions - LP', 'Sessions - LY', 'Sessions PoP (%)', 
              'Sessions YoY (%)', 'Bookings - TY', 'Bookings - LP', 'Bookings PoP (%)', 'Bookings PoP (Abs)', 'Bookings - LY', 'Bookings YoY (%)', 'Bookings YoY (Abs)', 'Revenue - TY', 'Revenue - LP', 'Revenue PoP (Abs)', 'Revenue PoP (%)', 'Revenue - LY', 'Revenue YoY (%)', 'Revenue YoY (Abs)',]]
              + [{'if': {'column_id': 'Spend PoP (Abs)', 'filter': 'Spend_PoP_abs_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Spend PoP (%)', 'filter': 'Spend_PoP_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Spend YoY (%)', 'filter': 'Spend_YoY_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Sessions PoP (%)', 'filter': 'Sessions_PoP_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Sessions YoY (%)', 'filter': 'Sessions_YoY_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Bookings PoP (Abs)', 'filter': 'Bookings_PoP_abs_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Bookings YoY (Abs)', 'filter': 'Bookings_YoY_abs_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Bookings PoP (%)', 'filter': 'Bookings_PoP_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Bookings YoY (%)', 'filter': 'Bookings_YoY_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Revenue PoP (Abs)', 'filter': 'Revenue_PoP_abs_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Revenue YoY (Abs)', 'filter': 'Revenue_YoY_abs_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Revenue PoP (%)', 'filter': 'Revenue_PoP_percent_conditional < num(0)'}, 'color': 'red'}]
              + [{'if': {'column_id': 'Revenue YoY (%)', 'filter': 'Revenue_YoY_percent_conditional < num(0)'}, 'color': 'red'}],
              style_header={'backgroundColor': 'black','color': 'white'},
        )
```

I describe the method to update the graphs using the selected rows in the data table below.

----------

# 9. Building the Download Data link

![](https://miro.medium.com/max/30/1*PaIwCRRB855x2xhTHpyb7Q.png?q=20)

![](https://miro.medium.com/max/444/1*PaIwCRRB855x2xhTHpyb7Q.png)

Figure 7: Download data link

One of the features I wanted for the dashboard was the ability to download the data that was presented in the data tables. Specifically, I wanted the downloaded data to be updated according to the dates selected (and presented in the data tables). In addition, since the dates are not displayed, it was necessary to add the dates to the downloaded file. Moreover, even though the data is formatted in the data tables (with  `$`,  `%`  , and thousand comma separators, I wanted the downloaded data to be free of formatting.

There were two critical Plotly community threads which helped me to build this functionality at  [Allow users to dowload [sic] an Excel in a click](https://community.plot.ly/t/allow-users-to-dowload-an-excel-in-a-click/9410)  and  [Allowing users to download CSV on click](https://community.plot.ly/t/allowing-users-to-download-csv-on-click/5550).

The download data functionality was implemented using the following:

-   There is simply a placeholder for the download button in the  `layouts.py`  file.

```py
# Download Button
html.Div([
  html.A(html.Button('Download Data', id='download-button'), id='download-link-paid-search-1')
  ]),
```

-   You will need the following modules for the download link to work properly:

```py
import io
import xlsxwriter
import flask
from flask import send_file
```

-   The callback for the excel download is placed in the  `callbacks.py`  file. The callback is taking the  `start_date`  and the  `end_date`  from the date picker element and outputting a file reference to the download link.
-   The  `update_link`  function is updating the URL link to serve, based upon the start and end dates.
-   The function  `download_excel_1`  takes the URL value and splits it up back into  `start_date`  and  `end_date`  so that I can name the  `filename`  based upon the start and end dates, as well as the current date.

```py
# Callback for excel download
@app.callback(
    Output('download-link-paid-search-1', 'href'),
    [Input('my-date-picker-range-paid-search', 'start_date'),
	 Input('my-date-picker-range-paid-search', 'end_date')])   
def update_link(start_date, end_date):
	return '/cc-travel-report/paid-search/urlToDownload?value={}/{}'.format(dt.strptime(start_date,'%Y-%m-%d').strftime('%Y-%m-%d'),dt.strptime(end_date,'%Y-%m-%d').strftime('%Y-%m-%d'))
@app.server.route("/cc-travel-report/paid-search/urlToDownload") 
def download_excel_1():
    value = flask.request.args.get('value')
    #here is where I split the value
    value = value.split('/')
    start_date = value[0]
    end_date = value[1]

    filename = datestamp + '_paid_search_' + start_date + '_to_' + end_date + '.xlsx'
	# Dummy Dataframe
    # d = {'col1': [1, 2], 'col2': [3, 4]}
    # df = pd.DataFrame(data=d)

    buf = io.BytesIO()
    excel_writer = pd.ExcelWriter(buf, engine="xlsxwriter")
    download_1 = update_first_download(start_date, end_date, 'Paid Search', 'Placement type')
    download_1.to_excel(excel_writer, sheet_name="sheet1", index=False)
    # df.to_excel(excel_writer, sheet_name="sheet1", index=False)
    excel_writer.save()
    excel_data = buf.getvalue()
    buf.seek(0)

    return send_file(
        buf,
        mimetype = 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet', 
        attachment_filename=filename,
        as_attachment=True,
        cache_timeout=0
    )
```

-   The function  `download_excel_1`  also calls another function,  `update_first_download`, which is very similar to the  `update_first_download`  function presented above, except that the data is not formatted.
-   The downloaded Excel file is named according to the product name and the start and end dates selected, as well as the current date. Columns for the start and end dates and other appropriate dates are added to the downloaded data file.

![](https://miro.medium.com/max/30/1*4Pqj0pzEyUSkdUuMPa6NFA.png?q=20)

![](https://miro.medium.com/max/2578/1*4Pqj0pzEyUSkdUuMPa6NFA.png)

Figure 8: Snap shot of the downloaded data.

----------

# 10. Building the Second Data Table

![](https://miro.medium.com/max/30/1*bUz81xK2IGo9abzsIzz3gw.png?q=20)

![](https://miro.medium.com/max/2214/1*bUz81xK2IGo9abzsIzz3gw.png)

Figure 9: Data Table with Calculated Metrics

The second data table featured metrics such as cost-per-session, conversion rate and and cost-per-session which are calculated “on-the-fly,” depending upon the dates selected in the date range selected.

The second data table is created is a similar manner to the first data table so the details are left out of this tutorial, but the complete files are on  [Github](https://github.com/davidcomfort/dash_sample_dashboard).

----------

# 11. Updating Graphs by Selecting Rows in a Dash Data table

![](https://miro.medium.com/max/22/1*XrmB2nwuHPxtpCICXWDcVA.png?q=20)

![](https://miro.medium.com/max/1710/1*XrmB2nwuHPxtpCICXWDcVA.png)

Figure 10: Digital Marketing Metric Graphs

The graphs below the data tables display metrics aggregated by week, and include the current year’s data, last year’s data, as well as the percentage changes between the two.

![](https://miro.medium.com/max/30/1*PXT7I6DAcaaVG0s4g_6vnw.png?q=20)

![](https://miro.medium.com/max/2122/1*PXT7I6DAcaaVG0s4g_6vnw.png)

Figure 11: Diagram of callback and function to update graphs

The steps to update the graphs are:

1.  Set placeholder in the  `layouts.py`  file.
2.  Create callback for each set of graphs, for each page of the Dashboard in the  `callbacks.py`  file.
3.  Build a function which filters the complete list of products by the list of products selected in the Dash data table, and subsequently creates a pandas data frame based upon this selection.
4.  The filtered data frame is then passed to another function,  `update_graph`  that (a) calculates metrics such as cost-per-session, conversion rate and cost-per session, and (b) produces the output for the graphs.

These steps are detailed below.  _Step 4 is detailed in Section 12, “Updating the Graphs and Calculating metrics on the fly.”_

## Step 1

In the  `layouts.py`  file, there is simply a placeholder for the graphs:

```py
html.Div([
    dcc.Graph(id='paid-search'),
    ], className=" twelve columns"
    )
```

## Step 2

There is a callback for each set of graphs on each page in the  `callbacks.py`  file:

```py
# Callback for the Graphs
@app.callback(
   Output('paid-search', 'figure'),
   [Input('datatable-paid-search', "selected_rows"),
   Input('my-date-picker-range-paid-search', 'end_date')])
```

The callback takes input from the first data table, as well as input from the date picker, and outputs to the  `dcc.Graph`  element with the  `id`,  `paid-search`.

## Step 3

One of the challenges I had had was to figure out a way of updating the graphs depending upon the products selected in the data table.

In the code for the first data table, it was necessary to set the parameters for  `row_selectable`  to  `multi`  and  `selected_rows=[0]`. The former parameter enables checkboxes next to each row in the data table, whereas the latter parameter ensures that the selected rows has an initial value. The parameter,  `n_fixed_columns`  freezes the first two rows in the data table so that they are visible when a user enables the complete data frame, (thus exposing all of the available columns).

Here is a simplified code block for the first data table (which is in the  `layouts.py`  file):

```py
dash_table.DataTable(
    id='datatable-paid-search',
    columns=[{"name": i, "id": i, 'deletable': True} for i in dt_columns],
    n_fixed_columns=2,
    row_selectable="multi",
    selected_rows=[0],
    )
```

Hence, the callback for the graphs acquire the  `selected_rows`. In the function to update the graphs,  `update_paid_search`, a list of products is built by filtering the original data frame by the dashboard page category (Paid Search in this case) and getting a complete list of unique placement types. Then, a  `for`  loop filters this list by the list of products selected in the data table. Subsequently, a filtered data frame,  `filtered_df`  is created by filtering the original data frame by the list of selected products and performing a pandas  `groupby`  and summing the spend, sessions, bookings and revenue columns. The callback and function,  `update_paid_search`, for the graphs is presented below:

```py
# Callback for the Graphs
@app.callback(
   Output('paid-search', 'figure'),
   [Input('datatable-paid-search', "selected_rows"),
   Input('my-date-picker-range-paid-search', 'end_date')])
def update_paid_search(selected_rows, end_date):
	travel_product = []
	travel_product_list = df[(df['Category'] == 'Paid Search')]['Placement type'].unique().tolist()
	for i in selected_rows:
		travel_product.append(travel_product_list[i])
		# Filter by specific product
	filtered_df = df[(df['Placement type'].isin(travel_product))].groupby(['Year', 'Week']).sum()[['Spend TY', 'Spend LY', 'Sessions - TY', 'Sessions - LY', 'Bookings - TY', 'Bookings - LY', 'Revenue - TY', 'Revenue - LY']].reset_index()
	fig = update_graph(filtered_df, end_date)
	return fig
```

----------

# 12. Updating the Graphs and Calculating metrics on the fly

The graphs for each metric are aggregated by week and by the products that are selected in the data table (as detailed above).

The features I wanted for the graphs and for the update function included:

-   Since the graphs can depict metrics on more than one product at a time, the update function needs to calculate the metrics on-the-fly.
-   The graph for each metric should include the value for this year, the value for last year, as well as the year-to-year percentage difference.These should be overlaid on the same graph, with the values being line graphs, and the year-to-year change being bar graphs.
-   I wanted the zoom function to work across all of the graphs simultaneously, such that zooming in on one graph, zooms in the other graphs at the same zoom level.

The complete  `update_graph`  function (which resides in the  `functions.py`  file is below:

```py
def update_graph(filtered_df, end_date):
    if end_date is not None:
        end_date = dt.strptime(end_date, '%Y-%m-%d')
        end_date_string = end_date.strftime('%Y-%m-%d')
    if end_date_string <= '2018-12-29':
        current_year = 2018
    else:
        current_year = 2019

    # Calulate YoY Differences
    filtered_df['Spend YoY (%)'] = ((filtered_df['Spend TY'] - filtered_df['Spend LY'])/filtered_df['Spend LY']) * 100
    filtered_df['Sessions YoY (%)'] = ((filtered_df['Sessions - TY'] - filtered_df['Sessions - LY'])/filtered_df['Sessions - LY']) * 100
    filtered_df['Bookings - % - PY'] = ((filtered_df['Bookings - TY'] - filtered_df['Bookings - LY'])/filtered_df['Bookings - LY']) * 100
    filtered_df['Revenue - % - PY'] = ((filtered_df['Revenue - TY'] - filtered_df['Revenue - LY'])/filtered_df['Revenue - LY']) * 100

    # Calculate CPS, CR, CPA
    filtered_df['CPS - TY'] = np.nan
    filtered_df['CPS - LY'] = np.nan
    filtered_df['% YoY_CPS'] = np.nan

    filtered_df['CVR - TY'] = np.nan
    filtered_df['CVR - LY'] = np.nan
    filtered_df['CVR YoY (Abs)'] = np.nan

    filtered_df['CPA - TY'] = np.nan
    filtered_df['CPA - LY'] = np.nan
    filtered_df['% YoY_CPA'] = np.nan

    filtered_df['CPS - TY'] = np.where((filtered_df['Spend TY'] != 0) &  (filtered_df['Sessions - TY'] != 0), (filtered_df['Spend TY']/filtered_df['Sessions - TY']), filtered_df['CPS - TY'])                      
    filtered_df['CPS - LY'] = np.where((filtered_df['Spend LY'] != 0) &  (filtered_df['Sessions - LY'] != 0), (filtered_df['Spend LY']/filtered_df['Sessions - LY']), filtered_df['CPS - LY'])
    filtered_df['% YoY_CPS'] =  np.where((filtered_df['CPS - TY'] != 0) &  (filtered_df['CPS - LY'] != 0), ((filtered_df['CPS - TY'] - filtered_df['CPS - LY'])/filtered_df['CPS - LY']), filtered_df['% YoY_CPS'])

    filtered_df['CVR - TY'] = np.where(((filtered_df['Bookings - TY'] != 0) & (filtered_df['Sessions - TY'] != 0)), (filtered_df['Bookings - TY']/filtered_df['Sessions - TY'] * 100), filtered_df['CVR - TY'])
    filtered_df['CVR - LY'] = np.where(((filtered_df['Bookings - LY'] != 0) & (filtered_df['Sessions - LY'] != 0)), (filtered_df['Bookings - LY']/filtered_df['Sessions - LY'] * 100), filtered_df['CVR - LY'])
    filtered_df['CVR YoY (Abs)'] =  np.where((filtered_df['CVR - TY'].notnull() & filtered_df['CVR - LY'].notnull()), ((filtered_df['CVR - TY'] - filtered_df['CVR - LY'])), filtered_df['CVR YoY (Abs)'])

    filtered_df['CPA - TY'] = np.where((filtered_df['Spend TY'] != 0) & (filtered_df['Bookings - TY'] != 0), (filtered_df['Spend TY']/filtered_df['Bookings - TY']), filtered_df['CPA - TY'])                     
    filtered_df['CPA - LY'] = np.where((filtered_df['Spend LY'] != 0) & (filtered_df['Bookings - LY'] != 0), (filtered_df['Spend LY']/filtered_df['Bookings - LY']), filtered_df['CPA - LY'])
    filtered_df['% YoY_CPA'] =  np.where((filtered_df['CPA - TY'] != 0) & (filtered_df['CPA - LY'] != 0), ((filtered_df['CPA - TY'] - filtered_df['CPA - LY'])/filtered_df['CPA - LY']) * 100, filtered_df['% YoY_CPA'])


    # Sessions Graphs 
    sessions_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Sessions - TY'],
      text='Sessions - TY'
    )
    sessions_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['Sessions - TY'],
      text='Sessions - LY'
    )
    sessions_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Sessions YoY (%)'],
      text='Sessions YoY (%)', opacity=0.6
    )
    # Spend Graphs
    spend_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Spend TY'],
      text='Spend TY'
    )
    spend_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['Spend TY'],
      text='Spend LY'
    )
    spend_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Spend YoY (%)'],
      text='Spend YoY (%)', opacity=0.6
    )
    # Bookings Graphs
    bookings_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Bookings - TY'],
      text='Bookings - TY'
    )
    bookings_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['Bookings - TY'],
      text='Bookings - LY'
    )
    bookings_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['Bookings - % - PY'],
      text='Bookings - % - PY', opacity=0.6
    )
    cpa_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['CPA - TY'],
      text='CPA - TY'
    )
    cpa_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['CPA - TY'],
      text='CPA - LY'
    )
    cpa_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['% YoY_CPA'],
      text='% CPA - YoY', opacity=0.6
    )
    cps_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['CPS - TY'],
      text='CPS - TY'
    )
    cps_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['CPS - TY'],
      text='CPS - LY'
    )
    cps_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['% YoY_CPS'],
      text='% CPS - YoY', opacity=0.6
    )
    cr_ty = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['CVR - TY'],
      text='CVR - TY'
    )
    cr_ly = go.Scatter(
      x=filtered_df[(filtered_df['Year'] == current_year-1)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year-1)]['CVR - TY'],
      text='CVR - LY'
    )
    cr_yoy = go.Bar(
      x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
      y=filtered_df[(filtered_df['Year'] == current_year)]['CVR YoY (Abs)'],
      text='CVR YoY (Abs)', opacity=0.6
    )

    fig = tools.make_subplots(
      rows=6, 
      cols=1, 
      shared_xaxes=True,
      subplot_titles=(								# Be sure to have same number of titles as number of graphs
        'Sessions', 
        'Spend',
        'Bookings', 
        'Cost per Acquisition',
        'CPS',
        'Conversion Rate'
        ))

    fig.append_trace(sessions_ty, 1, 1)		# 0
    fig.append_trace(sessions_ly, 1, 1)		# 1
    fig.append_trace(sessions_yoy, 1, 1)	# 2
    fig.append_trace(spend_ty, 2, 1)		# 3
    fig.append_trace(spend_ly, 2, 1)		# 4
    fig.append_trace(spend_yoy, 2, 1)		# 5
    fig.append_trace(bookings_ty, 3, 1)		# 6
    fig.append_trace(bookings_ly, 3, 1)		# 7
    fig.append_trace(bookings_yoy, 3, 1)	# 8
    fig.append_trace(cpa_ty, 4, 1)			# 9
    fig.append_trace(cpa_ly, 4, 1)			# 10
    fig.append_trace(cpa_yoy, 4, 1)			# 11
    fig.append_trace(cps_ty, 5, 1)			# 12
    fig.append_trace(cps_ly, 5, 1)			# 13
    fig.append_trace(cps_yoy, 5, 1)			# 14
    fig.append_trace(cr_ty, 6, 1)			# 15
    fig.append_trace(cr_ly, 6, 1)			# 16
    fig.append_trace(cr_yoy, 6, 1)			# 17

    # integer index below is the index of the trace
    # yaxis indices below need to start from the number of total graphs + 1 since they are on right-side
    # overlaing and anchor axes correspond to the graph number

    fig['data'][2].update(yaxis='y7')
    fig['layout']['yaxis7'] = dict(overlaying='y1', anchor='x1', side='right', showgrid=False, title='% Change YoY')

    fig['data'][5].update(yaxis='y8')
    fig['layout']['yaxis8'] = dict(overlaying='y2', anchor='x2', side='right', showgrid=False, title='% Change YoY')

    fig['data'][8].update(yaxis='y9')
    fig['layout']['yaxis9'] = dict(overlaying='y3', anchor='x3', side='right', showgrid=False, title='% Change YoY')

    fig['data'][11].update(yaxis='y10')
    fig['layout']['yaxis10'] = dict(overlaying='y4', anchor='x4', side='right', showgrid=False, title='% Change YoY')

    fig['data'][14].update(yaxis='y11')
    fig['layout']['yaxis11'] = dict(overlaying='y5', anchor='x5', side='right', showgrid=False, title='% Change YoY')

    fig['data'][17].update(yaxis='y12')
    fig['layout']['yaxis12'] = dict(overlaying='y6', anchor='x6', side='right', showgrid=False, title='% Change YoY')

    fig['layout']['xaxis'].update(title='Week of the Year' + ' - ' + str(current_year))
    for i in fig['layout']['annotations']:
      i['font'] = dict(size=12)
    fig['layout'].update(
      height= 1500,
      # width=750, 
      showlegend=False, 
      xaxis=dict(
        dtick=5,
        ticklen=8,
        tickwidth=2,
        tickcolor='#000',
        showgrid=True,
        zeroline=True,
        gridwidth=2
    ),
      )
    updated_fig = fig
    return updated_fig
```

In order to “group” the graphs together, I utilized the subplot capability of Plotly detailed at  [https://plot.ly/python/subplots/](https://plot.ly/python/subplots/). The  `update_graph`  function has the following main elements:

-   On-the-fly calculation of the metrics.
-   Each graph “trace” is defined using the  `graph_objs`  method in the Plotly library (remember to import this method via`import plotly.graph_objs as go`). Specifically, each graph is defined with the  `go.Scatter`  method:

```py
sessions_ty = go.Scatter(
  x=filtered_df[(filtered_df['Year'] == current_year)]['Week'],
  y=filtered_df[(filtered_df['Year'] == current_year)]['Sessions - TY'],
  text='Sessions - TY'
)
```

-   The main graph figure and its parameters are defined when we call  `tools.make_subplots`. During app development, I found that potential sources of error are not remembering to change the number of rows when you add additional traces (  `rows=6`) , as well as ensuring that you have the same number of titles as the number of graphs. Both of these might cause the app to fail.

```py
fig = tools.make_subplots(
  rows=6, 
  cols=1, 
  shared_xaxes=True,
  subplot_titles=(    # Be sure to have same number of titles as number of graphs
    'Sessions', 
    'Spend',
    'Bookings', 
    'Cost per Acquisition',
    'CPS',
    'Conversion Rate'
    ))
```

-   The different subplot “traces” are appended to the main graph figure with the statements such as  `fig.append_trace(sessions_ty, 1, 1)`, where  `sessions_ty`  is the trace name defined above; the first number,  `1`  is the graph number and the last number is the column number (which is  `1`  in every case since we only have one column). I have included commented-out numbers for each trace in order to assist me in the next step.

```py
fig.append_trace(sessions_ty, 1, 1)		# 0
fig.append_trace(sessions_ly, 1, 1)		# 1
fig.append_trace(sessions_yoy, 1, 1)	# 2
fig.append_trace(spend_ty, 2, 1)		  # 3
fig.append_trace(spend_ly, 2, 1)		  # 4
fig.append_trace(spend_yoy, 2, 1)		  # 5
fig.append_trace(bookings_ty, 3, 1)		# 6
fig.append_trace(bookings_ly, 3, 1)		# 7
fig.append_trace(bookings_yoy, 3, 1)	# 8
fig.append_trace(cpa_ty, 4, 1)			  # 9
fig.append_trace(cpa_ly, 4, 1)			  # 10
fig.append_trace(cpa_yoy, 4, 1)			  # 11
fig.append_trace(cps_ty, 5, 1)			  # 12
fig.append_trace(cps_ly, 5, 1)			  # 13
fig.append_trace(cps_yoy, 5, 1)			  # 14
fig.append_trace(cr_ty, 6, 1)			    # 15
fig.append_trace(cr_ly, 6, 1)			    # 16
fig.append_trace(cr_yoy, 6, 1)			  # 17
```

In order to overlay the year-to-year changes, I had to have several update statements, as well as adding new y-axes for each overlaid graph (the year-to-year change graphs). The syntax required for these overlaid graphs was a little tricky.

```py
# integer index above is the index of the trace
# yaxis indices below need to start from the number of total graphs + 1 since they are on right-side
# overlaying and anchor axes correspond to the graph number

fig['data'][2].update(yaxis='y7')
fig['layout']['yaxis7'] = dict(overlaying='y1', anchor='x1', side='right', showgrid=False, title='% Change YoY')

fig['data'][5].update(yaxis='y8')
fig['layout']['yaxis8'] = dict(overlaying='y2', anchor='x2', side='right', showgrid=False, title='% Change YoY')

fig['data'][8].update(yaxis='y9')
fig['layout']['yaxis9'] = dict(overlaying='y3', anchor='x3', side='right', showgrid=False, title='% Change YoY')

fig['data'][11].update(yaxis='y10')
fig['layout']['yaxis10'] = dict(overlaying='y4', anchor='x4', side='right', showgrid=False, title='% Change YoY')

fig['data'][14].update(yaxis='y11')
fig['layout']['yaxis11'] = dict(overlaying='y5', anchor='x5', side='right', showgrid=False, title='% Change YoY')

fig['data'][17].update(yaxis='y12')
fig['layout']['yaxis12'] = dict(overlaying='y6', anchor='x6', side='right', showgrid=False, title='% Change YoY')
```

-   For instance, in the first update statement, the index number  `2`  in the statement  `fig['data'][2]`  refers to the third trace,  `sessions_yoy`  (since Python is zero-indexed).

The following figure hopefully assists in visualizing the indexing of the various elements of the combined graph.

![](https://miro.medium.com/max/19/1*ZBUumyprilJgMy0HB9OmGg.png?q=20)

![](https://miro.medium.com/max/1282/1*ZBUumyprilJgMy0HB9OmGg.png)

Figure 12: Schematic of the Different Axis Indexes

-   The y-axis name,  `y7`, in the statement  `yaxis='y7'`  needs to be  `7`  since there are already 6 y-axes (one for each metric: sessions, spend, bookings, cpa, cps, and cr. For each metric, this year’s and last year’s data shares the same left y-axis). Hence, we need start numbering the right-side y axes at  `7`.
-   We need to assign the parameter for each of the additional y-axes using the  `fig['layout']['yaxis']`  statements. Specifically, the first right-side axis for the year-to-year changes in sessions overlaps with the other session traces in the first graph. Hence, we need to assign the parameters accordingly:  `overlaying='y1', anchor='x1'`  and, of course, we need to assign it to the right side by setting  `side='right'`. In addition, I update the title of the set of the graphs with the following:

```py
fig['layout']['xaxis'].update(title='Week of the Year'  +  ' - '  +  str(current_year))
```

Finally, I need to update the overall figure layout with the following statement. I should note that there are several parameters below which are commented out since I am still experimenting with different parameters.

```py
fig['layout'].update(
  height= 1500,
  # width=750, 
  showlegend=False, 
  xaxis=dict(
    # tickmode='linear',
    # ticks='outside',
    # tick0=1,
    dtick=5,
    ticklen=8,
    tickwidth=2,
    tickcolor='#000',
    showgrid=True,
    zeroline=True,
    # showline=True,
    # mirror='ticks',
    # gridcolor='#bdbdbd',
    gridwidth=2
)
```

----------

# 13. Plotly Graph Tools

I should note that there are several helpful tools available in Dash to manipulate the graphs. If you hover over the top right-side of the graph figure, you can view these tools.

![](https://miro.medium.com/max/30/1*6iox1sjUoB9CcADal-3WAA.png?q=20)

![](https://miro.medium.com/max/1080/1*6iox1sjUoB9CcADal-3WAA.png)

Figure 13: Plotly Graph Tools

With these tools you can:

-   Drag to zoom in and double-click to return to the original graph.
-   Drag the corners of a graph to zoom along one axis.
-   Double-click to autoscale a single axis.
-   Change the hover mode to compare data or investigate a single data point.

Certainly, one of the nicest tools is the ability to download a pic of the graph:

![](https://miro.medium.com/max/14/1*76Ni1D-TvMa7Q2C9eH92FQ.png?q=20)

![](https://miro.medium.com/max/700/1*76Ni1D-TvMa7Q2C9eH92FQ.png)

Figure 14: Downloaded image of the graphs

----------

# 14. Deploying the Dashboard

I essentially followed the  [Deploying Dash Apps](https://dash.plot.ly/deployment)  guide in the  [Dash User Guide](https://dash.plot.ly/), with a few changes. Specifically, I deployed the Dashboard on  [Heroku](https://devcenter.heroku.com/)  using the following steps:

-   **Step 1**: I had already created a folder for the my dashboard code in a previous step.

```py
$ mkdir dash_app_example
$ cd dash_app_example
```

-   **Step 2**: Initialize the folder with  `git`  . Rather than use  `venv`, I had previously set up a  [conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)  for Dash.

```py
git init        # initializes an empty git repo
conda create --n dash
source activate dash
```

And I had either installed the app’s dependencies using either  `conda`  or  `pip`:

```py
pip install dash
pip install dash-renderer
pip install dash-core-components
pip install dash-html-components
pip install plotly
pip install pandas
pip install numpy
pip install xlsxwriter
pip install flask
pip install gunicorn
```

You will also need a new dependency,  `gunicorn`, for deploying the app (line 10 in the above code segment).

-   **Step 3**: Initialize folder with an app (  `app.py`), a  `.gitignore`  file, a  `requirements.txt`  file, and a  `Procfile`  file for deployment. We only need a minimal  `app.py`  since we are defining our app using multiple files. You need to create the following files in your project folder.

`app.py`

```py
import dash
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']
app = dash.Dash(__name__, external_stylesheets=external_stylesheets, url_base_pathname='/cc-travel-report/paid-search/')
server = app.server
app.config.suppress_callback_exceptions = True
import dash_auth
# Keep this out of source code repository - save in a file or a database
VALID_USERNAME_PASSWORD_PAIRS = [
    ['[username]', '[password']
]
auth = dash_auth.BasicAuth(
    app,
    VALID_USERNAME_PASSWORD_PAIRS
)
```

`.gitignore`

```py
*.pyc
.DS_Store
```

And a`Procfile`  file:

```py
web: gunicorn index:server
```

You also need to generate a  `requirements.txt`  file. You can do this with:

```py
pip freeze > requirements.txt
```

-   **Step 4**: Initialize Heroku, add files to Git, and Deploy. Prior to initializing Heroku, you need to install the Heroku Command Line Interface (CLI) either with their installer available at  [https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)  or, on a Mac, using homebrew:  `brew tap heroku/brew && brew install heroku`.

```py
$ heroku create my-dash-app # change my-dash-app to a unique name
$ git add . # add all files to git
$ git commit -m 'Initial app boilerplate'
$ git push heroku master # deploy code to heroku
$ heroku ps:scale web=1  # run the app with a 1 heroku "dyno"
```

You should be able to view your app at  `https://my-dash-app.herokuapp.com`  (changing  `my-dash-app`  to the name of your app).

-   **Step 5**: Update the code and redeploy. When you modify any element of your app, you will need to add the changes to git and push those changes to Heroku. Also, whenever I change the underlying CSV data file, you need to push the new data set to Heroku.

```py
git status # view the changes
git add .  # add all the changes
git commit -m 'a description of the changes'
git push heroku master
```

I should note that if you have issues deploying to Heroku, try deploying a simply app first and test whether you are doing each step correctly. For instance, I found that I needed to add the following to the  `index.py`  file in order for the Heroku deployment to work:  `from app import server`.

## Resolving an Issue with Custom.css File and Authentication

In addition, I found that when I added authentication to my app, the app could no longer access my  `custom.css`  file, so I needed to create a css file on  [codepen.io](https://codepen.io/)  and include it in the list of external css files (I am assuming that this is a bug in Dash).

## Dash Deployment Server

Plotly also offers a  [Dash Deployment Server](https://plot.ly/dash/pricing/)…

> for easy app deployment in commercial IT environments, get started with support plans and workshops for mission critical projects, or contract our world-class engineering team for custom feature development or proof of concept app development.

I should note that I have no affiliation with Plotly.

----------

# 15. Wrapping up

From start to finish, the project took about two and half weeks. I had not previously used Dash and had limited experience using Plotly. Some of the methods which I employed to build the dashboard included:

-   Building minimal parts of the dashboard first. Basically, I do not try to tackle everything at once. I built element at a time, and often by itself, before adding it to the entire dashboard.
-   To ensure that I got my python syntax correct, I used a Jupyter notebook with the original data frame and applied each change in a piecewise fashion.
-   I would make small incremental changes to the app and then test. Rinse and repeat.
-   I developed one section first and got it working and to my liking. Then I would copy and paste this section to the other sections and make appropriate changes.
-   I saved deployment for the last step. I tested everything locally.

Some things on my wish list to update the Dashboard include:

-   Add weeks to each graph axis, most likely using annotations.
-   Have the graph x-axis cross over years, rather than just depict either 2018 or 2019.
-   Add a “print PDF” button for the report. I tried to implement one but haven’t been able to get it working yet.
-   Add a footer with metadata (data sources, date data was pulled, where it was pulled from, etc.)

Thanks for reading this far. I know it is a little overwhelming, but I essentially broke things down into manageable pieces.

----------

# 16. Resources for Dash

Here are some resources to help you further with Dash:

-   [Dash User Guide](https://dash.plot.ly/)
-   [Udemy Course](https://www.udemy.com/interactive-python-dashboards-with-plotly-and-dash/)  (I have not taken this online course so I cannot comment on it though.
-   [Dash Community Forum](https://community.plot.ly/c/dash)
-   [Awesome Dash Resource Guide on Github](https://github.com/ucg8j/awesome-dash)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxMjgwMjUxNSwtMTQzOTQ5ODcwN119
-->