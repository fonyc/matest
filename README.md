Introduction
===================

Mate is an open source CI tool that can make easier the software building, testing, deployment through automatization. It is docker contained itself aswell every action that Mate runs.  

Table of Contents
=================

  * [Introduction](#introduction)
  * [Why Mate](#why-mate)
  * [Installing Mate](#installing-mate)
  * [Matefile](#matefile)
    * [Example](#matefile-example)
   
  
## Introduction

Mate is an open source CI tool that can make easier the software building, testing, deployment through automatization. It is docker contained itself aswell every action Mate runs.  


## Why Mate
- Mate runs every action and itself in a docker container, making the process faster? and free of dependecies. 
- Mate follows 2 principles: 
  - Convention over configuration (Thats why you cant configure the workspace in some other directory)

## Installing Mate


## Matefile
Matefiles are constructed with YAML

``` triggers:
- trigger: test
  chains:
    - start:
      - build: Dockerfile
```


### Example
The first thing we do is downloading the Mate repository

``` git clone www.github.com/mateci ```

Now we go to the mate folder and build the image 

```docker build -t mateci/mate .```

For a fast test we can fake a trigger, and run mate with this line: 

```docker run --rm -e MATE_TRIGGER=test -v $PWD:/work -v /var/run/docker.sock:/var/run/docker.sock -v env:/env mateci/mate```

But let's explain this more slow. 

``` -v $PWD:/work ``` The current folder will be shared with the /work folder in the docker container. This shows the Convention over configuration principle we believe. Also, the next action will be able to access the /work folder with the changes that the previous action did. 

``` -v /var/run/docker.sock:/var/run/docker.sock ``` 

``` -v env:/env mateci/mate ``` In /env we save all the environment variables that the next action will recieve, because actions cant communicate directly but yes like this. Let's enlighten it with a drawing 




 
