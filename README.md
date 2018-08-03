Mate CI
===================

Mate is an open source CI tool that can make easier the software building, testing, deployment through automatization. It is docker contained itself aswell every action that Mate runs. 

Table of Contents
=================

  * [Why Mate](#why-mate)
  * [Installing Mate](#installing-mate)
  * [Matefile](#matefile)
    * [Triggers](#triggers)
    * [Chains](#chains)
    * [Actions](#actions)
    * [Example](#matefile-example)


## Why Mate
- Mate runs every action and itself in a docker container, making the process faster? and free of dependecies. 
- Mate follows 2 principles: 
  - Convention over configuration (Thats why you cant configure the workspace in some other directory)

### Installing Mate
The first thing we do is downloading the Mate repository

``` git clone www.github.com/mateci ```

Now we go to the mate folder and build the image 

```docker build -t mateci/mate .```

For a fast test we can fake a trigger, and run mate with this line: 

```docker run --rm -e MATE_TRIGGER=test -v $PWD:/work -v /var/run/docker.sock:/var/run/docker.sock -v env:/env mateci/mate```

But let's explain this more slow. 

``` -v $PWD:/work ``` The current folder will be shared with the /work folder in the docker container. This shows the Convention over configuration principle we believe. Also, the next action will be able to access the /work folder with the changes that the previous action did. 

``` -v /var/run/docker.sock:/var/run/docker.sock ``` We share the sockets 

``` -v env:/env mateci/mate ``` In /env we save all the environment variables that the next action will recieve, because actions cant communicate directly but yes like this. Let's enlighten it with a drawing


![alt text](https://github.com/fonyc/matest/blob/master/Untitled%20Diagram%20(2).png)



## Matefile
Matefiles are constructed with YAML. Also, they are composed by three key elements: Triggers, Chains and Actions. 

### Triggers
A trigger is a free string, defined by the launcher, that tells Mate which actions to run. An example trigger is ```github.push```, set by the github launcher when someone pushes to a repository.

### Chains
A chain is a sequence of actions inside a trigger. The actions inside a chain are executed sequentially, one after the other, if an action fails, the chain ends and the next one is executed. The first chain to run is always run and then after.

### Actions
Actions are the core of Mate. An action is always a docker container. Every action runs in a new docker container. Actions be a prebuilt docker image (from the docker registry, for example) or a docker image built from a dockerfile in the work directory.


### Matefile Example


```
  triggers:
   - trigger: test.build
     chains:
     - start:
       - build: Dockerfile
```









 
