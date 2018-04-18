# Scala_with_sbt
Summary of how to set_up Scala development  environment  without IDE on Linux.

1.Download sbt

sbt is a build tool for Scala, Java, and more. It requires Java 1.8 or later.

Install sbt on Linux:
>echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list

>sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823

>sudo apt-get update

>sudo apt-get install sbt

2.Create a project with sbt
cd to the directory where you want to create a scala project.
type "sbt" to start sbt
commands:
>show name		//show directory name
version		
organization	

>//all these things we set will write into build.sbt
>set name := "Your project name"	
         version := "1.0"			//Set the project version
         organization := "org.example"	
>//this is a reverse domain name that you own, typically one specific to your project. It is used as a namespace for projects.
         scalaVersion:=”2.11.8”
>session save
>exit

>//create src path to write scala file 
>mkdir -p src/main/scala
>touch src/main/scala/test.scala

write scala program in .scala file
define package in .scala file like:

//Unlike Java, in Scala, the file’s package name doesn’t have to match the directory name.
>package com.appliedscala.test

>object Main extends App {
    println("Hello, world")
}

import lib:type below in build.sbt file
>libraryDependencies += groupID % artifactID % revision 

e.g.
>libraryDependencies ++= Seq(

>"org.apache.spark" %% "spark-core" % "2.3.0", 

>"org.apache.spark" %% "spark-sql" %”2.3.0”,

>"org.scalanlp" %% "breeze" % "0.12",

>)

after program:
>sbt compile

>sbt run

>sbt package

2.Launching Scala Applications with spark-submit
>./bin/spark-submit \
--class <main-class> \
--master <master-url> \
--deploy-mode <deploy-mode> \
--conf <key>=<value> \
... # other options
<application-jar> \
[application-arguments]

Some of the commonly used options are:

--class: The entry point for your application (e.g. org.apache.spark.examples.SparkPi)

--master: The master URL for the cluster (e.g. spark://23.195.26.187:7077)

--deploy-mode: Whether to deploy your driver on the worker nodes (cluster) or locally as an external client (client) (default: client) 

--conf: Arbitrary Spark configuration property in key=value format. For values that contain spaces wrap “key=value” in quotes (as shown).

application-jar: Path to a bundled jar including your application and all dependencies. The URL must be globally visible inside of your cluster, for instance, an hdfs:// path or a file:// path that is present on all nodes.

application-arguments: Arguments passed to the main method of your main class, if any

Reference:

1.https://www.scala-sbt.org/

2.https://spark.apache.org/docs/latest/submitting-applications.html
