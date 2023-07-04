# cjm-psl-utils

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
                    markdown=False, # Return the source code formatted as markdown
                    remove_documentation=False): # Remove docstrings and comments
    """
    Returns the source code of an object, with an optional markdown formatting.
    """
    # Get the source code of the object
    source = inspect.getsource(obj)
    
    # If the remove_documentation flag is set to True, remove docstrings and comments
    if remove_documentation:
        in_docstring = False
        lines = source.split('\n')
        source = ''
        # Remove docstrings
        for line in lines:
            if line.strip().startswith(('\'\'\'', '\"\"\"')):
                in_docstring = not in_docstring
            elif not in_docstring:
                source += line + '\n'
        # Remove comments
        source = '\n'.join([line for line in source.split('\n')
                            if not line.strip().startswith(('#'))])
        source = source.replace('\n\n', '\n')

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

### file_extract

``` python
from cjm_psl_utils.core import file_extract
from pathlib import Path
```

``` python
fname = "../images/images.zip"
dest = Path("./images")
```

``` python
print(dest.exists())
file_extract(fname, dest)
print(dest.exists())
print(list(os.walk(dest))[0][2])
```

    False
    True
    ['cat.jpg']
