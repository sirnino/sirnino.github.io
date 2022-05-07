+++
date = 2022-05-07T16:05:21Z
description = ""
hero = "/uploads/default-hero.jpg"
title = "How to build a gitops pipeline"
[author]
avatar = "/uploads/default-avatar.jpg"
name = "Nino Sirchia"

+++
Nowadays many development teams use Kubernetes. 

Kubernetes, and all his "brothers" like Openshift, are very powerful tools to orchestrate the deployment of software; and if compared with a traditional IaaS approach - where the developer needed to access directly the server to update the docker image version somewhere in the filesystem - the advantage is remarkable and evident.

Nevertheless, it also has some disadvantages that is really important to know and be able to manage and prevent. Being aware of this, **I've alwasy seen Kubernetes like a nail gun**: it could be a very useful (in some case indispensable) tool, but at the condition that who uses it knows exactly what he's doing otherwise the risk is to get really hurt.

An example of this is the need for a proper management policy for the plethora of yaml files that are necessary to manage the resources deployed on Kubernetes. One of the activities that for sure they need to do most frequently is to manage manifest files needed to steer the software on the cluster for deployments, upgrades, deletion etc... In many cases two or more people could be working on the same yaml files (e.g. one guy for releasing a new version and another one for the fine-tuning of the resource requirements and scaling policies) so, as you could imagine, the proper coordination and conflicts management is a crucial point.

A developer has then two choices: the first one is to write down the yaml file 