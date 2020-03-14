
 1. Mac OSX 10.5 or later
In Mac OSX 10.5 or later, Apple recommends to set the $JAVA_HOME variable to /usr/libexec/java_home, just export $JAVA_HOME in file ~/. bash_profile or ~/.profile.

```
$ vim .bash_profile 

export JAVA_HOME=$(/usr/libexec/java_home)

$ source .bash_profile

$ echo $JAVA_HOME
/Library/Java/JavaVirtualMachines/1.7.0.jdk/Contents/Home
```
Why /usr/libexec/java_home?
----------------------------
This java_home can return the Java version specified in Java Preferences for the current user. For examples,

/usr/libexec/java_home -V
Matching Java Virtual Machines (3):
    1.7.0_05, x86_64:	"Java SE 7"	/Library/Java/JavaVirtualMachines/1.7.0.jdk/Contents/Home
    1.6.0_41-b02-445, x86_64:	"Java SE 6"	/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
    1.6.0_41-b02-445, i386:	"Java SE 6"	/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home

This Mac OSX has three JDK installed.
```
##return top Java version
$ /usr/libexec/java_home
/Library/Java/JavaVirtualMachines/1.7.0.jdk/Contents/Home

## I want Java version 1.6
$ /usr/libexec/java_home -v 1.6
/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
```
[important java directories on macOSX]{https://developer.apple.com/library/archive/qa/qa1170/_index.html}

just set JAVA_HOME to the output of that command, which should give you the Java path specified in your Java preferences. Here's a snippet from my .bashrc file, which sets this variable:

export JAVA_HOME=$(/usr/libexec/java_home)
I haven't experienced any problems with that technique.

Occasionally I do have to change the value of JAVA_HOME to an earlier version of Java. For example, one program I'm maintaining requires 32-bit Java 5 on OS X, so when using that program, I set JAVA_HOME by running:

export JAVA_HOME=$(/usr/libexec/java_home -v 1.5)
For those of you who don't have java_home in your path add it like this.

sudo ln -s /System/Library/Frameworks/JavaVM.framework/Versions/Current/Commands/java_home /usr/libexec/java_home


install Maven
--------------
https://mkyong.com/maven/install-maven-on-mac-osx/?utm_source=mkyong.com&utm_medium=referral&utm_campaign=afterpost-related&utm_content=link4


create Maven project
--------------------
https://mkyong.com/maven/how-to-create-a-java-project-with-maven/




<!--project - the top level or root element of the POM.
modelVersion - POM model to use and it should be set to 4.0.0
groupId - project’s group id and normally, it is organization name which owns the project such as org.apache, org.springsource etc.,
artifactId - name of the project such as commons-lang, junit etc.,-->



three values form the project’s fully qualified artifact name and the fully qualified name of our simple maven project is 
com.xyz:simple-app:1.0.
```
simple.app/
    - pom.xml
    - src
        - main
            - java
                - com
                    - xyz
                        - App.java

```
Ellipsis
----------
AS we progress through Maven , the pom.xml will be lengthy, 
to shorten this we use ellipsis in the listing , to run these examples add the snippet between the ellipses to the existing pom.xml or other files at appropriate place.

BUILD PROJECT
-------------
run maven and complile the simple-app
maven downlods the core plugins during initial run, so internet connetion and execute maven from the top folder of the project where `pom.xml` exists ie from the simple-app folder

cd simple-app
mvn compile

```
simple.app/
|-- pom.xml
|-- src
|   - main
|       - java
|           - com
|               - xyz
|                   - App.java
|
|--target
    - classes
        - com
           - xyz
              - App.class
```

create a bunde directory called `target` in the top folder and compiled class files goes into it

on installaton of maven , it delegates the functionality such as test,compile,validate etc to plugins

1. on first run maven compile maven downloads the dependencies , maven downloads Apache Resources Plugin and Apache Compiler Plugin from central repo and stores in local repository and the uses the compiler plugin to compile the project.
    
Maven CLI- `mvn` command line reference of maven- used to build manage and also to interact with maven ,
everything in maven is done through mvn and is executed from top folder that contains pom.xml