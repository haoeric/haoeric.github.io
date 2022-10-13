---
layout: post
title: Commonly Used Jupyter Notebook Configurations
comments: true
categories: [Skills]
tags: [jupyter, notebook, python, shortcut]
---



### For high resolution plot using plotnine

```python
import plotnine as p9

from IPython.display import set_matplotlib_formats
set_matplotlib_formats('svg')

%matplotlib inline
```



### Change display rows, columns

```python
pd.set_option('display.max_rows', 1000)
pd.set_option('display.max_colwidth', 1000)
```

### Change the cell width

```
from IPython.core.display import display, HTML
display(HTML("<style>.container { width:80% !important; }</style>"))
```


### Change working directory path 

```python
sys.path.insert(1, '/a/b/c')
```
