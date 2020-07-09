#  type ascription

Variable Argument Function - varargs :_ * 관련하여 collection을 이용할 때 사용

```scala
def printReport(names: String*) {
  println(s"""Donut Report = ${names.mkString(" - ")}""")
}
// printReport(listDonuts) // 안됨
printReport(listDonuts: _*) // 됨
```

