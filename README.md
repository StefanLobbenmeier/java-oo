# Java Operator Overloading #

Java-OO is a modular extension (plugin) to Java compilers and IDEs
for ([Scala-like]) [Operator Overloading] support.
Works with standard JavaC compiler, [Netbeans IDE], [Eclipse IDE], [IntelliJ IDEA] IDE and any build tools.

Example (see other examples at [examples/](https://github.com/amelentev/java-oo/tree/master/javac-oo-mvndemo/src/) dir):

```java
import java.math.*;
import java.util.*;
public class Test {
  public static void main(String[] args) {
    BigInteger a = BigInteger.valueOf(1), // without OO
               b = 2, // with OO

    c1 = a.negate().add(b.multiply(b)).add(b.divide(a)), // without OO
    c2 = -a + b*b + b/a; // with OO

    if (c1.compareTo(c2)<0 || c1.compareTo(c2)>0) // without OO
      System.out.println("impossible");
    if (c1<c2 || c1>c2) // with OO
      System.out.println("impossible");

    HashMap<String, String> map = new HashMap<>();
    if (!map.containsKey("qwe")) map.put("qwe", map.get("asd")); // without OO
    if (map["qwe"]==null) map["qwe"] = map["asd"]; // with OO
  }
}
```

# Versions #

	JavaC/Netbeans: 0.5
	JavaC8:         0.5
	Eclipse:        0.5
	IntelliJ IDEA:  0.7

Note plugin versions are independent. If version for X > version for Y then it doesn't mean Y is behind feature wise.

# News #
16 Nov 2019. [IntelliJ IDEA](#IDEA) plugin v0.7 released with support of IDEA 2019.2+.

20 May 2017. [IntelliJ IDEA](#IDEA) plugin v0.6 released with support of IDEA 2017.

14 July 2016. As a workaround [Eclipse plugin](#Eclipse) works fine on Eclipse 4.4+ if you install [Scala IDE] plugin first.

2 Feb 2016. [IntelliJ IDEA](#IDEA) plugin v0.5 released with support of IDEA 15. Requires Java8 to run the plugin.

10 April 2015. [IntelliJ IDEA](#IDEA) plugin v0.4.1 released with support of IDEA 14.1.

27 January 2015. Eclipse-oo-plugin version 0.5 released with support of [reverse binary operator overload][operatorRev].

2 December 2014. New feature: [Reverse binary operator overload via `operatorRev` methods][operatorRev].<br/>
Plugin versions updated: <br/>
[JavaC7 & JavaC8](#javac): 0.5 <br/>
[IntelliJ IDEA](#IDEA): 0.4. Support of IDEA 14

31 May 2014. Javac8 plugin version 0.1.1 released. Removed runtime depencendy on nbjavac.

24 May 2014. [IntelliJ IDEA](#IDEA) plugin v0.3.1 released. Bugfixes for IDEA 13 Ultimate and for type resolution for binary expressions with primitives.

30 April 2014. [IJPLA] published a [paper] about Java-OO.

3 Feb 2014. New JavaC8 plugin version 0.1 for JDK8 was released.
It has the same features as JavaC plugin for JDK7 but doesn't work in Netbeans yet.

12 Jan 2014. JavaC plugin version 0.4 and Eclipse plugin version 0.4 released.
Now operator overloading perform autoboxing/autounboxing primitive to/from wrapper types where appropriate.
Fixed [javac plugin bug with index-set OO](https://github.com/amelentev/java-oo/issues/13).

3 Jan 2014. JavaC plugin version 0.3 released.
Fixed [#10 javac: binary operator adds erroneous cast on 1st operand](https://github.com/amelentev/java-oo/issues/10).

8 Sep 2013. Eclipse plugin version 0.3 released.
Removed copypasta from Eclipse Compiler. Plugin should be more steady agains compiler changes.

14 May 2013. [IntelliJ IDEA](#IDEA) IDE plugin v0.2.1 with IDEA Ultimate Edition support.

17 Apr 2013. [IntelliJ IDEA](#IDEA) IDE plugin v0.2.

26 Nov 2012. [Version 0.2] released. New feature: [Assignment operator overloading](https://github.com/amelentev/java-oo/issues/4) via static _#valueOf_ method.

# Installation #

<a name="javac" />

## javac, ant, etc ##
Just add to classpath: [javac8-oo-plugin.jar] for JDK8 or [javac-oo-plugin.jar] for JDK7.

```
javac -cp javac8-oo-plugin.jar <sources>
```

Demo at [examples/compile.sh](https://github.com/amelentev/java-oo/blob/master/javac-oo-mvndemo/src/compile.sh)

<a name='Eclipse' />

## [Eclipse IDE] update site ##
Click in menu: `Help - Install New Software`. Enter in `Work with` field:

	http://amelentev.github.io/eclipse.jdt-oo-site/

Tested on Eclipse Standard 4.3.2. Should work with older versions too. <br/>
To work on 4.4+ you need to install [Scala IDE] plugin (or similar plugin with Equanox weaving). You can find it in `Help -> Eclipse Marketplace`. This is workaround until normal solution will be found. Tested on 4.4 and 4.6.

## [Netbeans IDE] ##
1. Add [javac-oo-plugin.jar] as compile or processor library to Netbeans.
2. Enable "Annotation Processing in Editor": `Project Properties -> Build -> Compiling`.

Tested on 7.2.1

<a name="IDEA" />

## [IntelliJ IDEA] IDE ##
1. Install [Java Operator Overloading support](https://plugins.jetbrains.com/idea/plugin/7224-java-operator-overloading-support) plugin: `File -> Settings -> Plugins -> Browse repositories`. Mirror: [idea-oo-plugin.jar]) <br/>
For [Maven projects](#maven) installation is done. IDEA should setup everything according to pom.xml. <br/>
For other project types: <br/>
2. Add [javac8-oo-plugin.jar] as compile or processor library.
3. Enable Annotation Processing:
`Menu File -> Settings -> Compiler -> Annotation Processing -> Enable annotation processing`
4. Make sure you use `javac` compiler in `Settings -> Java Compiler -> Use compiler`. <br/>
Tested on IDEA 2019.2.4 Ultimate & Community editions. You can use earlier plugin versions for older IDEA releases.

### Android project in IDEA 12 ###
Add [javac-oo-plugin.jar] to `File - Settings - Compiler - Annotation Processors - Processor path`

### Android Studio (IDEA 13) / Gradle ###
add to `build.gradle`:

```
repositories {
	maven { url 'http://amelentev.github.io/mvnrepo/' }
}
dependencies {
	compile 'java-oo:javac-oo-plugin:0.5'
}
```

<a name="maven" />

## Maven ##
Look at [javac-oo-mvndemo/pom.xml](https://github.com/amelentev/java-oo/blob/master/javac-oo-mvndemo/pom.xml)

# Details #

Read the [paper] to learn more.
Supported operators (operator to method name map):

binary:

	| OPERATOR | METHOD NAME|
	-------------------------
	| +        | add        |
	| -        | subtract   |
	| *        | multiply   |
	| /        | divide     |
	| %        | remainder  |
	| &        | and        |
	| |        | or         |
	| ^        | xor        |
	| <<       | shiftLeft  |
	| >>       | shiftRight |

If left operand has no such method then the plugin will try to use ['reverse' method `<methodName>Rev`][operatorRev] on right operand.
So `2*a` will be transformed to `a.multiplyRev(2)` if `a` has such method.

unary:

	| -        | negate     |
	| ~        | not        |

comparison:

	| <, <=, >, >= | compareTo	| example: `a < b` <=> `a.compareTo(b)<0`
	`==` and `!=` are not overloadable because it will break things

index:

	| []  | get       | `v = lst[i]` <=> `v = lst.get(i)`
	| []= | set, put  | `map[s] = v` <=> `map.put(s,v)`,  `lst[i] = v` <=> `lst.set(i,v)`

assignment:

	| var = expr | var = VarClass.valueOf(expr) |

if `expr` is not assignable to `var` and `var` is an instance of `VarClass` and `expr` has type `ExprType` and there are static method `VarClass#valueOf(ExprType)` <br/>
then `var = expr` is transformed to `var = VarClass.valueOf(expr)`.
example: <br/>
`BigInteger a = 1` is transformed to `BigInteger a = BigInteger.valueOf(1)`

These methods exists in many java classes (example: BigInteger, BigDecimal) so you can
use operators on them "out of the box". Or you can add these methods to your classes to use OO (see [examples/Vector.java](https://github.com/amelentev/java-oo/blob/master/javac-oo-mvndemo/src//Vector.java)).


## Subprojects / Implementation details

- javac-oo-plugin
	- Plugin to JavaC 1.7 and [Netbeans IDE] for operator overloading. Based on [javac-oo].
	- Building via [maven] at top level: `cd java-oo; mvn clean install`. Or import maven settings in your IDE.

- eclipse-oo-plugin
	- [Eclipse IDE](JDT) plugin for OO support.
	- Patching Eclipse Java Compiler to allow OO.
	- Build in Eclipse with [PDE], [AJDT and Equanox Weaving] plugins. Run as Eclipse application with [equinox weaving enabled][equinox-weaving-launcher].

- idea-oo-plugin
	- [IntelliJ IDEA] IDE plugin for OO support.
	- Modify Java frontend in IDEA to allow OO. Need javac-oo-plugin to actually compile.
	- Build in IDEA. Run as IDEA plugin.

- by-products:
	- [javac-oo]
		- Patched version of JavaC 1.7 for Operator Overloading support. If you need standalone javac compiler with OO.
		- Build via ant or netbeans: http://openjdk.java.net/groups/compiler/README.html#build
	- [eclipse-oo]
		- Eclipse [Java Developer Tools] fork for Operator Overloading.
		- Use it if you need native [Eclipse IDE] support, or Eclipse Java Compiler support.
		- Build in Eclipse with [PDE]. Run as Eclipse application.

## Publications
["Java Modular Extension for Operator Overloading", IJPLA, April 2014.](https://github.com/amelentev/java-oo/raw/master/doc/ijpla.pdf)

[Scala-like]: http://www.slideshare.net/joeygibson/operator-overloading-in-scala-2923973
[javac-oo]: https://bitbucket.org/amelentev/javac-oo
[lombok]: http://projectlombok.org/
[lombok-oo]: https://github.com/amelentev/lombok-oo
[Eclipse IDE]: http://eclipse.org/
[Netbeans IDE]: http://www.netbeans.org/
[IntelliJ IDEA]: http://www.jetbrains.com/idea/
[Java Developer Tools]: http://eclipse.org/jdt/
[eclipse-oo]: https://github.com/amelentev/eclipse.jdt-oo
[Operator Overloading]: http://en.wikipedia.org/wiki/Operator_overloading
[AJDT and Equanox Weaving]: http://wiki.eclipse.org/Equinox_Weaving_QuickStart
[PDE]: http://www.eclipse.org/pde/
[maven]: https://maven.apache.org/

[javac-oo-plugin.jar]: http://amelentev.github.io/mvnrepo/java-oo/javac-oo-plugin/0.5/javac-oo-plugin-0.5.jar
[javac8-oo-plugin.jar]: http://amelentev.github.io/mvnrepo/java-oo/javac8-oo-plugin/0.5/javac8-oo-plugin-0.5.jar
[idea-oo-plugin.jar]: http://amelentev.github.io/mvnrepo/java-oo/idea-oo-plugin/idea-oo-plugin-0.7.jar
[IJPLA]: http://airccse.org/journal/ijpla/current2014.html#apr
[paper]: https://github.com/amelentev/java-oo/raw/master/doc/ijpla.pdf
[operatorRev]: https://github.com/amelentev/java-oo/issues/25
[equinox-weaving-launcher]: https://github.com/milessabin/equinox-weaving-launcher
[Scala IDE]: http://scala-ide.org/download/current.html
[Version 0.2]: https://github.com/amelentev/java-oo/issues?milestone=1&state=closed
