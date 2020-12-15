---
title: "Common error On deploying Fastai notebook to Heroku"
description: "Just some tips"
layout: post
toc: true
comments: true
hide: false
search_exclude: true
categories: [fastai, heroku]
---

### Fasitai, voila and heroku
For anyone learning from the fastai "[Practical Deep Learning for Coders](https://course.fast.ai/)", one of the assignment is to deploy your own machine learning model and create a simple
web application. And Heroku is one of the easiest and fastest way to deploy them. While people claim that it's easy, it can still be hard for someone who have less experience in the 
python development environment. Here's a list of common error I found in the fastai forum, where people failed to use heroku.

**Disclaimer: This is not a full guide on using heroku, this just list some common problem people encounter when following the
[fastai guide](https://course.fast.ai/deployment_heroku), and the guide failed to mention. (Probably because the guide is not written for complete beginner)**.

In this guide: 
* The Jupyter notebook using for deployment will be called **deployment.ipynb**.
* **requirements.txt** is a list of python package that is needed when deploying the app.
* **Procfile** is the command to run when your webpage is loading up.
* **export.pkl** is the machine learning model that you export with ``` learn.export() ```.

### Common error 1: fastai version problem.

One of the most encountered problem is error from fastai. They are mostly costed by not using the same version of fastai installed in heroku 
and the version of fastai you use the train your **export.pkl** in Google colob or paperspace gradient.
These error don't have a common message, they are usually like this: 

``` 
AttributeError: Can't get attribute 'CrossEntropyLossFlat' on <module 'fastai.layers' from '/app/.heroku/python/lib/python3.6/site-packages/fastai/layers.py'>
```

These error usually happen because the version of fastai, or any package you install in heroku is not the same, so remember the check them.
To check the version of you are using in the notebook, call: ``` ! pip show fastai ```.

Use this command in the environment(e.g. Google Colb, paperspace Gradient) where you originally work on your model and make sure the version is the same.


### Common error 2: Wait, you are getting error message??

Some people when they deploy the app, they only see the voila message of which cell not working like this: 

``` 
There was an error when executing cell [3]. Please run Voilà with --debug to see the error message.
```

But then where do I run voila ?? Where should place this --debug flag??
The answer is the **Procfile**, Procfile is basically the command to run when the Web page start.
To see the error message, add it into the Procfile, and your Procfile will look something like this:

```
web: voila --port=$PORT --debug --no-browser --enable_nbextensions=True deployment.ipynb
```

### Common error 3: 500mb limit

redce packages, import form googld drive



### Common error 4: Pytorch CPU only version
use CPU wheel pakage, provide link




### Alternate method: streamlit
