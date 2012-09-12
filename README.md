Deprecated
=======

This project is now deprecated. Please see Scoobi's userguide on using how to use sbt-assembly.


sbt-scoobi
============

*sbt-scoobi is an sbt plugin that allows you to build self contained jars ready to use with*


Version
------
0.0.1

How To Use
----------

Create a file at  `$PROJECT_ROOT/project/plugins.sbt`:

```scala
resolvers += "Sbt Scoobi" at "http://nicta.github.com/sbt-scoobi/repository/"

addSbtPlugin("com.nicta" %% "sbt-scoobi" % "0.0.1")
```

Now from sbt you will have a new `package-hadoop` task which will compile your project,
run your tests, and then pack your class files and all your dependencies into a
single JAR file: `target/scala_X.X.X/projectname-hadoop-X.X.X.jar`.

This jar is ready to send to haddop, using "hadoop jar projectname-hadoop-X.X.X.jar"

*Note*: There is currently an [undiagnosed issue](link-to-issue) in which there is an error finding "scala.math" from inside javassist. This appears to be a Mac specific issue, and a work around exists. Set *$HADOOP_CLASSPATH* to the name of the built jar, then run hadoop by passing in the name of the object with a `main` function to execute. e.g.

        # mac workaround
        $ export HADOOP_CLASSPATH=/path/to/WordCount-haddop-0.1.jar
        $ hadoop ExamplesMainObjectToRun

Other options
-------------

There are a few extra options you can use in your build.sbt, to:

* To change jar name:
 
        ScoobiKeys.jarName := "newName.jar"
 
* Don't run tests when building jar:

        ScoobiKeys.test := {}

* If sbt is unable to correctly detect the intended main function to execute when the jar is run, you can tell it (make sure the NameOfTheClass is fully qualified)

        mainClass := Some("NameOfTheClass")


License
-------

Copyright (c) 2010-2011 e.e d3si9n, Coda Hale

Published under The MIT License, see LICENSE
