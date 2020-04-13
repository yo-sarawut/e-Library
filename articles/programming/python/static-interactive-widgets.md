# Static Interactive Widgets for IPython Notebooks

> Thu 05 December 2013

_Note: with the release of_ [_ipywidgets v0.6_](https://github.com/ipython/ipywidgets) _in early 2017, static widgets are now supported by the Jupyter project!_

The inspiration of my previous [kernel density estimation post](http://jakevdp.github.io/blog/2013/12/01/kernel-density-estimation/) was a blog post by [Michael Lerner](http://www.mglerner.com/blog/?p=28), who used my [JSAnimation](http://jakevdp.github.io/blog/2013/05/19/a-javascript-viewer-for-matplotlib-animations/) tools to do a nice interactive demo of the relationship between kernel density estimation and histograms.

This was on the heels of [Brian Granger](https://twitter.com/ellisonbg)'s excellent [PyData NYC Keynote](http://vimeo.com/79832657) where he live-demoed the brand new IPython interactive tools. This new functionality is very cool. Wes McKinney [remarked](https://twitter.com/wesmckinn/status/399560987415965696) that day on Twitter that "IPython's interact machinery is going to be a huge deal". I completely agree: the ability to quickly generate interactive widgets to explore your data is going to change the way a lot of people do their daily scientific computing work.

But there's one issue with the new widget framework as it currently stands: unless you're connected to an IPython kernel \(i.e. actually running IPython to view your notebook\), the widgets are useless. Don't get me wrong: they're incredibly cool when you're actually interacting with data. But the bread-and-butter of this blog and many others is static notebook views: for this purpose, widgets with callbacks to the Python kernel aren't so helpful.

This is where `ipywidgets` comes in.

## My Afternoon Hack: IPy-Widgets

I've been thinking about this issue for the past few weeks, but this morning as I was biking to work through Seattle's current cold-snap, the idea came to me. Interactive widgets can be done, and done rather easily. I got to work, and after doing a few things I couldn't put off, decided to forego my real research for the day and instead focus on the betterment of humanity \(or at least the growing portion of humanity who use the IPython notebook for their work\). For anyone who follows me [on Twitter](https://twitter.com/jakevdp), you might say I [chose option B](https://twitter.com/jakevdp/status/408678764705378304). The result is `ipywidgets`: a rough attempt at what, with some effort, might become a very useful library. You can view the current progress on my [GitHub](http://github.com/jakevdp/ipywidgets) page. To run the code in this notebook, clone that repository and type `python setup.py install`. The package is pure python, very lightweight, and should install painlessly on most systems.

The basic idea of creating these widgets is this: you set up a function that does something interesting, you specify the range of parameter choices, and call a function which pre-generates the results and displays a javascript slider which allows you to interact with these results. Here's a quick example of how it works:

First we set up a function which takes some arguments and plots something:

```python
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

Next, you import some tools from `ipywidgets`, and interact with your plot:

```python
In [2]:

from ipywidgets import StaticInteract, RangeWidget, RadioWidget

StaticInteract(plot,
               amplitude=RangeWidget(0.1, 1.0, 0.1),
               color=RadioWidget(['blue', 'green', 'red']))
```

Out\[2\]:

![](data:image/png;base64,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%0ANIhIyf8DzqfcRx15MIsAAAAASUVORK5CYII=)

blue: green: red:

That's all there is to it!

## How this all works

Because this is a static view, all the output must be pre-generated and saved in the notebook. The way this works is to save the generated frames within divs that are hidden and shown whenever the widget is changed. Here's a rough sample that gives the idea of what's going on with the HTML and Javascript in the background:

First we define a javascript function which takes the values from HTML5 `input` blocks, and shows and hides items based on those inputs.

```python
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

```python
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

Now if we run and view this script, we see a simple slider which shows and hides the `div`s in the way we expect.

```python
In [5]:

from IPython.display import HTML
HTML(JS_FUNCTION + WIDGETS)

Out[5]:
# 1: one (I)
```

That's all there is to it!

After writing some Python scripts to generate the HTML and Javascript code for us, we have our static interactive widgets.

## Some Examples

Now that this is in place, let's look at a few more examples of what this allows:

### Fibonacci Numbers

The simplest thing we can do is simply save some textual output. Let's write a function which displays the first $N$ Fibonacci numbers, and tie it to a slider:

```python
In [6]:

def show_fib(N):
    sequence = ""
    a, b = 0, 1
    for i in range(N):
        sequence += "{0} ".format(a)
        a, b = b, a + b
    return sequence

from ipywidgets import StaticInteract, RangeWidget
StaticInteract(show_fib,
               N=RangeWidget(1, 100))

Out[6]:

# 0
```

A slightly silly example, sure, but it shows just how easy it is to do this!

### SymPy Math

For some fancier mathematical gymnastics, we can turn to SymPy. [SymPy](http://sympy.org/) is a package which does Symbolic computation in Python. It has the ability to nicely render its output in the IPython notebook. Let's take a look at a simple factoring example with Sympy \(the following requires SymPy 0.7 or greater\):

```python
In [7]:

# Initialize notebook printing
from sympy import init_printing
init_printing()

# Create a factorization function
from sympy import Symbol, Eq, factor
x = Symbol('x')
def factorit(n):
    return Eq(x ** n - 1, factor(x ** n - 1))

# Make it interactive!
from ipywidgets import StaticInteract, RangeWidget
StaticInteract(factorit,
               n=RangeWidget(2, 20))
```

Out\[7\]:

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAANUAAAAZBAMAAABURHZ/AAAAMFBMVEX///8AAAAAAAAAAAAAAAAA%0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHarIkSJZt3NVLsy%0Ame8Q6PJIAAACj0lEQVRIDb2VP2gTURzHv5deLndJGkMFoQhyrZC1IoJL0VvEISDBQRwEqw7qUOwg%0AqKBQWoe2UxyEXlWI4CBOFQSn0myODXQWOujgZCoKIkJ9v/fn8t69u9ql+Q3vfn8+v9/37vVHAwib%0A3ahL79AfXjTSPnQRKeBH1Z/D0qq13F/D0gLKu8PT8sMDaH3KY0pdUanO5RGPtcKs5nM3sBfTXU9D%0ACTktKs1MAM+AkW5SKvUSVzjupq2VIc9gTgaiiw3NsCb9fdpJ4QquJT45zsZ5W6thIDIQZGGGQnHK%0AApxIeMe3SStprq69e68Q+Zyytb6kEI10diioRXQqK4fSK5DWCZWu7e31lS+ftlZxPoXo5BoFVw3A%0A1Ao6wNjJC43QYERga3k9dreTZy7fTNGc5LtFx2CeqcW6nZnSgt9OdVMote7GZK8oU5kDjuFhuEyB%0AZpx8RImP7GUG80ytUhte3dstR1qncu3v8jvADdyrv1GIfHLyLQUr0OeZWuV5OAjWk15ndYnZcpcS%0AtlatBdTxgtPjBC695D4nt8j9yr5rMM/UqvYZcCQkzLJsLeBHNqm01Dwvjle/xXGPaL6HXGury97W%0ANql1h3/AItXpDlH9y17dNE7yFWR3CCTzzO9iW1yuT6Gwj5Y2lnbjdaGPCS1HLtdSu6HNM7XYblzv%0AbOJiqpmH9h16p1D8U+m7TNIwTn6m1C3o80yt0R6OTo7dTjdT2/b3xXSa3YJzeqLxgMqaCfI5ZdhF%0AavOU1ui532eBoKX1/N99mo+4O1TzIzqVKS0RX1Lpgz2f5GNeSDXz16JoXEz6v03+LF6pRLnAuKh8%0AyAWcdm4ps5DzW0msFGlm9lFyn/fM7slcWEJLkWiwdlSk2Xkf+AdgGIh8PzP/hAAAAABJRU5ErkJg%0Agg==)

By moving the slider, we see the factorization of the resulting polynomial.

### Matplotlib

And of course, you can use this to display matplotlib plots. Keep in mind, though, that every image must be pre-generated and stored in the notebook, so if you have a large number of settings \(or combinations of multiple settings\), the notebook size will blow up very quickly!

For this example, I want to quickly revisit the [post](http://www.mglerner.com/blog/?p=28) which inspired me, and compare the kernel density estimation of a distribution with a couple kernels and bandwidths. We'll make the figure smaller so as to not blow-up the size of this notebook:

```python
In [8]:

%matplotlib inline
from sklearn.neighbors import KernelDensity
import numpy as np

np.random.seed(0)
x = np.concatenate([np.random.normal(0, 1, 1000),
                    np.random.normal(1.5, 0.2, 300)])

def plot_KDE_estimate(kernel, b):
    bandwidth = 10 ** (0.1 * b)
    x_grid = np.linspace(-3, 3, 1000)
    kde = KernelDensity(bandwidth=bandwidth,
                        kernel=kernel)
    kde.fit(x[:, None])
    pdf = np.exp(kde.score_samples(x_grid[:, None]))

    fig, ax = plt.subplots(figsize=(4, 3),
                           subplot_kw={'axisbg':'#EEEEEE',
                                       'axisbelow':True})
    ax.grid(color='w', linewidth=2, linestyle='solid')
    ax.hist(x, 60, histtype='stepfilled', normed=True,
            edgecolor='none', facecolor='#CCCCFF')
    ax.plot(x_grid, pdf, '-k', lw=2, alpha=0.5)
    ax.text(-2.8, 0.48,
            "kernel={0}\nbandwidth={1:.2f}".format(kernel, bandwidth),
            fontsize=14, color='gray')

    ax.set_xlim(-3, 3)
    ax.set_ylim(0, 0.601)

    return fig

In [9]:

from ipywidgets import StaticInteract, RangeWidget
StaticInteract(plot_KDE_estimate,
               kernel=RadioWidget(['gaussian', 'tophat', 'exponential'],
                                  delimiter="<br>"),
               b=RangeWidget(-14, 8, 2))
```

Out\[9\]:

![](data:image/png;base64,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%0ATkSuQmCC)

```text
gaussian:  
tophat:  
exponential:
```

Sliding the slider adjusts the bandwidth, and the radio buttons change the kernel used.

## Summary

I'm pretty excited about these tools. I think they'll allow for some really interesting demos and visualizations, especially if more time can be spent polishing them. The package is still very rough: it offers little flexibility in how the widgets are displayed, it only implements radio buttons and a slider, and it still hiccups at times when the slider items are floating-point values \(this is due to differences in Javascript's and Python's default representations of floating point numbers\). Regardless, I hope you have fun playing with this, and I hope to see some posts using this on other blogs in the near future!

Happy Hacking!

_This post was written entirely in the IPython notebook. You can_ [_download_](http://jakevdp.github.com/downloads/notebooks/IPythonWidgets.ipynb) _this notebook, or see a static view_ [_here_](http://nbviewer.ipython.org/url/jakevdp.github.com/downloads/notebooks/IPythonWidgets.ipynb)_._

> [Source : ](https://jakevdp.github.io/blog/2013/12/05/static-interactive-widgets/).

