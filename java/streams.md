# Streams

## Streams creation

* you can turn any collection into stream by `collection.stream();`
* and any array by `Stream.of(arr)` or `Arrays.stream(arr, st, ed)`
* `Stream.empty()` -> will return an empty stream
* `Stream.generate( () -> "echo")` this will return a stream that will return the value returned from the given generator 
  every time it is asked for a value, it could result in infinite loop;
* `Stream.iterate(seed, predicate, unaryOperator)`
* `Stream.ofNullable(T t)` -> will return a stream of one element if non null or empty stream

## Stream Functions

* `stream.filter(predicate)`
* `stream.map(function)`
* `stream.flatMap(function)` -> if you have a stream of Streams
* `stream.limit(n)` -> returns a stream with the first n elements
* `stream.skip(n)` -> returns a stream with all the elements except the first n elements
* `stream.takewhile(predicate)`
* `stream.dropwhile(predicate)`
* `Stream.concat(stream1, stream2)`
* `stream.distinct()` 
* `stream.sorted(comparator)`
* `stream.peek(consumer)`

* `str.count()`
* `str.max() `
* `str.min()`
* `str.findFirst()`
* `str.findAny()`
* `str.anyMatch(<predicate>)`
* `str.allMatch(<predicate>)`
* `str.nonMatch(predicate)`



