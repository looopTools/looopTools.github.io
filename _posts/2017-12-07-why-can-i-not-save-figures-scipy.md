---
layout: post
title:  "[Why can't I] Save matplotlib plots/graphs/figures"
categories: guide python scipy matplotlib
---

More and more of my fellow students and researchers have started to used a tool called [Jupyter notebooks][1] to contain perform the data analysis
in a contained environment using Python. Including plotting plots using [SciPy][2] and [matplotlib][3]. Both my colleagues and I really enjoy using
these features. However, a lot have initial problems with to things, one is showing the graphs in a Jupyter Notebook and the second is to store the plots.

Here I will illustrated how I do it. First you need to include a few libraries, see code example below and this will allow you to call the needed functions.
However, they will not allow you to show, the plots in a Jupyter Notebook. For that you will need to enable inline matplotlib, and that is what the line `%matplotlib inline` does. So these line should be enough for that part.

```
import pandas as pd
import numpy as np
%matplotlib inline
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
```

So the next thing will be to save the plot and this is where the code gets weird, without looking weird.
So in the code below I have omitted loading and analysing data, and basically only focusing on generating the plot figure.


```
fig = plt.figure()
my_xticks = ['1kB','1MB','10MB','20MB','32MB','64MB','128MB','256MB','512MB']
plt.xticks(data_size, my_xticks)
plt.plot(data_size, latency)
plt.legend(['G=32'])
plt.ylabel('Latency in ms')
plt.xlabel('Data size')
fig.savefig('results/graphs/full_vector_gen_32.eps')
plt.show()
```

The first line generate our figure, this figure, is what we want to save. The next six lines are used to configure the plot.
The seventh line `fig.savefig('results/graphs/full_vector_gen_32.eps')`saves the figure. HOWEVER, based on the documentation for matplotlib
that is not enough to save the figure. Because the next line `plt.show()` is what inline uses to show the figure. BUT! for some reason, this
line have to be called for the save function to work. I cannot figure out why and others claim that it works without, but I have not been
able to and others I know haven't either.

But this is how you can use save your figures from a Jupyter notebook. You can store them in different formats, but if you are using latex for your paper or report, why not go with the king `.eps`.



[1]: http://jupyter.org/ "Jupyter Notebook"
[2]: https://www.scipy.org/ "SciPy"
[3]: https://matplotlib.org/ "matplotlib"
