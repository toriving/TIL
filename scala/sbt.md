# sbt 

기본적으로 `project/src/main/scala/helloworld.scala` 가 존재

```scala
helloworld.scala

object helloworld {
  def main(args: Array[String]): Unit = {
    println("Hello, world!")
  }
}
```

## sbt package

build.sbt 를 아래와 같이 작성하자

```sbt
build.sbt


lazy val commonSettings = Seq(
  name := "untitled",
  version := "0.1",
  scalaVersion := "2.12.2"
)

lazy val app = (project in file(".")).
  settings(commonSettings: _*)
```

그 후 sbt package를 

```shell-script
$ sbt package

[info] welcome to sbt 1.4.2 (Oracle Corporation Java 1.8.0_241)
[info] loading global plugins from /Users/Danny/.sbt/1.0/plugins
[info] loading settings for project untitled-build from plugins.sbt ...
[info] loading project definition from /Users/Danny/workspace/untitled/project
[info] loading settings for project app from build.sbt ...
[info] set current project to untitled (in build file:/Users/Danny/workspace/untitled/)
[success] Total time: 0 s, completed Nov 11, 2020 12:22:47 AM

$ jar tf target/scala-2.12/untitled_2.12-0.1.jar 
META-INF/MANIFEST.MF
helloworld$.class
helloworld.class
```
jar 파일을 통해 프로젝트를 배포하는 데 도움이되는 sbt에 포함 된 매우 기본적인 sbt 명령

root 경로에서 `sbt package` 명령을 하면 `target/scala-2.12/{projectName_scalaVersion_projectVersion}.jar` 경로에 application 이 jar파일로 배포됨

내부에는 MANIFEST 파일과 class 파일이 존재함을 볼 수 있음

package 명령으로 생성 된 jar 파일에는 scala 라이브러리의 collection (예 : collection.mutable.Map.class)과 같은 스칼라 관련 라이브러리가 포함되지 않음.

따라서 생성 된 jar 파일에는 내가 구현 한 스칼라 소스에서 생성 된 최소 클래스 만 포함되어 있기 때문에 프로그램을 실행하려면 스칼라 라이브러리가 필요할 수 있음.


## sbt universal:packageBin

바이너리파일로 패키징 함

`project/project/plugins.sbt`에 다음을 추가해야함

`addSbtPlugin("com.typesafe.sbt" % "sbt-native-packager" % "1.3.3")`

또한 `build.sbt`에 다음을 추가해야함

`enablePlugins(JavaAppPackaging)`

```shell-script
$ sbt universal:packageBin
[info] welcome to sbt 1.4.2 (Oracle Corporation Java 1.8.0_241)
[info] loading global plugins from /Users/Danny/.sbt/1.0/plugins
[info] loading settings for project untitled-build from plugins.sbt ...
[info] loading project definition from /Users/Danny/workspace/untitled/project
[info] Updating 
...
[warn] There may be incompatibilities among your library dependencies; run 'evicted' to see detailed eviction warnings.
[info] loading settings for project app from build.sbt ...
[info] set current project to untitled (in build file:/Users/Danny/workspace/untitled/)
[info] Wrote /Users/Danny/workspace/untitled/target/scala-2.12/untitled_2.12-0.1.pom
[info] Main Scala API documentation to /Users/Danny/workspace/untitled/target/scala-2.12/api...
[info] compiling 1 Scala source to /Users/Danny/workspace/untitled/target/scala-2.12/classes ...
model contains 2 documentable templates
[info] Main Scala API documentation successful.
[success] Total time: 3 s, completed Nov 11, 2020 12:35:31 AM
```

패키징된 파일이 나오는 경로는 `./target/universal/{zip파일}` 이다


압축을 풀면 bin 폴더에 프로젝트명과 동일한 실행파일 (sh)과 .bat 파일이 나옴

```shell-script
$ jar tf target/universal/untitled-0.1.zip     
untitled-0.1/lib/untitled.untitled-0.1.jar
untitled-0.1/lib/org.scala-lang.scala-library-2.12.2.jar
untitled-0.1/bin/untitled
untitled-0.1/bin/untitled.bat
```

전체 프로젝트 (runnable class)는 jar로 말리고 실행파일을 통해 실행함


## sbt assembly

보통 하나의 Application을 개발하기 위해서는 상당히 많은 library를 사용하게 되는데 이를 배포하기 위해 사용된다.

사용된 library의 jar 파일과 classpath를 함께 제공 할 수 있음.


`project/project/plugins.sbt`에 다음을 추가해야함

`addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.5")`

```shell-script
$ sbt assembly
[info] welcome to sbt 1.4.2 (Oracle Corporation Java 1.8.0_241)
[info] loading global plugins from /Users/Danny/.sbt/1.0/plugins
[info] loading settings for project untitled-build from plugins.sbt ...
[info] loading project definition from /Users/Danny/workspace/untitled/project
[warn] There may be incompatibilities among your library dependencies; run 'evicted' to see detailed eviction warnings.
[info] loading settings for project app from build.sbt ...
[info] set current project to untitled (in build file:/Users/Danny/workspace/untitled/)
[info] Including: scala-library-2.12.2.jar
[info] Checking every *.class/*.jar file's SHA-1.
[info] Merging files...
[warn] Merging 'META-INF/MANIFEST.MF' with strategy 'discard'
[warn] Strategy 'discard' was applied to a file
[info] SHA-1: fd27d05cf21c9e6f1ddaddbc32
[success] Total time: 2 s, completed Nov 11, 2020 12:40:45 AM

$ jar tf target/scala-2.12/untitled-assembly-0.1.jar
...
scala/util/control/Exception$Catch$.class
scala/util/control/Exception$Catch.class
scala/util/control/Exception$Described.class
scala/util/control/Exception$Finally.class
scala/util/control/Exception.class
scala/util/control/NoStackTrace$.class
scala/util/control/NoStackTrace.class
scala/util/control/NonFatal$.class
```

이러한 assembly jar는 일명 fat jar라고도 불리며 application을 실행하는데 필요한 class와 jar를 모두 포함한다.

따라서 실행가능한 jar, Excutable jar라고도 불린다

```shell-script
$ java -jar target/scala-2.12/untitled-assembly-0.1.jar 
Hello, world!
```


### Reference

https://stackoverflow.com/questions/22556499/what-are-key-differences-between-sbt-pack-and-sbt-assembly  
https://rtfmplz.github.io/2017/05/30/scala-app-packaging  
https://gist.github.com/jungbin-kim/823e6d929d805823f265bb430d2b5e03  

