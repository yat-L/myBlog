---
title: "Common error On deploying Fastai notebook to Heroku"
description: Tips on using Heroku and voila
layout: post
toc: true
comments: true
hide: false
search_exclude: true
categories: [fastai, heroku]
image: images/heroku-logo.png
---
![heroku](images/heroku-logo.png)

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

One of the most encountered problem is error from fastai. They are mostly caused by not using the same version of fastai installed in heroku 
and the version of fastai you use the train your **export.pkl** in Google colob or paperspace gradient.
These error don't have a common message, they are usually like this: 

``` 
AttributeError: Can't get attribute 'CrossEntropyLossFlat' on <module 'fastai.layers' from '/app/.heroku/python/lib/python3.6/site-packages/fastai/layers.py'>
```

These error usually happen because the version of fastai, or any package you install in heroku is not the same, so remember the check them.
To check the version of you are using in the notebook, call: ``` !pip show fastai ```.

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

### Common error 3: 500 mb limit

Since we are using the free version of heroku, which only have 500 mb of storage, we have to minimize our package installed in heroku.
Therefore, doing ``` pip freeze > requirements.txt ``` is not a option for generating **requirements.txt**.

First of all, all the package you installed with pip at the start of the notebook deployment.ipynb should be transfered to **requirements.txt**.
If you include all the minimum files and package, and the size is still larger than 500 mb, the next step would be linking them from Google drive and 
other cloud service.
You should link them by including the following code block at the beginning of **deployment.ipynb**:

```
import urllib.request

MODEL_URL = "https://drive.google.com/uc?export=download&id=YOUR_FILE_ID"
urllib.request.urlretrieve(MODEL_URL, "export.pkl")

learner = load_learner(Path("."), "export.pkl")
```

Make sure to replace the ``` YOUR_FILE_ID ``` in the code block with your own.
This method not only good for linking your **export.pkl**, it can also be used for other files. For example, image to make your site prettier.
This can effectively reduce the size needed.

### Common error 4: Pytorch CPU only version
In the [guide](https://course.fast.ai/deployment_heroku) I linked at the start of this tutorial, they include a example **requirements.txt**, which is
the right one at the time. Since fastai is under heavy development, the pytorch version used in the latest fastai might be different. We also cannot 
just right pytorch in the **requirements.txt** because heroku have no GPU, and we can only use the CPU version of pytorch.

Therefore, we have to download our own persion of pytorch in this [link](https://download.pytorch.org/whl/torch_stable.html).
(You can also find the link with a quick google of "pytorch wheel").

To find the right version of pytorch to download, make sure that it start with ``` cpu/torch ``` for CPU only version.
Also make sure it's for Linux, not Macos or Windows.
When building the website, heroku have to install the packages in **requirements.txt** and it will tell you which version of pytorch should be used in
the fastai version of your choice.
Your **requirements.txt** should looks like this:

```
https://download.pytorch.org/whl/cpu/torch-1.7.0%2Bcpu-cp36-cp36m-linux_x86_64.whl
https://download.pytorch.org/whl/cpu/torchvision-0.8.0-cp36-cp36m-linux_x86_64.whl
fastai
voila
ipywidgets
```


### Alternate method: streamlit intead of voila
Lot's of people are having trouble using voila, but voila is not the only choice out there. One of the other popular choice would be 
[Streamlit](https://www.streamlit.io/). 

Streamlit is also pretty easy to use and have lots of feature packed in. But the downside is that it do not support Jupyter notebook file .ipynb, only 
.py is supported, to make this work, you may need to convert .ipynb file to a working .py file, and also change the **requirements.txt** and the
**Procfile**. **requirement.txt** should include streamlit, and the **Procfile** should change to a command for starting Streamlit.

For more information on using Streamlit on Heroku, check out other blog posts from the community.

[From Streamlit to Heroku](https://towardsdatascience.com/from-streamlit-to-heroku-62a655b7319)


### Summary

Heroku can be easy to use if you understand what it's doing, if you have other question, feel free the comment below.
