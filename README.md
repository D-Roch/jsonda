# Jsonda - Simple DSL for JSON objects which is independent from specific JSON library

This project provides a Jsonda DSL, which can be used to construct JSON object
easily, in Scala.  The code size of Jsonda is small and it is easy to 
understand what it does.  Although Jsonda was formerly Jsonic, I was told that
there is already another Jsonic library in Java by @okapies san.  Then, I renamed
Jsonic to Jsonda.

# Using with sbt

If you woule like to use Jsonda with sbt, what you need to do is only
adding the following lines to your build.sbt.  There exists jsonda 0.6.0
for Scala 2.9.1 and Scala 2.9.2 and Scala 2.10.0.

```scala
libraryDependencies += "com.github.kmizu" %% "jsonda-json4s"  % "0.8.0"
```

or

```scala
libraryDependencies += "com.github.kmizu" %% "jsonda-lift"  % "0.8.0"
```

or

```scala
libraryDependencies += "com.github.kmizu" %% "jsonda-std"  % "0.8.0"
```

# For Developer

* By running sbt gen-idea, project definition files for IntelliJ IDEA is generated.
* By running sbt eclipse, project definition files for Scala IDE for Eclipse is generated.

# Syntax

Jsonda is very simple DSL for creating JSON objects.  Notations are followings:

* object: 

```scala```
    %{ $key1 :- $value1; $key2 :- $value2; ... }
```

or

```scala```
    %{ $key1 :- $value1
       $key2 :- $value2 }
```

Both have same meanings.

* array:

```scala```
    $($value1, $value2, ...)
```

or Traversable[JsonValueType] as the followings (new in jsonda 0.8.0):

```scala```
    Seq($value1, $value2, ...)
```

* primitive: 
  * number(Int):

```scala```
      100
      200
      300
```

  * number (Long)

```scala```
      1000000000000L
      2000000000000L
      3000000000000L
```

  * number(Float):
```scala``
      10.5F
      12.0F
```

  * number(Double):

```scala```
      10.5
      20.5
```

  * string (from Scala's BigInt):

```scala```
      BigInt("100000000000000000000")
      BigInt("2000000000000000000000000")
```

  * string (from Scala's BigDecimal):

```scala```
      BigDecimal("1.123456789")
      BigDecimal("2.234568978")
```

  * string:

```scala```
      "Hello, World!"
      "Hello, Scala!"
```

  * boolean:

```scala```
      true
      false
```

  * null:

```scala```
      JsonNull
```

  * Option[A]:
    If value of Option[A] is Some(a), a is implicitly converted.  None is regarded as null in JSON.

# Quick Start

Here are the way to create JSON using Jsonda (with jsonda-json4s):

```scala
import com.github.kmizu.jsonda.dsl.Json4sDSL._

val person = %{
  'name :- "Kota Mizushima"
  'age :- 29
}
```
    
The type of person is `org.json4s.native.JValue`.  If you are familiar with [json4s](https://github.com/json4s/json4s), 
you can easily manipulate JSON objects.  

Nested JSON can be written easily as the followings:

```scala
import com.github.kmizu.jsonda.dsl.Json4sDSL._
    
val config = % {
  'name :- "a config"
  'debug :- false
  'logging :- % {
    'level :- "warn"
    'verbose :- true
  }
  'optimization :- %{
    'agressive :- true
    'inline :- true
  }
}
```

Jsonda 0.8.0 supports not only json4s but also [lift-json](https://github.com/lift/lift/tree/master/framework/lift-base/lift-json/), and 
[scala.util.parsing.json](http://www.scala-lang.org/api/current/index.html#scala.util.parsing.json.package).  **Note that the return type
of `%` method depends on the underlying JSON library.**

* Jsonda with lift-json:

```scala
import com.github.kmizu.jsonda.dsl.LiftJsonDSL._
```

* Jsonda with `scala.util.parsing.json`:

```scala
import com.github.kmizu.jsonda.dsl.StdJsonDSL._
```

# Scaladoc

Scaladoc is available via the following links:

* [Scaladoc(0.8.0)](http://kmizu.github.com/jsonda/api/0.8.0)
* [Scaladoc(0.6.0)](http://kmizu.github.com/jsonda/api/0.6.0)
* [Scaladoc(0.4.0)](http://kmizu.github.com/jsonda/api/0.4.0)
* [Scaladoc(0.2.1)](http://kmizu.github.com/jsonda/api/0.2.1)
* [Scaladoc(0.2)](http://kmizu.github.com/jsonda/api/0.2)
* [Scaladoc(0.1)](http://kmizu.github.com/jsonda/api/0.1)
* [Scaladoc(0.0.2)](http://kmizu.github.com/jsonda/api/0.0.2/)

# License

This software is distributed under modified BSD License. See:
LICENSE.txt
