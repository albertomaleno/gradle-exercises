# Gradle exercises



Every task has a description and the command used to execute it. Some task may be executed in more than one way, so they're group together into '()' and separated using '||'



**1 -** Printing a message on console

 `gradle -q iWantToSayHello`

```groovy
task iWantToSayHello{
	println 'Hello then'
}
```



**2 -** Using the clausures DoFirst and DoLast to indicate that an action should go before another 

`gradle -q doingFirstAndThen`

```groovy
task doingFirstAndThen {
	doFirst {
		println 'This goes before'
	}
    doLast {
		println 'This goes after'
    }
}
```

**3 -** Creating a dynamic iteration on an internal task and mixing java variables with groovy

 `(gradle -q anIteration0 || gradle -q anIteration1 || gradle -q anIteration1)`

```groovy
3.times { i ->
	task "anIteration$i" {
		println i
	}
}
```





**4 -** Specifiying that a task runs after another, it creates a 'contract' between two task

`(gradle -q saludation || gradle -q todayDate)`

```groovy
task saludation {
	println 'HIII, today is:'
}

task todayDate {
	mustRunAfter {
		"saludation"
	}
	def date = new Date().format( 'yyyy-MM-dd' )
	println date
}
```



**5 -** Chaining tasks by creating dependencies between iterations and creating a group that runs all these chained tasks 

`gradle -q grouping`

```groovy
anIteration0.dependsOn saludation
anIteration2.dependsOn anIteration1, anIteration0
task grouping(dependsOn: anIteration2)
```



