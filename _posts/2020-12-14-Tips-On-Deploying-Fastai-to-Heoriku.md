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
One of the most encountered problem is error from fastai.




### Common error 2: 500mb limit
reduce packages, import form googld drive



### Common error 3: Pytorch CPU only version
use CPU wheel pakage, provide link


### Common error 4: Debugging
use --debug flag



### Alternate method: streamlit
