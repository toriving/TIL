# @

```scala
val o: Option[Int] = Some(2)

>> o: Option[Int] = Some(2)



o match {
  case Some(x) => println(x)
  case None =>
}

>> 2


o match {
  case x @ Some(_) => println(x)
  case None =>
}

>> some(2)


o match {
  case Some(_) => println(o)
  case None =>
}


>> some(2)


val d@(c@Some(a), Some(b)) = (Some(1), Some(2))

>> d: (Some[Int], Some[Int]) = (Some(1),Some(2))
>> c: Some[Int] = Some(1)
>> a: Int = 1
>> b: Int = 2

(Some(1), Some(2)) match { case d@(c@Some(a), Some(b)) => println(a, b, c, d) }

>> (1,2,Some(1),(Some(1),Some(2)))

for (x@Some(y) <- Seq(None, Some(1))) println(x, y)

>> (Some(1),1)

val List(x, xs @ _*) = List(1, 2, 3)

>> x: Int = 1
>> xs: Seq[Int] = List(2, 3)

```


[refer](https://stackoverflow.com/questions/2359014/scala-operator)
