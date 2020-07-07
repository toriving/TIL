# Learning Scala - Chapter 9. 객체, 케이스 클래스, 트레이트

### [원본링크](https://www.notion.so/Learning-Scala-Chapter-9-e60971bf6d4441298ada7c253b2c4b70)

## 객체

객체(object)는 하나 이상의 인스턴스를 가질 수 없는 형태의 클래스로, 객체지향 설계에서는 싱글턴(singleton)이라 한다.

new 키워드로 생성하는 대신 이름으로 직접 해당 객체에 접근한다.

객체는 키워드 class 대신 object를 사용하여 정의

구문: 객체 정의하기

```scala
object <식별자> [extends <식별자>] [ {필드, 메소드, 클래스} ]
```

객체가 자동으로 인스턴스화 되는지 보여주는 예제

```scala
scala> object Hello { println("in Hello"); def hi = "hi"}
defined obejct Hello

scala> prinln(Hello.hi)
in Hello // 최초 접근하는 시점인 인스턴스화/초기화 시점에만 호출
hi

scala> prioln(Hello.hi)
hi
```

순수함수 (pure function) : 주어진 입력값으로만 계산하여 결괏값을 반환하는 함수 → 부작용이 없으며, 참조에 투명한 함수.

순수함수를 유틸리티로 제공하는 객체

```scala
scala> object HtmUtils {
				def removeMarkup(input: String) = {
					input
						.replaceAll("""</?\w[^>]*>""","")
						.replaceAll("<.*>"."")
					}
				}
defined object HtmlUtils

scala> val html = "<html><body><h1>Introduction</h1></body></html>"
html: String = <html><body><h1>Introduction</h1></body></html>

scala> val text = HtmlUtils.removeMarkup(html)
text: String = Introduction
```

### Apply 메소드와 동반 객체

클래스와 마찬가지로 객체에서도 하나 또는 그 이상의 apply() 메소드를 정의하여 호출 할 수 있다.

동반 객체 (companion object)는 클래스와 동일한 이름을 공유하며, 동일한 파일 내에서 그 클래스로 함께 정의되는 객체다.

동반 객체와 클래스가 접근 제어 관점에서는 하나의 단위로 간주되기 때문에 각각의 프라이빗(private) 그리고 프로텍티드(protected) 필드와 메소드에 서로 접근할 수 있다.

apply() 팩토리 패턴과 동반 객체 패턴을 동일 예제에서 사용해보자.

```scala
class Multiplier(val x: Int) { def product(y: Int) = x * y}
object Multiplier { def apply(x: Int) = new Multiplier(x) }

scala> val tripler = Multiplier(3)
tripler: Multiplier = Multiplier@5af28b27

scala> val result = tripler.product(13)
result: Int = 39
```

클래스 Multiplier는 product 메소드를 제공, 동반 객체는 매개변수를 가지는 'apply' 메소드를 가지고 있어 팩토리 메소드 역할을 한다.

클래스가 동반 객체의 private 구성원에 접근하는 새로운 예제를 보자.

```scala
object DBConnection {
  private val db_url = "jdbc://localhost"
  private val db_user = "franken"
  private val db_pass = "berry"

  def apply() = new DBConnection
}

class DBConnection {
  private val props = Map(
    "url" -> DBConnection.db_url,
    "user" -> DBConnection.db_user,
    "pass" -> DBConnection.db_pass
  )
  println(s"Created new connection for " + props("url"))
}

defined object DBConnection
defined class DBConnection

scala> val conn = DBConnection()
Created new connection for jdbc://localhost
conn: DBConnection = DBConnection@4d27d9d
```

객체 DBConnection에서 프라이빗 상수들을 동일 이름의 클래스에서 읽을 수 있다.

## 케이스 클래스

케이스 클래스(case class)는 자동으로 생성된 메소드 몇 가지를 포함하는 인스턴스 생성이 가능한 클래스다.

또한, 케이스 클래스는 자동으로 생성되는 동반 객체를 포함하는데, 이 동반 객체도 자신만의 자동으로 생성된 메소드를 가지고 있다.

케이스 클래스는 생성된 데이터 기반 메소드가 주어졌을 때 주로 데이터를 저장하는 데 사용되는 클래스인 데이터 전송 객체를 잘 지원한다.

구문: 케이스 클래스 정의하기

