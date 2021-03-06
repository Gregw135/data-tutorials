---
title: Processing Trucking IoT Data with Apache Storm
tutorial-id: 800
platform: hdp-2.6.0
tags: [storm, trucking, iot, kafka]
---

# Deploying the Topology

## Introduction

Now that we know how to develop a Storm topology, let's go over how to package it up into a JAR file and deploy it onto a cluster.


## Outline

-   [Packaging a JAR](#packaging-a-jar)
-   [Deplying to Storm](#deploying-to-storm)
-   [Summary](#summary)


## Packaging a JAR

In a terminal, navigate to where the Storm project is located and run:
```
mvn package
```

This produces an **uber jar**, housing your topology and all of its dependencies.  The jar is saved to `/trucking-storm-topology-java/target/trucking-storm-topology-java-<version>-shaded.jar`.  This gets uploaded to the cluster for deployment to Storm.

> Note: Storm 1.1.0 enhances the way topologies are deployed, providing alternatives to using uber jars.  Check out the [Storm 1.1.0 release notes](https://storm.apache.org/2017/03/29/storm110-released.html#topology-deployment-enhancements) for more information.


## Deploying to Storm

> Note: If the jar from the previous section was built on your computer, you'll have to copy it onto your cluster before running the next command.

On your cluster, run the following command:
```
storm jar trucking-storm-topology-java/target/trucking-storm-topology-java-0.3.2-shaded.jar com.orendainx.hortonworks.storm.java.topologies.KafkaToKafka
```

`storm jar` will submit the jar to the cluster.  After uploading the jar, `storm jar` calls the main function of the class we specified (_com.orendainx.hortonworks.storm.java.topologies.KafkaToKafka_), which deploys the topology by way of the `StormSubmitter` class.


## Summary

Congratulations!  You now know about the role that Storm plays in a real-time data pipeline and how to create and deploy a topology from scratch.
