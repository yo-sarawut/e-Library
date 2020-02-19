
Static Interactive Widgets for IPython Notebooks
====

> Thu 05 December 2013

_Note: with the release of  [ipywidgets v0.6](https://github.com/ipython/ipywidgets)  in early 2017, static widgets are now supported by the Jupyter project!_

The inspiration of my previous  [kernel density estimation post](http://jakevdp.github.io/blog/2013/12/01/kernel-density-estimation/)  was a blog post by  [Michael Lerner](http://www.mglerner.com/blog/?p=28), who used my  [JSAnimation](http://jakevdp.github.io/blog/2013/05/19/a-javascript-viewer-for-matplotlib-animations/)  tools to do a nice interactive demo of the relationship between kernel density estimation and histograms.

This was on the heels of  [Brian Granger](https://twitter.com/ellisonbg)'s excellent  [PyData NYC Keynote](http://vimeo.com/79832657)  where he live-demoed the brand new IPython interactive tools. This new functionality is very cool. Wes McKinney  [remarked](https://twitter.com/wesmckinn/status/399560987415965696)  that day on Twitter that "IPython's interact machinery is going to be a huge deal". I completely agree: the ability to quickly generate interactive widgets to explore your data is going to change the way a lot of people do their daily scientific computing work.

But there's one issue with the new widget framework as it currently stands: unless you're connected to an IPython kernel (i.e. actually running IPython to view your notebook), the widgets are useless. Don't get me wrong: they're incredibly cool when you're actually interacting with data. But the bread-and-butter of this blog and many others is static notebook views: for this purpose, widgets with callbacks to the Python kernel aren't so helpful.

This is where  `ipywidgets`  comes in.

## My Afternoon Hack: IPy-Widgets[](https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/#My-Afternoon-Hack:-IPy-Widgets)

I've been thinking about this issue for the past few weeks, but this morning as I was biking to work through Seattle's current cold-snap, the idea came to me. Interactive widgets can be done, and done rather easily. I got to work, and after doing a few things I couldn't put off, decided to forego my real research for the day and instead focus on the betterment of humanity (or at least the growing portion of humanity who use the IPython notebook for their work). For anyone who follows me  [on Twitter](https://twitter.com/jakevdp), you might say I  [chose option B](https://twitter.com/jakevdp/status/408678764705378304). The result is  `ipywidgets`: a rough attempt at what, with some effort, might become a very useful library. You can view the current progress on my  [GitHub](http://github.com/jakevdp/ipywidgets)  page. To run the code in this notebook, clone that repository and type  `python setup.py install`. The package is pure python, very lightweight, and should install painlessly on most systems.

The basic idea of creating these widgets is this: you set up a function that does something interesting, you specify the range of parameter choices, and call a function which pre-generates the results and displays a javascript slider which allows you to interact with these results. Here's a quick example of how it works:

First we set up a function which takes some arguments and plots something:
```py
In [1]:

%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

def plot(amplitude, color):
    fig, ax = plt.subplots(figsize=(4, 3),
                           subplot_kw={'axisbg':'#EEEEEE',
                                       'axisbelow':True})
    ax.grid(color='w', linewidth=2, linestyle='solid')
    x = np.linspace(0, 10, 1000)
    ax.plot(x, amplitude * np.sin(x), color=color,
            lw=5, alpha=0.4)
    ax.set_xlim(0, 10)
    ax.set_ylim(-1.1, 1.1)
    return fig
```

Next, you import some tools from  `ipywidgets`, and interact with your plot:
```py
In [2]:

from ipywidgets import StaticInteract, RangeWidget, RadioWidget

StaticInteract(plot,
               amplitude=RangeWidget(0.1, 1.0, 0.1),
               color=RadioWidget(['blue', 'green', 'red']))
```

Out[2]:

![](data:image/png;base64,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%0ANIhIyf8DzqfcRx15MIsAAAAASUVORK5CYII=)

blue:  green:  red:  

That's all there is to it!

## How this all works[](https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/#How-this-all-works)

Because this is a static view, all the output must be pre-generated and saved in the notebook. The way this works is to save the generated frames within divs that are hidden and shown whenever the widget is changed. Here's a rough sample that gives the idea of what's going on with the HTML and Javascript in the background:

First we define a javascript function which takes the values from HTML5  `input`  blocks, and shows and hides items based on those inputs.
```py
In [3]:

JS_FUNCTION = """
<script type="text/javascript">
 function interactUpdate(div){
 var outputs = div.getElementsByTagName("div");
 var controls = div.getElementsByTagName("input");

 var value = "";
 for(i=0; i<controls.length; i++){
 if((controls[i].type == "range") || controls[i].checked){
 value = value + controls[i].getAttribute("name") + controls[i].value;
 }
 }

 for(i=0; i<outputs.length; i++){
 var name = outputs[i].getAttribute("name");
 if(name == value){
 outputs[i].style.display = 'block';
 } else if(name != "controls"){
 outputs[i].style.display = 'none';
 }
 }
 }
</script>
"""
```
Next we create a few divs with different outputs: here our outputs are simply the numbers one through 4, along with their text and roman numeral representations. We also define the input slider with the appropriate callback:
```py
In [4]:

WIDGETS = """
<div>
 <div name="num1", style="display:block">
 <p style="font-size:20px;">1: one (I)</p>
 </div>
 <div name="num2", style="display:none">
 <p style="font-size:20px;">2: two (II)</p>
 </div>
 <div name="num3", style="display:none">
 <p style="font-size:20px;">3: three (III)</p>
 </div>
 <div name="num4", style="display:none">
 <p style="font-size:20px;">4: four (IV)</p>
 </div>

<input type="range" name="num" min="1" max="4", step="1" style="width:200px", onchange="interactUpdate(this.parentNode);" value="1">
</div>
"""
```
Now if we run and view this script, we see a simple slider which shows and hides the  `div`s in the way we expect.
```py
In [5]:

from IPython.display import HTML
HTML(JS_FUNCTION + WIDGETS)

Out[5]:
# 1: one (I)
```







> [Source : ](https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNzQ1NzgyNzhdfQ==
-->