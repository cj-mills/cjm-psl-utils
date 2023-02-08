cjm-psl-utils
================

<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

This file will become your README and also the index of your
documentation.

## Install

``` sh
pip install cjm_psl_utils
```

## How to use

### get_source_code

``` python
from cjm_psl_utils.core import get_source_code
```

``` python
get_source_code(get_source_code, markdown=True)
```

``` python
def get_source_code(obj:object, # The object whose source code you want to retrieve.
                    markdown=False): # Returns the source code formatted as markdown
    """
    Returns the source code of an object, with an optional markdown formatting.
    """
    # Get the source code of the object
    source = inspect.getsource(obj)
    
    if markdown:
        # Format the source code as markdown code block
        source = f"```python\n{source}\n```"
        
        # Check if the code is running in Jupyter Notebook
        try:
            get_ipython
            from IPython.display import Markdown
            # Format the source code as an IPython Markdown object
            source = Markdown(source)
        except NameError:
            # If not in Jupyter Notebook, do nothing
            pass
    # Return the formatted source code
    return source
```
