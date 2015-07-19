---
layout: post
title:  "Java Build Systems: Maven"
date:   2015-07-19 08:46
categories: java build system maven
---

### About Maven

Maven is a java build system which also has built-in dependency management and it also allows you to publish your modules really easily. It 
uses pom.xml to describe build process. Maven is also based around targets, but it doesn't expose them to pom.xml writer.

### How does a typical POM.xml look?

This example comes from maven's homepage:

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
     
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-app</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>jar</packaging>
     
      <name>Maven Quick Start Archetype</name>
      <url>http://maven.apache.org</url>
     
      <dependencies>
        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.8.2</version>
          <scope>test</scope>
        </dependency>
      </dependencies>
    </project>

### Beginner experience

I was happy with structure of POM.xml, as it's cleaner than ANT's structure. 
I was stunned by dependency management capabilities of maven. Majority of libraries you need can be found at http://mvnrepository.com/ . 
They also provide copy-paste pieces to paste to your pom.xml, so you don't need to worry about adding dependencies!

### Intermediate experience

Packaging abilities of ANT are missing, I want to include some files while not including others. Extracting dependencies into the JAR is 
also missing. I was happy to find out that missing features can be added by plugins, but structure of pom.xml gets worse in that case. See 
this example:
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

	<modelVersion>4.0.0</modelVersion>

	<groupId>sk.tomsik68</groupId>

	<artifactId>myLauncher</artifactId>

	<version>1.0.0 BETA</version>

	<build>

		<sourceDirectory>src</sourceDirectory>

		<resources>

			<resource>

				<directory>resources</directory>

			</resource>

		</resources>

		<plugins>

			<plugin>

				<artifactId>maven-compiler-plugin</artifactId>

				<version>3.1</version>

				<configuration>

					<source>1.8</source>

					<target>1.8</target>

				</configuration>

			</plugin>

			<!-- Setup the main class so we can run the JAR -->

			<plugin>

				<groupId>org.apache.maven.plugins</groupId>

				<artifactId>maven-jar-plugin</artifactId>

				<configuration>

					<archive>

						<manifest>

							<addClasspath>true</addClasspath>

							<mainClass>sk.tomsik68.myLauncher.launcher.Launcher</mainClass>

						</manifest>

					</archive>

				</configuration>

			</plugin>

			<!-- Copy all the dependencies into the JAR(this will produce another JAR) -->

			<plugin>

				<artifactId>maven-assembly-plugin</artifactId>

				<executions>

					<execution>

						<phase>package</phase>

						<goals>

							<goal>single</goal>

						</goals>

					</execution>

				</executions>

				<configuration>

					<descriptorRefs>

						<descriptorRef>jar-with-dependencies</descriptorRef>

					</descriptorRefs>

					<archive>

						<manifest>

							<addClasspath>true</addClasspath>

							<mainClass>sk.tomsik68.myLauncher.launcher.Launcher</mainClass>

						</manifest>

					</archive>

				</configuration>

			</plugin>

		</plugins>

	</build>

	<repositories>

    <repository>

      <id>sk_tomsik68</id>

      <name>Tomsik68's maven repository</name>

      <url>http://raw.githubusercontent.com/tomsik68/maven-repo/master/</url>

    </repository>

  </repositories>

	<dependencies>

		<dependency>

			<groupId>net.minidev</groupId>

			<artifactId>json-smart</artifactId>

			<version>1.1.1</version>

		</dependency>

		<dependency>

			<groupId>junit</groupId>

			<artifactId>junit</artifactId>

			<version>4.11</version>

		</dependency>

		<dependency>

			<groupId>com.flowpowered</groupId>

			<artifactId>flow-nbt</artifactId>

			<version>1.0.0</version>

		</dependency>

		<dependency>

			<groupId>sk.tomsik68</groupId>

			<artifactId>mclauncher-api</artifactId>

			<version>0.3</version>

		</dependency>

	</dependencies>

</project>
```


### IDE integration

Eclipse's integration is very poor. Sometimes the project changes back to non-maven project, forgets libraries or java version. However, 
IntelliJ has awesome integration with maven. It behaves just like normal project where you don't need to take care of build path. I 
switched to IntelliJ because the integration was so awesome ;)

### Sum-Up

Maven is great dependency management tool, which also provides advanced package abilities of ANT. These abilities, however, hide in 
additional plugins that need to be installed on some systems and pom.xml gets less readable over time. pom.xml is still too verbose(yeah, 
it's XML). It also doesn't give you control of targets, which could be useful in some cases. Maven is great for projects which haven't got 
specific requirements for packaging or creating a runnable jar file.

Thank you for reading :) 

My build system journey will end (probably next week) with gradle.
