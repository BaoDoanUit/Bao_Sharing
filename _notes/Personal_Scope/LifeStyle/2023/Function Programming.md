Functional programming is not about not having state. It about keeping the functions [referential transparency](http://en.wikipedia.org/wiki/Referential_transparency_%28computer_science%29) and without side effects. Usually this mean having no state, but that not has to be the case.  
Referential transparency mean that for a given input parameters the function will always return the same output.  
No having side effect mean that the function does not change the outer world, for example not changing some global parameter. This also mean that not calling the function wont effect other functions.

One example when there is a state but it still keep referential transparency and no side effects are caching.


```scala
class StatefullCache {
  val remoteRepository = ???
  var map: Map[String,Data] = Map()
  private def fetchFromRemote(id: String) = {
    val data = remoteRepository.get(id)
    map = map + (id -> data)
    data
  }
  def get(id: String) = map.getOrElse(id, fetchFromRemote(id))
}
```

This class have state but it referential transparency, since it always return the same result for any given id. It also does not has side effects (well... it has the memory growing, but that a limitation which does not effect the application flow).  
In practice no application is a "pure functional". printing to the screen, file & network I/O have all size effects (and get to to the extreme, even the CPU heat is a side effect). The idea in functional programming is to keep the side effect to the minimum and isolated. Some languages force you do that. Scala does not force it, but encourage you do so.

Depending on your use case calling 3rd party API/REST/whatever which isn't immutable or has side effect, may be count for practical uses by your application as functional or not. For example if any running of the application is "new world" where the data may be change the class above will work well (Since it will only access the external service once per id).

To summarize it, if you minimize the mutability and the side effect and keep it all in control then you can have the benefits for functional programming in the rest of the app.

