#Run Spark Application

## Install Spark on a Lacal Machine
### Install on Machine
1. Install the latest version of Java Development Kit.
2. Install the latest version of Scala.
    ``` shell
    $ brew install scala
    ```
3. Download and unzip [Spark](https://spark.apache.org/downloads.html "Download Spark").
4. Try running Spark interactive shell, inside spark bin directory, by typing:
    ``` shell
    $ ./bin/spark-shell
    ```

## Run Spark Application
### Use sbt to create scala project
1. Create a project `$ sbt new sbt/scala-seed.g8`, and set your project name 'myapp'.
2. Write your scala application in  **src/main/myapp.scala**. Below is a example from 'Spark':
```
package org.apache.spark.examples

import scala.math.random

object LocalPi {
  def main(args: Array[String]) {
    var count = 0
    for (i <- 1 to 100000) {
      val x = random * 2 - 1
      val y = random * 2 - 1
      if (x*x + y*y <= 1) count += 1
    }
    println("Pi is roughly " + 4 * count / 100000.0)
  }
}
```
3. Compile and package your application code, first set your **build.sbt** file, then run `$ sbt compile`.
```
import Dependencies._

lazy val root = (project in file(".")).
  settings(
    inThisBuild(List(
      organization := "com",
      scalaVersion := "2.11.7",
      version      := "0.1.0-SNAPSHOT"
    )),
    name := "App Name",
    libraryDependencies += "org.apache.spark" %% "spark-core" % "2.1.0"
  )
```
**build.sbt** describes about the dependency of our project. After that, your project directory should be like this:
```
#### In you project directory
$ fird .
.
./build.sbt
./project
./project/build.properties
./project/Dependencies.scala
./src
./src/main
./src/main/scala
./src/main/scala/example
./src/main/scala/example/Hello.scala
./src/test
./src/test/scala
./src/test/scala/example
./src/test/scala/example/HelloSpec.scala
```
Here **example** and **hello** is my project, you can change to your project name.
Once that is in place, we can create a JAR package containing the application’s code.
```
# Inside your project directory:
$ sbt package
```

### Submit you application
