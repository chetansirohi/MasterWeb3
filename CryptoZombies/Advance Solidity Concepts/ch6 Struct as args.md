You can pass a storage pointer to a struct as an argument to a private or internal function. This is useful, for example, for passing around our Zombie structs between functions.

```
function _doStuff(Zombie storage _zombie) internal {
  // do stuff with _zombie
}
```
