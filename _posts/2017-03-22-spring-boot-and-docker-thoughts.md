---
layout: post
title:  "Spring Boot and Docker Thoughts"
date:   2017-03-22 14:57:00
categories: blog
comments: true
---

I recently tried the [Spring Boot with Docker](https://spring.io/guides/gs/spring-boot-docker/) tutorial and was very impressed.  I got through most of the guide until I hit a roadblock when trying to push the image created to the [Docker Hub](https://hub.docker.com/) registry.

It turns out that to push to Docker Hub you need to already have an account or be part of an organization.  Furthermore if you push to Docker Hub you will almost certainly have credentials.  If you go through the tutorial and get to the section where you push using the [Docker Maven Plugin](https://github.com/spotify/docker-maven-plugin) by Spotify and just change the Docker Image Prefix to your name you won't be able to push your code to the Hub.  Pushing from the command line worked for me because I was already authenticated.  Pushing using `mvn package docker:build -DpushImage` did not work however because I never gave Maven my credentials.

There are two things you need to do to be able to push to Docker Hub:
1. Store your credentials in your Maven settings.xml file
2. Make sure the Docker Plugin has access to said credentials

# Store your credentials in your Maven settings.xml file
You may or may not already have this in your directory.  Typically Maven puts it in `${user.home}/.m2/settings.xml` but may not exist as typically you have to create one from scratch.  See Maven's [Settings Reference](https://maven.apache.org/settings.html) for more detail.  If you already have one add the server tag and all child elements to your "servers" section.  Otherwise you can use the below snippet in it's entriety:
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>docker-hub</id>
            <username>username</username>
            <password>password</password>
            <configuration>
                <email>name@example.org</email>
            </configuration>
        </server>
    </servers>
</settings>
```

# Make sure the Docker Plugin has access to said credentials
In your POM you need to make sure that you insert the "serverId" in your configuration.  Use the same name that was the "id" in the previous step:
```xml
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>0.4.11</version>
    <configuration>
        <serverId>docker-hub</serverId>
        <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
        <dockerDirectory>src/main/docker</dockerDirectory>
        <resources>
            <resource>
                <targetPath>/</targetPath>
                <directory>${project.build.directory}</directory>
                <include>${project.build.finalName}.jar</include>
            </resource>
        </resources>
        <imageTags>
            <imageTag>${project.version}</imageTag>
            <imageTag>latest</imageTag>
        </imageTags>
    </configuration>
</plugin>
```
Per the documentation you don't need to specify a URL to the registry if you're using Docker Hub as it uses [https://index.docker.io/v1/](https://index.docker.io/v1/).  If you do add have a URL to a specific registry add a sibling element to `serverId`: `<registryUrl>https://index.docker.io/v1/</registryUrl>`.  Now running `mvn package docker:build -DpushImage` should work and you can continue with the rest of the guide!

I really like the Docker Maven Plugin.  It makes publishing a deployable and executable artifact a breeze. I've been using [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/) to develop a delivery pipeline and it seems that it would be very easy to incorporate this into it.