---
layout: post
title:  "Java Build Systems: ANT"
date:   2015-07-14 11:50
categories: java build system ant ivy
---

### About ANT

ANT is a java build system from apache. It's based on targets, which may or may not depend on other targets. 
A target is a set of commands ANT will perform. ANT provides huge variety of different commands you can use.
ANT is great for projects with very difficult build process which involves working with java files, non-java files and external tools.


### How does a Buildfile look?

```
<project>

    <target name="clean">
        <delete dir="build"/>
    </target>

    <target name="compile">
        <mkdir dir="build/classes"/>
        <javac srcdir="src" destdir="build/classes"/>
    </target>

    <target name="jar">
        <mkdir dir="build/jar"/>
        <jar destfile="build/jar/HelloWorld.jar" basedir="build/classes">
            <manifest>
                <attribute name="Main-Class" value="oata.HelloWorld"/>
            </manifest>
        </jar>
    </target>

    <target name="run">
        <java jar="build/jar/HelloWorld.jar" fork="true"/>
    </target>

</project>
```

### Beginner experience

It feels really weird to write a buildfile in XML, but I guess it allows for great portability (no endline issues etc).
ANT doesn't have any template which would only say "hey, this is a java project". 

### Intermediate experience

I found out other build systems support dependency management(e.g. they download necessary libraries). 
ANT doesn't directly support this, but you can install Ivy which handles it. I've installed Ivy to have this nice addition. 
I've been using ANT for some time to build bukkit plugins. My build files became more complex as they handle tasks like compiling more jars into one, deploying
to my test server, compiling plugin.yml and other resources into jar file etc. and also installing to local maven repository. <-- I'll explain that later, but I just wanted to mention it :)


So this is what a more complex build file looks like:
```
<project xmlns:ivy="antlib:org.apache.ivy.ant" name="ProperWeather" default="deploy_test_server">

	<!-- Global variables -->
	<property name="build" location="build" />
	<loadproperties srcfile="../testserver.properties" />
	<property name="sources.dir" location="src" />
	<property name="lib" location="lib" />
	<property name="version" value="1.1.8b" />
	<property name="jarname" value="properweather-${version}.jar" />

	<!-- These JARs will be compiled against. Here, you can put bukkit, other plugin JARs which user should install etc. -->
	<path id="compile_against.jars">
		<fileset dir="lib">
			<include name="*bukkit*.jar" />
			<include name="*junit*.jar" />
		</fileset>
	</path>

	<!-- These JARs will be compiled into your output JAR. You can use this for libraries which you have in separate projects etc. 
	If you put someone else's library here, you must make sure the license allows it.
	-->
	<zipfileset id="compile_into.jars" dir="${lib}">
		<include name="permsguru-*.jar" />
		<include name="autocommand-*.jar" />
	</zipfileset>

	<!-- Additional non-class files you want to include in your JAR file(plugin.yml, default config etc.) -->
	<path id="jar_include">
		<!-- Please don't remove plugin.yml :) -->
		<fileset dir=".">
			<include name="plugin.yml" />
			<include name="defconfig.yml" />
			<include name="en.txt" />
		</fileset>
	</path>

	<!-- You shouldn't need to modify the script below this line, everything is in variables... -->
	<target name="clean">
		<delete dir="${build}" />
	</target>


	<!-- All JARs that need to be compiled into the project will be re-packaged -->
	<target name="extractJars">
		<unzip dest="${build}/classes">
			<fileset refid="compile_into.jars" />
		</unzip>
	</target>

	<target name="compile" depends="clean,resolve,extractJars" description="--> compile the project">
		<mkdir dir="${build}/classes" />
		<javac srcdir="${sources.dir}" destdir="${build}/classes" classpathref="compile_against.jars" debug="on" />
	</target>

	<target name="copyInclude">
		<copy todir="${build}/classes">
			<path refid="jar_include" />
		</copy>
	</target>

	<target name="jar" depends="compile,copyInclude">
		<mkdir dir="${build}/jar/" />
		<jar destfile="${build}/jar/${jarname}" basedir="${build}/classes">
		</jar>
	</target>

	<target name="local_install" depends="jar">
		<ivy:publish status="integration" resolver="local" overwrite="true">
			<artifacts pattern="${build}/jar/[artifact]-${version}.jar" />
		</ivy:publish>
	</target>

	<target name="deploy_test_server" depends="local_install" description="--> deploy the plugin to test server">
		<copy file="${build}/jar/${jarname}" overwrite="yes" todir="${testServer.dir}/plugins" />
	</target>

	<target name="resolve" description="--> retrieve dependencies with ivy">
		<ivy:retrieve sync="true" />
	</target>
</project>
```

Besides, you also need ivy.xml, which is used by Ivy to handle dependencies. Ivy.xml is not very complex, it just gives basic information about the module we're building
and required libraries:

```
<?xml version="1.0" encoding="ISO-8859-1"?>

<ivy-module version="1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="http://ant.apache.org/ivy/schemas/ivy.xsd">
    <info
        organisation="sk.tomsik68"
        module="properweather"
        status="integration">
	</info>
	<publications>
		<artifact name="properweather" type="jar" ext="jar"></artifact>
	</publications>
	<dependencies>
		<dependency org="sk.tomsik68" name="permsguru" rev="latest.integration" />
		<dependency org="sk.tomsik68" name="autocommand" rev="latest.integration" />
		<dependency org="junit" name="junit" rev="4.11"/>
		<dependency org="org.bukkit" name="bukkit" rev="1.7.9-R0.2"/>
	</dependencies>
	
</ivy-module>
```

### IDE integration

ANT Integration in Eclipse which I used was insufficient, because it wasn't able to parse build errors from ANT output, 
so I had to add all the libraries manually to get correct error highlighting. Ivy Integration which I used was terrible. 
I had to refresh project every 5 seconds because it wasn't able to find its libraries. 
However, I'm glad I used ANT because automated deploying to test server really saved me some time and I was also happy with packaging which I previously handled with eclipse's Export > Jar file and I had to manually include all libraries and config files I needed.

### Sum-Up

To sum up, ANT is very verbose and complex build system. It doesn't have good IDE integration, but it offers very detailed control of build process. 
It doesn't provide any "default targets", but that's not an issue, because they're almost always the same, so I can copy that from old projects :)
Dependency management with Ivy was fine, because it downloaded all the libraries I needed. 
However, IDE integration of Ivy is terrible, so right now, ANT+Ivy is unsuitable for me. 

Thank you for reading :) 

My build system journey will continue (hopefully this week) with maven.
