# Python

## conda

### Jupyter

```bash
jupyter notebook --generate-config  # Jupyter Notebook config
jupyter server --generate-config  # Jupyter Lab config
```

jupyter config

> jupyter_*_config.py:
> ```python
> ## The directory to use for notebooks and kernels.
> #  Default: ''
> c.ServerApp.root_dir = ''         # for lab
> c.NotebookApp.notebook_dir = ''   # for notebook
> ```
