---
title: 'Why Docker is essential for researchers'
date: 2018-12-29
permalink: /posts/2019/12/why-docker-is-essential-for-researchers/
tags:
  - Docker
  - Reproducibility
  - Open Science
---

One of the best things that can happen during research is finding a software library that efficiently solves a problem you are struggling with so you can solve your own problem. But most of the time this happiness turns to frustration and sadness quickly because the library was written in 2003, is [unmaintained](https://xkcd.com/979/) and depends on Windows 95. 

It might also happen that you stumble old code of yourself and find that it does not work anymore. This especially happens often in Machine Learning, where everything is obsolete and stops working after about six months. 

This is particularly frustrating because one of the Tenets of Science is that it is reproducible. And how can your output -- in this case, code -- be reproducible if it does not even run or compile? And although maintenance of external libraries is beyond your control, it is still an impediment when you spend a day or two fixing someone else's Matlab code.

So what can we do about this? In this blog post, I will convince you that Docker is an essential tool towards reaching Always Working Code<sup>TM</sup> and reproducible science.

So what is Docker?
------
When you go to [https://docker.com](https://docker.com) you will find a whole bunch Enterprise Talk about continuous innovation and cloud-native applications, which you will abruptly leave without having learned anything. 

![](/images/2018-12-29-why-docker-is-essential-for-researchers/docker_logo.png)

Docker is an application that provides *operating-system-level virtualization*. You can think of this as a lightweight operating system that runs on top of your current operating system. It is lightweight in the sense that it does not run a full operating system but only its own libraries and applications in an isolated bundle.  

This is in the Docker nomenclature known as a "container". A container is what actually runs when people say they have it "running in a Docker". It is the instantiation of a Docker image, which is described by a configuration. So a configuration describes what applications and libraries are supposed to be in an image. This image is then built from a configuration, after which the image can be started with the right parameters as a container. Easy peasy lemon squeezy, right? 

So why Docker?
------
There are a few important upsides to this seemingly complex chain of operations:
- **Fixed environment**  
Because containers are fixed once they are created your program will always work within the Docker container, no matter what library you have installed on your computer. 
- **Easy sharing**  
So you've written a beautiful piece of code and want to share it with your supervisor/fellow researchers/journal reviewers? Great, send them a Docker image and they have it running within a minute! (Bonus points if it is in a [Jupyter Notebook](https://jupyter.org/), but that's for another time).
- **Separation of concerns**  
Although these advantages are more prominent in software development than in research they are still important. Docker allows for simple separation of concerns by just chucking unrelated parts in separate containers. Suppose you have developed a blog. This typically consists of a front-end (the website served to the reader), a back-end (to handle requests such as adding a comment or logging in) and a database (to store comments and blog posts). These are ideal candidates for three Docker containers. This has as advantages that a rogue connection can't take down your database because they are separated, different parts are easily swapped out for a different version with minimal changes, and different parts *scale* easily (e.g. having more than one back-end to handle adding multiple comments being added concurrently). 
- **Composability**  
If you have solved something once it is easy to reuse that component next time. Docker environments are very easily extended by composing multiple containers. This means you can also use solutions from others easily by just embedding them in your environment. These are often easily found on [Dockerhub](https://hub.docker.com/).

Docker for science
------
The advantages of Docker containers are so great that for publishing code in science it should be the absolute minimum. Having code that Always Works<sup>TM</sup> because of a fixed, isolated environment that has every detail of every environmental variable explicit is a blessing in the complex world that is software development.  

It must be admitted that Docker is not perfect. It has a steep learning curve and has a reduced performance because it is virtualized. But it is more than worth it. The steep learning curve is something that unfortunately needs to be mastered, but gets lower with every release of Docker and its companion libraries such as `docker-compose` and [Awesome Docker](https://github.com/veggiemonk/awesome-docker).  
In the end, it is better to have potentially slow code than non-working code. The slow code can be inspected and studied and can be optimized later.   

My Docker Utopia
------
Having one piece of code in a Docker container is a good start. But in a better world, we take it one step further. I want to have the entire pipeline from having only raw data to published paper captured in a reproducible workflow.  

There I propose the following architecture, which I dub **The Science Machine** (TSM). 
The exact details and architecture of The Science Machine are still a bit vague but the global idea is that it should do the following. 
Suppose you published a paper (Congratulations!). I want to be able to recreate the paper from only the raw, unfiltered, freshly-acquired data. TSM is a Docker container which has the raw data and LaTeX sources attached to it. TSM's main entry point is called `main` which looks something like this:
```
main():
    perform_data_filtering()
    process_data()
    generate_results()
    compile_latex()
```
`perform_data_filtering` -- as the name suggests -- processes and selects your raw data based on deterministic and reproducible criteria. This should prevent cherry-picking data because it supports your hypothesis and articulate *why* you exclude certain data points. It can also do certain transformations such that your data is ready for the next step.  

After this, you should have the data on which you draw your conclusions. In the step `process_data` you do your post-processing, statistical analysis, Deep Learning, etc. Then you should have trained models and other output on which you base your results. This step is easily merged with the next, `generate_results`, which should spit out plots, confidence intervals, hypotheses, tables, etc. These should be all your presentable results. These results are saved in a known location in a fixed format such that the results are unambiguous in what they mean and where they are derived from.  

In the final step, `compile_latex`, you take the results from the known locations and place them in the correct locations in your paper, as described by the LaTeX documents. This should produce a document which is exactly the same as the published paper if you use the same raw data. 

In the end, this should help everybody because the researcher is being explicit about their choices which should help the quality of their research and the ability to express and transfer their work. It also helps supervisors because all work and choices are explicit, progress is quantified and errors are easily spotted. It also helps other researchers because work is reproducible. All you have to do to reproduce results is to attach your own data and run TSM. In the end, it should create the same results. 

Conclusions
-----
By now, I hope to have convinced you of the value that Docker might offer for reproducible science if your output includes software. Having an explicit, fixed, and isolated environment is a prerequisite for software that is expected to always produce the same results, given the same data. Still, I think we can still do better by capturing the entire data processing pipeline in fixed environments. This is what I want to achieve by introducing The Science Machine. 
