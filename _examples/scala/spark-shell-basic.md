## Basic example

In this example, the spark-shell is used to show a simple usage of the `source{d} Engine`.

First, you can see how to import the package and instantiate and object that provide all the methods to manipulate the data retrieved from repositories.

The `engine` object is used to filter repositories by `id`, get the `HEAD` references from the repositories and look for the commits in that references which contain the word `Initial` in their messages. Then a table is showed selecting the columns `repository_id`, `hash` and `message`.

Launch spark-shell:
```sh
$ spark-shell --packages com.github.src-d:engine:master-SNAPSHOT --repositories https://jitpack.io
```

Code:
```scala
import tech.sourced.engine._

val engine = Engine(spark, "/path/to/siva-files")
engine.getRepositories.filter('id === "github.com/mingrammer/funmath.git").getReferences.filter('name === "refs/heads/HEAD").getCommits.filter('message.contains("Initial")).select('repository_id, 'hash, 'message).show

/* Output:
+--------------------+--------------------+--------------+
|       repository_id|                hash|       message|
+--------------------+--------------------+--------------+
|github.com/mingra...|aac052c42c501abf6...|Initial commit|
+--------------------+--------------------+--------------+
*/
```