```scala
case class <식별자> ([var] <식별자>: <타입>[, ...])
										 [extends <식별자>(<입력 매개변수>)]
										 [{ 필드와 메소드}]
```

기본적으로 케이스 클래스는 매개변수를 값 필드로 전환하므로 val 키워드를 매개변수 앞에 붙일 필요는 없다.
만약 변수 필드가 필요하다면 var 키워드를 사용할 수 있다.

[생성된 케이스 클래스 메소드](Learning%20Scala%20Chapter%209%20e60971bf6d4441298ada7c253b2c4b70/Untitled%207410c47f98b84b6b88f5043c765684fa.csv)

케이스 클래스 예제

```scala
scala> case class Character(name: String, isThief: Boolean)
defined class Character

scala> val h = Character("Hadrian", true)                    (1) // 동반 객체의 팩토리 메소드인 Character.apply()
h: Character = Character(Hadrian,true)                       (2) // 생성된 toString 메소드는 인스턴스의 필드들을 깔끔하고 간단하게 표시한다.

scala> val r = h.copy(name = "Royce")                        (3) // copy 메소드로 첫번째 인스턴스와 다른 name을 가짐
r: Character = Character(Royce,true)

scala> h == r                                                (4) // 비교 연산
res0: Boolean = false

scala> h match {
     |   case Character(x, true) => s"$x is a thief"         (5) // unapply 메소드 적용 첫 번째 필드를 바인딩
     |   case Character(x, false) => s"$x is not a thief"
     | }
res1: String = Hadrian is a thief
```

## 트레이트

트레이트(trait)는 다중 상속을 가능하게 하는 클래스 유형 중 하나다.

클래스, 케이스 클래스, 객체, 그리고 트레이트는 모두 하나 이상의 클래스를 확장할 수 없지만, 동시에 여러 트레이트를 확장할 수는 있다.

그러나 다른 유형과 달리 트레이트는 인스턴스화될 수 없다.

구문: 트레이트 정의하기

```scala
trait <identifier> [extends <identifier>] [{ fields, methods, and classes }]
```

HtmlUtils 객체를 trait로 다시 구현

```scala
scala> trait HtmlUtils {
     |   def removeMarkup(input: String) = {
     |     input
     |       .replaceAll("""</?\w[^>]*>""","")
     |       .replaceAll("<.*>","")
     |   }
     | }
defined trait HtmlUtils

scala> class Page(val s: String) extends HtmlUtils {
     |   def asPlainText = removeMarkup(s)
     | }
defined class Page

scala> new Page("<html><body><h1>Introduction</h1></body></html>").asPlainText
res2: String = Introduction
```

with 키워드를 이용하여 두 번째 트레이트를 추가한다.

```scala
scala> trait SafeStringUtils {
     |
     |   // Returns a trimmed version of the string wrapped in an Option,
     |   // or None if the trimmed string is empty.
     |   def trimToNone(s: String): Option[String] = {
     |     Option(s) map(_.trim) filterNot(_.isEmpty)
     |   }
     | }
defined trait SafeStringUtils

scala> class Page(val s: String) extends SafeStringUtils with HtmlUtils {
     |   def asPlainText: String = {
     |     trimToNone(s) map removeMarkup getOrElse "n/a"
     |   }
     | }
defined class Page

scala> new Page("<html><body><h1>Introduction</h1></body></html>").asPlainText
res3: String = Introduction

scala> new Page("  ").asPlainText
res4: String = n/a

scala> new Page(null).asPlainText
res5: String = n/a
```

A가 클래스이고 B와 C가 트레이트인 class D extends A with B with C로 정의된 클래스는 컴파일러에 의해 class D extends C extends B extends A로 재구현 된다.

가장 오른쪽 트레이트는 정의된 클래스의 바로 위 부모이며, 클래스 또는 첫 번째 트레이트가 가장 나중의 부모 클래스가 된다.

```scala
scala> trait Base { override def toString = "Base" }
defined trait Base

scala> class A extends Base { override def toString = "A->" + super.toString }
defined class A

scala> trait B extends Base { override def toString = "B->" + super.toString }
defined trait B

scala> trait C extends Base { override def toString = "C->" + super.toString }
defined trait C

scala> class D extends A with B with C { override def toString = "D->" +
  super.toString }
defined class D

scala> new D()
res50: D = D->C->B->A->Base
```

