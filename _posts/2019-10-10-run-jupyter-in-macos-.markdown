---
layout: post
title: "run-jupyter-notebook-in-macos"
date:  2019-10-10 10:00:00  +0800
categories: [dev]
tags: [jupyter]
---

## what is jupyter notebook
An web application which could share runnable source code and document.

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## install jupyter in macOS
```bash
bash-3.2$ pip3 install jupyter
Requirement already satisfied: jupyter in /usr/local/lib/python3.7/site-packages (1.0.0)
Requirement already satisfied: jupyter-console in /usr/local/lib/python3.7/site-packages (from jupyter) (6.0.0)
Requirement already satisfied: ipywidgets in /usr/local/lib/python3.7/site-packages (from jupyter) (7.5.1)
Requirement already satisfied: qtconsole in /usr/local/lib/python3.7/site-packages (from jupyter) (4.5.5)
Requirement already satisfied: ipykernel in /usr/local/lib/python3.7/site-packages (from jupyter) (5.1.2)
Requirement already satisfied: notebook in /usr/local/lib/python3.7/site-packages (from jupyter) (6.0.1)
Requirement already satisfied: nbconvert in /usr/local/lib/python3.7/site-packages (from jupyter) (5.6.0)
Requirement already satisfied: pygments in /usr/local/lib/python3.7/site-packages (from jupyter-console->jupyter) (2.4.2)
Requirement already satisfied: prompt-toolkit<2.1.0,>=2.0.0 in /usr/local/lib/python3.7/site-packages (from jupyter-console->jupyter) (2.0.9)
Requirement already satisfied: ipython in /usr/local/lib/python3.7/site-packages (from jupyter-console->jupyter) (7.8.0)
Requirement already satisfied: jupyter-client in /usr/local/lib/python3.7/site-packages (from jupyter-console->jupyter) (5.3.3)
Requirement already satisfied: widgetsnbextension~=3.5.0 in /usr/local/lib/python3.7/site-packages (from ipywidgets->jupyter) (3.5.1)
Requirement already satisfied: nbformat>=4.2.0 in /usr/local/lib/python3.7/site-packages (from ipywidgets->jupyter) (4.4.0)
Requirement already satisfied: traitlets>=4.3.1 in /usr/local/lib/python3.7/site-packages (from ipywidgets->jupyter) (4.3.2)
Requirement already satisfied: ipython-genutils in /usr/local/lib/python3.7/site-packages (from qtconsole->jupyter) (0.2.0)
Requirement already satisfied: jupyter-core in /usr/local/lib/python3.7/site-packages (from qtconsole->jupyter) (4.5.0)
Requirement already satisfied: tornado>=4.2 in /usr/local/lib/python3.7/site-packages (from ipykernel->jupyter) (6.0.3)
Requirement already satisfied: Send2Trash in /usr/local/lib/python3.7/site-packages (from notebook->jupyter) (1.5.0)
Requirement already satisfied: jinja2 in /usr/local/lib/python3.7/site-packages (from notebook->jupyter) (2.10.1)
Requirement already satisfied: terminado>=0.8.1 in /usr/local/lib/python3.7/site-packages (from notebook->jupyter) (0.8.2)
Requirement already satisfied: pyzmq>=17 in /usr/local/lib/python3.7/site-packages (from notebook->jupyter) (18.1.0)
Requirement already satisfied: prometheus-client in /usr/local/lib/python3.7/site-packages (from notebook->jupyter) (0.7.1)
Requirement already satisfied: testpath in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (0.4.2)
Requirement already satisfied: mistune<2,>=0.8.1 in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (0.8.4)
Requirement already satisfied: pandocfilters>=1.4.1 in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (1.4.2)
Requirement already satisfied: bleach in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (3.1.0)
Requirement already satisfied: entrypoints>=0.2.2 in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (0.3)
Requirement already satisfied: defusedxml in /usr/local/lib/python3.7/site-packages (from nbconvert->jupyter) (0.6.0)
Requirement already satisfied: wcwidth in /usr/local/lib/python3.7/site-packages (from prompt-toolkit<2.1.0,>=2.0.0->jupyter-console->jupyter) (0.1.7)
Requirement already satisfied: six>=1.9.0 in /usr/local/lib/python3.7/site-packages (from prompt-toolkit<2.1.0,>=2.0.0->jupyter-console->jupyter) (1.12.0)
Requirement already satisfied: appnope; sys_platform == "darwin" in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (0.1.0)
Requirement already satisfied: jedi>=0.10 in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (0.15.1)
Requirement already satisfied: pexpect; sys_platform != "win32" in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (4.7.0)
Requirement already satisfied: decorator in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (4.4.0)
Requirement already satisfied: backcall in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (0.1.0)
Requirement already satisfied: setuptools>=18.5 in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (41.2.0)
Requirement already satisfied: pickleshare in /usr/local/lib/python3.7/site-packages (from ipython->jupyter-console->jupyter) (0.7.5)
Requirement already satisfied: python-dateutil>=2.1 in /usr/local/lib/python3.7/site-packages (from jupyter-client->jupyter-console->jupyter) (2.8.0)
Requirement already satisfied: jsonschema!=2.5.0,>=2.4 in /usr/local/lib/python3.7/site-packages (from nbformat>=4.2.0->ipywidgets->jupyter) (3.0.2)
Requirement already satisfied: MarkupSafe>=0.23 in /usr/local/lib/python3.7/site-packages (from jinja2->notebook->jupyter) (1.1.1)
Requirement already satisfied: ptyprocess; os_name != "nt" in /usr/local/lib/python3.7/site-packages (from terminado>=0.8.1->notebook->jupyter) (0.6.0)
Requirement already satisfied: webencodings in /usr/local/lib/python3.7/site-packages (from bleach->nbconvert->jupyter) (0.5.1)
Requirement already satisfied: parso>=0.5.0 in /usr/local/lib/python3.7/site-packages (from jedi>=0.10->ipython->jupyter-console->jupyter) (0.5.1)
Requirement already satisfied: attrs>=17.4.0 in /usr/local/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat>=4.2.0->ipywidgets->jupyter) (19.2.0)
Requirement already satisfied: pyrsistent>=0.14.0 in /usr/local/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat>=4.2.0->ipywidgets->jupyter) (0.15.4)
```

