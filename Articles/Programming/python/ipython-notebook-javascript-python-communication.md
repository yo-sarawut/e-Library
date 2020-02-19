
IPython Notebook: Javascript/Python Bi-directional Communication
===

> Sat 01 June 2013


_Note: recent releases of IPython/Jupyter greatly streamline this kind of communication, and the approach in this post will no longer work as shown here._

I've been working with javascript and the IPython notebook recently, and found myself in need of a way to pass data back and forth between the Javascript runtime and the IPython kernel. There's a bit of information about this floating around on various mailing lists and forums, but no real organized tutorial on the subject. Partly this is because the tools are relatively specialized, and partly it's because the functionality I'll outline here is planned to be  [obsolete](https://github.com/ipython/ipython/wiki/Roadmap:-IPython)  in the 2.0 release of IPython.

Nevertheless, I thought folks might be interested to hear what I've learned. What follows are a few basic examples of moving data back and forth between the IPython kernel and the browser's javascript. Note that if you're viewing this statically (i.e. on the blog or on nbviewer) then the javascript calls below will not work: to see the code in action, you'll need to  [download](http://jakevdp.github.io/downloads/notebooks/JSInteraction.ipynb)  the notebook and open it in IPython.

## Executing Python Statements From Javascript[](https://jakevdp.github.io/blog/2013/06/01/ipython-notebook-javascript-python-communication/#Executing-Python-Statements-From-Javascript)

The key functionality needed for interaction between javascript and the IPython kernel is the  `kernel`  object in the IPython Javascript package. A python statement can be executed from javascript as follows:

```py
var kernel = IPython.notebook.kernel;
kernel.execute(command);
```

where  `command`  is a string containing python code.

Here is a short example where we use HTML elements and javascript callbacks to execute a statement in the Python kernel from Javascript, using the  `kernel.execute`  command:
```py
In [1]:

from IPython.display import HTML

input_form = """
<div style="background-color:gainsboro; border:solid black; width:300px; padding:20px;">
Variable Name: <input type="text" id="var_name" value="foo"><br>
Variable Value: <input type="text" id="var_value" value="bar"><br>
<button onclick="set_value()">Set Value</button>
</div>
"""

javascript = """
<script type="text/Javascript">
 function set_value(){
 var var_name = document.getElementById('var_name').value;
 var var_value = document.getElementById('var_value').value;
 var command = var_name + " = '" + var_value + "'";
 console.log("Executing Command: " + command);
  
 var kernel = IPython.notebook.kernel;
 kernel.execute(command);
 }
</script>
"""

HTML(input_form + javascript)

Out[1]:

Variable Name:  
Variable Value:  
Set Value
```
After pressing  Set Value  above with the default arguments, the value of the variable  `foo`  is set in the Python kernel, and can be accessed from Python:
```py
In [2]:

print foo

bar
```
Examining the code, we see that when the button is clicked, the  `set_value()`  function is called, which constructs a simple Python statement assigning  `var_value`  to the variable given by  `var_name`. As mentioned above, the key to interaction between Javascript and the notebook kernel is to use the  `IPython.notebook.kernel.execute()`  command, passing valid Python code in a string. We also log the result to the javascript console, which can be helpful for Javascript debugging.

## Accessing Python Output In Javascript[](https://jakevdp.github.io/blog/2013/06/01/ipython-notebook-javascript-python-communication/#Accessing-Python-Output-In-Javascript)

Executing Python statements from Javascript is one thing, but we'd really like to be able to do something with the output.

In order to process the output of a Python statement executed in the kernel, we need to add a callback function to the  `execute`  statement. The full extent of callbacks is a bit involved, but the first step is to set a callback which does something with the  `output`  attribute.

To set an output, we pass a Javascript callback object to the execute call, looking like this:

```
var kernel = IPython.notebook.kernel;
function callback(out_type, out_data){
    // do_something
}
kernel.execute(command, {"output": callback});


```

Using this, we can execute a Python command and do something with the result. The python command can be as simple as a variable name: in this case, the value returned is simply the value of that variable.

To demonstrate this, we'll first import  `pi`  and  `sin`  from the  `math`  package in Python:

In [3]:

from math import pi, sin

And then we'll manipulate this value via Javascript:

In [4]:

# Add an input form similar to what we saw above
input_form = """
<div style="background-color:gainsboro; border:solid black; width:600px; padding:20px;">
Code: <input type="text" id="code_input" size="50" height="2" value="sin(pi / 2)"><br>
Result: <input type="text" id="result_output" size="50" value="1.0"><br>
<button onclick="exec_code()">Execute</button>
</div>
"""

# here the javascript has a function to execute the code
# within the input box, and a callback to handle the output.
javascript = """
<script type="text/Javascript">
 function handle_output(out_type, out){
 console.log(out_type);
 console.log(out);
 var res = null;
 // if output is a print statement
 if(out_type == "stream"){
 res = out.data;
 }
 // if output is a python object
 else if(out_type === "pyout"){
 res = out.data["text/plain"];
 }
 // if output is a python error
 else if(out_type == "pyerr"){
 res = out.ename + ": " + out.evalue;
 }
 // if output is something we haven't thought of
 else{
 res = "[out type not implemented]"; 
 }
 document.getElementById("result_output").value = res;
 }
  
 function exec_code(){
 var code_input = document.getElementById('code_input').value;
 var kernel = IPython.notebook.kernel;
 var callbacks = {'output' : handle_output};
 document.getElementById("result_output").value = "";  // clear output box
 var msg_id = kernel.execute(code_input, callbacks, {silent:false});
 console.log("button pressed");
 }
</script>
"""

HTML(input_form + javascript)

Out[4]:

Code:  
Result:  
Execute

Pressing  Execute  above will call  `kernel.execute`  with the contents of the  **Code**  box, passing a callback which displays the result in the result box.

The reason the callback has so many conditionals is because there are several types of outputs we need to handle. Note that the output handler is given as the  `output`  attribute of a Javascript object, and passed to the  `kernel.execute`  function. Again, we use  `console.log`  to allow us to inspect the objects using the Javascript console.

## Application: An On-the-fly Matplotlib Animation[](https://jakevdp.github.io/blog/2013/06/01/ipython-notebook-javascript-python-communication/#Application:-An-On-the-fly-Matplotlib-Animation)

In a  [previous post](http://jakevdp.github.io/blog/2013/05/19/a-javascript-viewer-for-matplotlib-animations/)  I introduced a javascript viewer for matplotlib animations. This viewer pre-computes all the matplotlib frames, embeds them in the notebook, and offers some tools to view them.

Here we'll explore a different strategy: rather than precomputing all the frames before displaying them, we'll use the javascript/python kernel communication and  _generate the frames as needed_.

Note that if you're viewing this statically (e.g. in nbviewer or on my blog), it will be relatively unexciting: with no IPython kernel available, calls to the kernel will do nothing. To see this in action, please  [download](http://jakevdp.github.io/downloads/notebooks/JSInteraction.ipynb)  the notebook and open it with a running IPython notebook instance.

In [6]:

%pylab inline

Welcome to pylab, a matplotlib-based Python environment [backend: module://IPython.kernel.zmq.pylab.backend_inline].
For more information, type 'help(pylab)'.

In [7]:

from IPython.display import HTML
from cStringIO import StringIO

# We'll use HTML to create a control panel with an
# empty image and a number of navigation buttons.

disp_html = """
<div class="animation" align="center">
<img id="anim_frame" src=""><br>
<button onclick="prevFrame()">Prev Frame</button>
<button onclick="reverse()">Reverse</button>
<button onclick="pause()">Pause</button>
<button onclick="play()">Play</button>
<button onclick="nextFrame()">Next Frame</button>
</div>
"""

# now the javascript to drive it.  The nextFrame() and prevFrame()
# functions will call the kernel and pull-down the frame which
# is generated.  The play() and reverse() functions use timeouts
# to repeatedly call nextFrame() and prevFrame().

javascript = """
<script type="text/Javascript">
var count = -1;  // keep track of frame number
var animating = 0;  // keep track of animation direction
var timer = null;
var kernel = IPython.notebook.kernel;

function output(out_type, out){
 data = out.data["text/plain"];
 document.getElementById("anim_frame").src = data.substring(1, data.length - 1);
  
 if(animating > 0){
 timer = setTimeout(nextFrame, 0);
 }
 else if(animating < 0){
 timer = setTimeout(prevFrame, 0);
 }
}

var callbacks = {'output' : output};

function pause(){
 animating = 0;
 if(timer){
 clearInterval(timer);
 timer = null;
 }
}

function play(){
 pause();
 animating = +1;
 nextFrame();
}

function reverse(){
 pause();
 animating = -1;
 prevFrame();
}

function nextFrame(){
 count += 1;
 var msg_id = kernel.execute("disp._get_frame_data(" + count + ")", callbacks, {silent:false});
}

function prevFrame(){
 count -= 1;
 var msg_id = kernel.execute("disp._get_frame_data(" + count + ")", callbacks, {silent:false});
}

// display the first frame
setTimeout(nextFrame, 0);

</script>
"""

# Here we create a class whose HTML representation is the above
# HTML and javascript.  Note that we've hard-coded the global
# variable name `disp` in the Javascript, so you'll have to assign
# the resulting object to this name in order to view it.

class DisplayAnimation(object):
    def __init__(self, anim):
        self.anim = anim
        self.fig = anim._fig
        plt.close(self.fig)
        
    def _get_frame_data(self, i):
        anim._draw_frame(i)
        buffer = StringIO()
        fig.savefig(buffer, format='png')
        buffer.reset()
        data = buffer.read().encode('base64')
        return "data:image/png;base64,{0}".format(data.replace('\n', ''))
    
    def _repr_html_(self):
        return disp_html + javascript

This code should be considered a proof-of-concept: in particular, it requires the display object to be named  `disp`  in the global namespace. But making it more robust would be a relatively simple process.

Here we'll test the result by creating a simple animation and displaying it dynamically:

In [8]:

from matplotlib import animation

fig = plt.figure()
ax = plt.axes(xlim=(0, 10), ylim=(-2, 2))
line, = ax.plot([], [], lw=2)

def init():
    line.set_data([], [])
    return line,

def animate(i):
    x = np.linspace(0, 10, 1000)
    y = np.cos(i * 0.02 * np.pi) * np.sin(x - i * 0.02 * np.pi)
    line.set_data(x, y)
    return line,

anim = animation.FuncAnimation(fig, animate, init_func=init,
                               frames=100, interval=30)

# For now, we need to name this `disp` for it to work
disp = DisplayAnimation(anim)
disp

Out[8]:

![](https://jakevdp.github.io/blog/2013/06/01/ipython-notebook-javascript-python-communication/)  
Prev Frame  Reverse  Pause  Play  Next Frame

Once again, if you're viewing this statically, you'll see nothing above the buttons. The kernel needs to be running in order to see this: you can  [download the notebook](http://jakevdp.github.io/downloads/notebooks/JSInteraction.ipynb)  and run it to see the results (To see a statically-viewable version of the animation, refer to the  [previous post](http://jakevdp.github.io/blog/2013/05/19/a-javascript-viewer-for-matplotlib-animations/)). But I assure you, it works! We've created an animation viewer which uses bi-directional communication between javascript and matplotlib to generate the frames in real-time.

Note that this is still rather limited, and should be considered a proof-of-concept more than a finished result. In particular, on my four-year-old linux box, I can only achieve a frame-rate of about 10 frames/sec. Part of this is due to the reliance on png images saved within matplotlib, as we can see by profiling the function:

In [10]:

def save_to_mem(fig):
    buffer = StringIO()
    fig.savefig(buffer, format='png')
    buffer.reset()
    data = buffer.read().encode('base64')
    return "data:image/png;base64,{0}".format(data.replace('\n', ''))

fig, ax = plt.subplots()
ax.plot(rand(200))

Out[10]:

[<matplotlib.lines.Line2D at 0x3a26f50>]

![](data:image/png;base64,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%0ANTAwgJ07dzqX2bdvH/r6+uqWKxX2N2rceuutU92EGRNTeSxn4m1RXJutE1aB9xXlWq1m/Z78exFF%0AFFFEEfmHFdH09/dj7969p3/fu3cvBgYGrMvs27cP/f39kZtZRBFFFFFEaFgFfsOGDRgcHMSePXsw%0APj6Oe++9F5s3b65bZvPmzfjyl78MAHj00UexYMGCBjxTRBFFFFFE88OKaMrlMu68805cffXVqFar%0A2LJlC9asWYO77roLALB161a8853vxP33348VK1agp6cHX/ziF5vS8CKKKKKIIhxRyzkeeOCB2qpV%0Aq2orVqyo3X777XlvbkbGueeeW1u7dm1t/fr1tUsuuaRWq9Vqr732Wu1tb3tbbeXKlbWrrrqqdvTo%0A0SluZWvGe9/73trSpUtrF1544enPbMfutttuq61YsaK2atWq2je/+c2paHJLh+54fvzjH6/19/fX%0A1q9fX1u/fn3t/vvvP/234nia4+WXX65t3LixdsEFF9Te+MY31j7zmc/UarW412euAl+pVGrnn39+%0A7cUXX6yNj4/X1q1bV9u9e3eem5yRsXz58tprr71W99lHPvKR2h133FGr1Wq122+/vfbRj350KprW%0A8vHQQw/VHn/88TpBMh27p59+urZu3bra+Ph47cUXX6ydf/75tWq1OiXtbtXQHc9bbrml9ulPf7ph%0A2eJ42uPAgQO1J554olar1WpDQ0O1N7zhDbXdu3dHvT5znarAp46+CL+oiUokPv7gPe95D/7xH/9x%0AKprV8vGWt7wFCxcurPvMdOy2bduG66+/Hh0dHVi+fDlWrFiBXbt2Nb3NrRy64wnoK+WK42mPs846%0AC+vXrwcAzJs3D2vWrMH+/fujXp+5CryuRn7//v15bnJGRqlUwtve9jZs2LABf/VXfwUAOHjw4Olk%0Adl9f34wbXJZnmI7dK6+8UlclVlyv/vHZz34W69atw5YtW3Ds2DEAxfEMiT179uCJJ57ApZdeGvX6%0AzFXgi8FNceKRRx7BE088gQceeAB//ud/jh/84Ad1fy+VSsWxThmuY1ccV3fcdNNNePHFF/Hkk0/i%0A7LPPxoc+9CHjssXxbIyTJ0/i2muvxWc+8xn09vbW/S3r9ZmrwPvU0RfhjrPPPhsAsGTJEvzqr/4q%0Adu3ahb6+Prz66qsAgAMHDmDp0qVT2cRpFaZjV4zpSBdLly49LUS/93u/dxobFMfTHRMTE7j22mtx%0Aww034Fd+5VcAxL0+cxV4nzr6IuwxMjKCoaEhAMDw8DC+9a1vYe3atdi8eTO+9KUvAQC+9KUvnb44%0AinCH6dht3rwZf/d3f4fx8XG8+OKLGBwcxC/8wi9MZVOnRRw4cOD0/7/+9a9j7dq1AIrj6YparYYt%0AW7bgggsuwAc/+MHTn0e9PnNMEtdqtVrt/vvvr73hDW+onX/++bXbbrst783NuHjhhRdq69atq61b%0At672xje+8fQxfO2112q/9Eu/VJRJOuK6666rnX322bWOjo7awMBA7Qtf+IL12H3yk5+snX/++bVV%0Aq1bVtm/fPoUtb82Qx/Pzn/987YYbbqitXbu2dtFFF9Wuueaa2quvvnp6+eJ4muMHP/hBrVQq1dat%0AW3e6xPSBBx6Ien2WarViopgiiiiiiJkY0/6NTkUUUUQRReijEPgiiiiiiBkahcAXUUQRRczQKAS+%0AiCKKKGKGRiHwRRRRRBEzNAqBL6KIIoqYofH/AXtefgmaVOPdAAAAAElFTkSuQmCC)

In [11]:

%timeit save_to_mem(fig)

10 loops, best of 3: 54.2 ms per loop

That's a cap of about 20 frames per second on matplotlib's end, not including the time required to serialize and send the data, or to render each frame on the page. I'm certain there are much better ways to do this particular application, but they would take a bit more thought.

I hope this post was helpful to you, as unpolished as the results are, and please let me know if you have ideas about how to do this more effectively! Also, keep in mind that Javascript support should be improving immensely in IPython 2.0, which (according to the  [roadmap](https://github.com/ipython/ipython/wiki/Roadmap:-IPython)) should be released in December of 2013. At that point I may have more to say on the subject!

_This post was composed entirely in IPython notebook._  _The source notebook can be downloaded_  [here](http://jakevdp.github.io/downloads/notebooks/JSInteraction.ipynb)

> [Source : ](https://jakevdp.github.io/blog/2013/06/01/ipython-notebook-javascript-python-communication/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyOTM4MjEyOSwtNzA4MTg0NzQ3XX0=
-->