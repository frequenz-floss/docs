# Experimental Packages

In Python, stable libraries might provide a `experimental` package. This package is used to host experiments or APIs that are considered unstable.

The goal is to allow developers to test new features or APIs, and to allow for rapid iteration and experimentation of new features, without affecting the stability of the main library or the non-breaking guarantees of the library as a whole.

## Experimental Package Guidelines

Experimental features, symbols and APIs follow these guidelines (using words like MUST, MAY, etc. with the meaning defined by [RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)):

* Breaking changes MUST NOT be introduced in minor releases, same as the main library code.
* Code MAY be unmaintained (reported issues MAY never be fixed).
* Code MAY have low quality.
* Additions or changes to `experimental` MAY NOT appear in release notes.
* Additions to `experimental` SHOULD have a low entry barrier.
* Unmaintained features and symbols (the ones that are already discarded as a candidate for the main library) MUST be deprecated as soon as they are considered inviable.
* Users SHOULD NOT use deprecated features or symbols.
* Experiments SHOULD create new symbols with the same name but adding a numeric suffix when breaking changes are needed, and MUST deprecate the previous iteration.
* Symbols SHOULD be copied to the main library and deprecated in `experimental` when they reach maturity.
* Deprecated symbols SHOULD be removed from `experimental` when a new major version is released.

Because of the above, it is likely that `experimental` packages could accumulate a lot of failed experiments (garbage).

## Examples

### Introducing breaking changes to a class or function

If we want to rename an argument for function `foo`:

```python
def foo(wrong_arg: int) -> None: ...
```

We can create a new function `foo1` with the new name and deprecate the old one:

```python
@deprecated("foo is deprecated, please use `foo1` instead")
def foo(wrong_arg: int) -> None: ...

def foo1(right_arg: float) -> None: ...
```
