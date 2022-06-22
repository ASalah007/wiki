# Optionals

to use Optionals effectively, use it with a method that produces 
alternative when the value is not present, or consumes the value only if it present

## consuming an Optional    

* `String s = optionalString.orElse("")` -> returns the string if it exists or "" if it doesn't
* `.orElseGet()`
* `.orElseThrow()`

* `optionalValue.ifPresent(v->process v)`
* `optionalValue.ifPresntOrElse(<consumer>, <function>)`
* `optionalValue.map(<function>) -> will return an op.`
* `OptionalValue.or(()->…);`
* `optionalValue.isPresent() -> boolean`

## creating an Optional

* `Optional.of(T t)`
* `Optional.ofNullable(obj) -> if you hava an object that might be null`
* `Optional.emtpy() `

if you have a function f() that returns an Optional of T and the object
of type T has a method g() that returns an `Optional<U>`<br>

normal function composition -> `U obj = f().g();` <br>

with optionals -> `Optional<U> obj = f().flatMap(T::g)` <br>

if we didn't use flat map and used map instead we would end up `with Optional<Optional<U>>`
use map whenever the function(g in this case) returns the obj not optional