부모 클래스의 행위를 재정의하기 위해 트레이트를 작성할 수 있다.

다음은 완전한 베이스 클래스에 서브클래스가 결합될 때 부가적 기능을 추가하는 트레이트를 더한 예제다.

```scala
scala> class RGBColor(val color: Int) { def hex = f"$color%06X" }
defined class RGBColor

scala> val green = new RGBColor(255 << 8).hex
green: String = 00FF00

scala> trait Opaque extends RGBColor { override def hex = s"${super.hex}FF" }
defined trait Opaque

scala> trait Sheer extends RGBColor { override def hex = s"${super.hex}33" }
defined trait Sheer
```

Opaque와 Sheer는 RGBColor 클래스를 확장한다.

이 새로운 트레이트를 사용하여 부모클래스와그 부모 클래스를 호가장한 트레이트 중 하나를 확장할 것이다.

```scala
scala> class Paint(color: Int) extends RGBColor(color) with Opaque
defined class Paint

scala> class Overlay(color: Int) extends RGBColor(color) with Sheer
defined class Overlay

scala> val red = new Paint(128 << 16).hex
red: String = 800000FF

scala> val blue = new Overlay(192).hex
blue: String = 0000C033
```

트레이트 선형화는 오른쪽부터 왼쪽의 순서를 가지기 때문에 'Paint'의 계층구조는 'Paint' → 'Opaque' → 'RGBColor'가 된다.

Paint 클래스에 추가된 클래스 매개변수는 RGBColor 클래스를 초기화하기 위해 사용되지만, Paint와 RGBColor 사이의 Opaque 트레이트는 부가적인 기능을 추가하기 위해ㅔ hex 메소드를 재정의한다.

### 셀프 타입

셀프 타입(self type)은 트레이트 애너테이션으로 그 트레이트가 클래스에 추가될 때 특정 타입 또는그 서브타입과 함께 사용되어야 함을 분명히 한다.

셀프 타입을 가지는 트레이트는 지정된 타입을 확장하지 않는 클래스에 추가될 수 없다.

셀프 타입의 보편적인 용도는 입력 매개변수가 필요한 클래스에 트레이트로 기능을 추가하는 것이다.

셀프 타입은 트레이트 정의의 중괄호를 연 바로 다음에 추가되며, 식별자, 요청받은 타입, 그리고 화살표(⇒)를 포함한다.

구문: 셀프 타입 정의하기

```scala
trait ..... { <identifier>: <type> => .... }
```

표준 식별자 'self' 대신 다른 식별자를 사용할 수도 있다. (키워드 제외)

```scala
scala> class A { def hi = "hi" }
defined class A

scala> trait B { self: A =>                                              (1) // 셀프타입을 가지며 A 클래스의 서브타입에만 함께 사용할 것을 요구
     |   override def toString = "B: " + hi
     | }
defined trait B

scala> class C extends B
<console>:9: error: illegal inheritance;                                 (2) // 안됨
 self-type C does not conform to B's selftype B with A
       class C extends B
                       ^

scala> class C extends A with B                                          (3) // 됨
defined class C

scala> new C()
res1: C = B: hi                                                          (4) // A 메소드 사용가능
```

셀프 타입의 이점을 보여주는 예제를 작성해보자.

우리는 매개변수를 필요로 하는 클래스를 정의하고, 그 클래스를 확장하기 위해서만 사용되어야 하는 트레이트를 생성할 것이다.

```scala
scala> class TestSuite(suiteName: String) { def start() {} }                (1) // 매개변수를 갖는 기본 클래스
defined class TestSuite

scala> trait RandomSeeded { self: TestSuite =>                              (2) // TestSuite.start()를 호출해야하는데 TestSuite가 입력 매개변수를 하드코딩을 요구해서 확장할 수 없다.
     |   def randomStart() {
     |     util.Random.setSeed(System.currentTimeMillis)
     |     self.start()
     |   }
     | }
defined trait RandomSeeded

scala> class IdSpec extends TestSuite("ID Tests") with RandomSeeded {       (3) IdSpec은 셀프 타입을 가진 트레이트를 서브클래스로 정의하여 random Start()가 호출할 수 있게 한다.
     |   def testId() { println(util.Random.nextInt != 1) }
     |   override def start() { testId() }
     |
     |   println("Starting...")
     |   randomStart()
     | }
defined class IdSpec
```