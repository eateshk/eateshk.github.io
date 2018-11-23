---
title = "Scala Setup"
date = "2018-11-23"
Xdescription = "Scala Setup on Ubuntu"
---

## Preparation

# Step 1 - Java Installation
Since scala runs on JVM we need java, it's a good idea to install whole of jdk with it. Issuing command below will bring both JRE and Java to your machine.

sudo apt-get install openjdk-8-jdk

# Step 2 - Download Scala
You can get scala from Scala website - Go to https://www.scala-lang.org/download/. Scroll down the page and get a debian package, with extension as .deb. You can click on it to download - or just use the command below.

wget <link to the .deb download>
Example - wget https://downloads.lightbend.com/scala/2.12.7/scala-2.12.7.deb

# Step 3 - Uncompress and Install Scala
Go to the directory where you've downloaded the .deb package and run below commmand
sudo dpkg -i <name of .deb file>

# Step 4 - Run Scala :)
Run scala by typing Scala, and it'll fire up a scala interpreter for you. You can then fiddle with Scala. Ctrl+C when you're done fiddling :)

# Step 5 - Installing Scala Build Tools (sbt)
Download SBT, link is again on the same page. Run the command below -
wget https://piccolo.link/sbt-1.2.6.tgz
tar -xvzf sbt-1.2.6.tgz
sudo mv sbt /usr/local/
sudo update-alternatives --install /usr/bin/sbt sbt /usr/local/sbt/bin/sbt 100

## SBT Working
1) it works on a particular project, run sbt where the project will reside. It'll download all the necessary libraries etc for the projet setup.
2) What is SBT ? - build tool like ant/maven/gradle required to compile,run, test and package your software. It's written in scala and is modern which makes it more convenient to use with Scala.
3) SBT uses Apache Ivy for dependency management.
4) SBT comes with REPL (Read-Eval-Print Loop). Helps in quick debugging and running Scala w/o setting up whole lot of context beforehand.
