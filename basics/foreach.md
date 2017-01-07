# Foreach

{{#img-right}}dman-teacher-foreach.jpg{{/img-right}}

D features a `foreach` loop which allows
less error-prone and better readable iterations.

### Element iteration

Given an array `arr` of type `int[]` it is possible to
iterate through the elements using a `foreach` loop:

    foreach (e; arr) {
        // typeof(e) is int
        writeln(e);
    }

The first field in the `foreach` definition is the variable
name used in the loop iteration. Its type is induced automatically.
The second field must be an array - or a special iterable
object called a **range** which will be introduced in the next section.

### Access by reference

Elements will be copied from the array or range during iteration.
This is acceptable for basic types, but might be a problem for
large types. To prevent copying or to enable *in-place
*mutation, `ref` can be used:

    foreach (ref e; arr) {
        e = 10; // overwrite value
    }

### Iterate `n` times

D allows to write iterations which should be executed
`n` times, more concisely with the `..` syntax:

    foreach (i; 0..3) {
        write(i, ' ');
    }
    // 0 1 2

The last number in `a..b`` is excluded from the range,
thus the loop body is executed `3` times.

### Iteration with index counter

For arrays, it's also possible to access a separate index variable.

    foreach (i, e; [4, 5, 6]) {
        writeln(i, ":", e, ' ');
    }
    // 0:4 1:5 2:6

For [ranges](basics/ranges) which will be introduced in the next section
`enumerate` from [`std.range`](https://dlang.org/phobos/std_range.html) can
be used for a similar behavior.

### Reverse iteration with `foreach_reverse`

A collection can be iterated in reverse order with
`foreach_reverse`:

    foreach_reverse (e; [1, 2, 3]) {
        write(e, ' ');
    }
    // 3 2 1

### In-depth

- [`foreach` in _Programming in D_](http://ddili.org/ders/d.en/foreach.html)
- [`foreach` with Structs and Classes  _Programming in D_](http://ddili.org/ders/d.en/foreach_opapply.html)
- [`foreach` specification](https://dlang.org/spec/statement.html#ForeachStatement)

## {SourceCode}

```d
import std.stdio;

void main() {
    auto arr = [ [5, 15], // 20
          [2, 3, 2, 3], // 10
          [3, 6, 2, 9] ]; // 20

    // Iterate through array in reverse order
    import std.range: retro;
    foreach (row; retro(arr))
    {
        double accumulator = 0.0;
        foreach (c; row)
            accumulator += c;

        writeln("The average of ", row,
            " = ", accumulator / row.length);
    }
}
```
