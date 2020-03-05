---
title: Getting started
type: guide
order: 100
---

## Overview

Label Studio is a self-contained Web application for multi-typed data labeling and exploration. The backend is written in Python powered by Flask. The frontend is a The frontend is a backend-agnostic [React](https://reactjs.org/) + [MST](https://github.com/mobxjs/mobx-state-tree) precompiled scripts. 
Here are the main concepts behind Label Studio's workflow:

<div style="margin:auto; text-align:center; width:100%"><img src="/images/label-studio-overview.png"/></div>

- **Tasks** are the labeled items. Label Studio is a multi-type labeling tool - each task could be either text, image, audio URL, HTML text or any number and combination of these data resources.
- **Completions** are the labeling results. Could be exported in various common formats ready to use in machine learning pipelines.
- **Predictions** are the optional labeling results, but unlike completions they are used for generating prelabelings in annotation process.
- **Machine learning backend** connects popular machine learning frameworks to Label Studio for active learning & generating model predictions on-the-fly
- **Config** is a simple XML tree with **tags** used to configure UI elements, connect input data to output labeling scheme.
- **Project** encompasses tasks, config, predictions and completions all-in-one in an isolated directory
- **Labeling UI** is accessible from any browser, distributed as precompiled js/css scripts and could be [easily extendable with new labeling tags](frontend.html). You can also [embed Label Studio UI into your applications](frontend.html#Quickstart).


## Quickstart

### Prerequisites

Label Studio is supported for Python 3.5 or greater, running on Linux, Windows and MacOSX.

> Note: for Windows users the default installation may fail building `lxml` package. Consider manually installing it from [unofficial Windows binaries](https://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml) e.g. if you are running on x64 with Python 3.8, run `pip install lxml‑4.5.0‑cp38‑cp38‑win_amd64.whl`.


### Running with pip

To install Label Studio via pip, you need Python>=3.5 and run:
```bash
pip install label-studio
```

Then launch new project which stores all labeling data in a local directory `my_labeling_project`:

```bash
label-studio start my_labeling_project --init
```
The default browser will open automatically at [http://localhost:8200](http://localhost:8200). 

### Running with Docker

Label Studio is also distributed as a docker container. Make sure you have [Docker](https://www.docker.com/) installed on your local machine.

Install and start Label Studio at [http://localhost:8200](http://localhost:8200) storing all labeling data in `./my_labeling_project` directory:
```bash
docker run --rm -p 8200:8200 -v `pwd`/my_labeling_project:/label-studio/my_labeling_project --name label-studio heartexlabs/label-studio:latest
```

> Note: if `./my_labeling_project` folder exists, an exception will be thrown. Please delete this folder or use `--force` option.
> Note: for Windows, you have to modify the volumes paths set by `-v` option

You can override the default startup command by appending any of [available command line arguments]():

```bash
docker run -p 8200:8200 -v `pwd`/my_project:/label-studio/my_project --name label-studio heartexlabs/label-studio:latest label-studio start my_project --init --force --template image_mixedlabel
```

If you want to build a local image, run:
```bash
docker build -t heartexlabs/label-studio:latest .
```

### Running from source

If you want to use nighty builds, consider to download using Git and run Label Studio locally from source:

```bash
git clone https://github.com/heartexlabs/label-studio.git
cd label-studio
python setup.py develop
```

Then launch new project which stores all labeling data in a local directory `my_labeling_project`:

```bash
label-studio start my_labeling_project --init
```
The default browser will open automatically at [http://localhost:8200](http://localhost:8200).


## Input options

You can specify input tasks, project config, machine learning backend and other options via command line interface. Run `label-studio start --help` to see all available options.