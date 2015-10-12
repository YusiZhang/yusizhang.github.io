---
layout: post
title: "Introduction to Cursive, the Clojure IDE Built on IntelliJ"
date: 2015-10-07 16:14:02 -0700
comments: true
categories: [clojure, IDE, IntelliJ, Cursive]
---

## Agenda
1. [Install IntelliJ](#Install IntelliJ)
2. Install Cursive plug-in
3. IntelliJ basics
4. Create a demo project with clojure and java module
5. REPL
6. Jar Clojure module
7. Invoke and Debug clojure code in Java module 

<!-- more -->

## <a id="Install IntelliJ">Install IntelliJ</a>

You can download the IntelliJ [here](https://www.jetbrains.com/idea/download/index.html) Cursive plug in will work with IntelliJ with version 12.1, 13.1, 14.1 and the 15 EAP. All the following examples will be using version 14.1 in Mac OS X

## Install Cursive plug-in

Open "IntelliJ IDEA" --> "Preference" --> "Plugins" --> "Browse Repositories" --> "Manage Repositories"

{% img center /images/install-cursive-plugin.png %}

Add this repository url based on the IntelliJ version you are using. In this case it is
https://cursiveclojure.com/plugins-14.1.xml

You can see other repository urls for different versions [here](https://cursiveclojure.com/userguide/index.html)

After that, you can see "cursive-**" in the list. Install it and restart the IntelliJ.

## IntelliJ Baiscs

If you are coming from Eclipse, these tips may be helpful.

1. There is no "save" button in IntelliJ. You can check all your changes from the "Local History". It is like a VCS but it is only for personal use. To see your history changes, you can do shortcut "cmd + shift + a" to bring up the action window. And type in "local history", press enter.

2. There is no "workspace" in IntelliJ. What is called "project" in IntelliJ is like "workspace" in the Eclipse. "project" in Eclipse is like "module" in IntelliJ.

3. IntelliJ is not compiling your codes automatically. Unlike Eclipse, which do an auto-compilation when you push the save button. Since there is no "save" in IntelliJ, there won't be auto-compilation. Normally it will compile for you when you invoke "make", which happens before you run a test by default. Don't worry about that too much at this moment, you will get used to it pretty soon.

4. Change your dependencies in "Module Setting". Like setting the class path and lib in the Eclipse, dependencies settings are located at "Module Setting"(right click on the module)

## Create a Demo Project with Clojure and Java Module

I will create a project mixed by clojure module and java module. And I will show you how to do REPL and debug in the next two sections using this project.

* "IntelliJ IDEA"-->"File"-->"New"-->"Project" Then select Empty Project.

* Type in project name and location. And finish.

* Create a new clojure module within the project you just created. Choose type Leiningen on the left. Next. Click "Use snapshots". Finish. I name it "clojuredemo"

Leiningen is a management tool for clojure project/module.

* Create a new clojure namespace named "core" in clojuredemo module under src dir.

```plain
(ns clojuredemo.core)
(defn foo
  "I don't do a whole lot."
  [x]
  (println x "Hello, World!"))
```

* Create a new java module in the same project. I name it "java-demo". Include "Clojure(1.7.0)" in the "Additional Libraries and Frameworks".

* Create a new java class named "DemoJava" in the java-demo module under src dir.

If everything goes right, you should see something like this:

{% img center /images/modules.png %}

## REPL

For more information about REPL, please see this [page](http://www.braveclojure.com/getting-started/).

Right click the *clojuredemo* module and create a REPL for the current module. And select "Run nREPL with Leiningen". OK.

Run REPL. You should see a REPL window prompts to you. 

```
Starting nREPL server...
...
Connecting to local nREPL server...
Clojure 1.6.0
nREPL server started on port 49950 on host 127.0.0.1 - nrepl://127.0.0.1:49950
```

As you can see, you can load the file to the REPL or you can switch REPL NS to current file. Let's do switch REPL NS to current file. 

{% img center /images/REPL.png %}

Then you can type in `(foo "UC")` in the cmd line. The result `UC Hello, World!` will be shown in the REPL window. 

You can also do a short cut "cmd + shift + p" to execute individual forms.

[More about REPL in IntelliJ](https://cursiveclojure.com/userguide/repl.html).

## Jar Clojure module

If you create your clojure module using Leiningen, then you should see a project.clj file in the dir.

You should see something like this:

```
(defproject clojuredemo "0.1.0-SNAPSHOT"
  :description "FIXME: write description"
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.6.0"]]
  )
```

Adding these two line after the ":dependencies..."

```
 :jar-name "clojuredemo.jar"
 :jar-path "/target/clojuredemo.jar"
```

Open the terminal. cd to the clojuredemo dir. And execute this:

```
lein jar
```

If everything goes right, you can see the "clojuredemo.jar" in the /target folder.

## Invoke and Debug clojure code in Java module

In the java-demo module, add Jar dependency for clojuredemo.jar. And change your DemoJava.java file to this:

```Java
import clojure.java.api.Clojure;
import clojure.lang.IFn;

public class DemoJava {

    public void invokeMethod() {
        // Require clojuredemo.core
        IFn require = Clojure.var("clojure.core", "require");
        require.invoke(Clojure.read("clojuredemo.core"));
        // Invode foo method in core.clj
        IFn foo = Clojure.var("clojuredemo.core", "foo");
        foo.invoke("UC");

    }

    public static void main(String[] args) {
        DemoJava demo = new DemoJava();
        demo.invokeMethod();
    }
}
```
Remember to include "Leiningen: org.clojure/clojure:1.7.0" in the dependency.

Then you can run the DemoJava in IntelliJ. You should see `UC Hello, World!` in the console.

Now let's do debug.

Set a break point at the line `demo.invokeMethod()`. And run the debug. Try out step in and step out yourself, just like what you do in the Eclipse.

I am sure you will be amazed by it allows you step from java code to clojure code!

{% img center /images/debug1.png %}
{% img center /images/debug2.png %}

## Important link
[Cursive User Guide](https://cursiveclojure.com/)

[IntelliJ download](https://www.jetbrains.com/idea/download/index.html)

[Building, Running and the REPL](http://www.braveclojure.com/getting-started/)


