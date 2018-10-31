---
layout: post
title: "Setting up Jenkins and SonarQube for PHP"
date: 2018-10-29 16:04:45 +0800
categories: blog
author: Jerome
---

# Jenkins and SonarQube for a PHP Project

I've been doing my research about how to dockerize the Static Analysis tool SonarQube and apply it to a PHP project. 

Why: 1.) to know how vulnerable and unclean the codebase is. 2.) to act as a warning for new codes that are being committed to the repository. 
The goal is to minimize mess at the lowes level of the production line.

I followed (this link)[dockerize-jenkins-2]'s steps and tweaked it a bit for my case.

## Setting Up Jenkins on Docker

This is the first step. I used (this Jenkins image)[dockerhub-jenkins] specifically the `jenkins/jenkins:lts` version for this trial.

[dockerize-jenkins-2]: https://ifritltd.com/2017/07/06/dockerize-jenkins-2-setup-with-sonarqube-declarative-build-pipeline/
[dockerhub-jenkins]: https://hub.docker.com/r/jenkins/jenkins/