## how to run jupyter
```bash
bash-3.2$ jupyter notebook
[I 10:05:20.420 NotebookApp] Serving notebooks from local directory: /Users/dancooper/Workspace/misc/dev/jupyter
[I 10:05:20.420 NotebookApp] The Jupyter Notebook is running at:
[I 10:05:20.420 NotebookApp] http://localhost:8888/?token=7c4458c4d52617ed3d0ab9e533ef6a2412b8d7a7e04479a9
[I 10:05:20.420 NotebookApp]  or http://127.0.0.1:8888/?token=7c4458c4d52617ed3d0ab9e533ef6a2412b8d7a7e04479a9
[I 10:05:20.420 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 10:05:20.426 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///Users/dancooper/Library/Jupyter/runtime/nbserver-70832-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=7c4458c4d52617ed3d0ab9e533ef6a2412b8d7a7e04479a9
     or http://127.0.0.1:8888/?token=7c4458c4d52617ed3d0ab9e533ef6a2412b8d7a7e04479a9
```

## how it works
* jupyter notebook starts a web server at localhost
* we could use the browser to manage a notebook: add source code and documentation
* we could save the notebook as a file such as Hello Jupyter.ipynb.
* the saved ipynb file could be run in website such as google Colaboratory.
* we could also export a notebook as a latex, html, pdf, and etc.

## how to export a notebook file as html files
```bash
bash-3.2$ jupyter nbconvert --to html --template full Hello\ Jupyter.ipynb 
[NbConvertApp] Converting notebook Hello Jupyter.ipynb to html
[NbConvertApp] Writing 285736 bytes to Hello Jupyter.html
```
