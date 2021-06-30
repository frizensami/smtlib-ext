# Node.js API for SMT-LIB 2.0

This is a fork of [Stanford Open Virtual Assistant Lab's Node.js SMT-LIB 2.0 library](https://github.com/stanford-oval/node-smtlib).

It adds new library calls to act as a utility library for [NUSMods](https://github.com/nusmodifications/nusmods), specifically a timetable optimizer.

SMT-LIB 2.0 is an interoperability format to communicate with
different SMT solvers, such as Z3.

The syntax of SMT-LIB is similar to Lisp:

```
(set-logic QF_ALL_SUPPORTED)
(declare-fun x () Bool)
(declare-fun y () Bool)
(assert (and (or x y) (not x) (not y))
(check-sat)
```

This package provides an high-level API to construct SMT-Lib
expressions, taking care of escaping. A simple example of its usage to assert a boolean condition is and get the SMT-LIB 2.0 string is:
```
const smt = require('smtlib');
let solver = new smt.BaseSolver('QF_ALL_SUPPORTED');
solver.add(smt.DeclareFun('x', [], 'Bool'))
solver.add(smt.DeclareFun('y', [], 'Bool'))
solver.assert(smt.And(smt.Or('x', 'y'), smt.Not('x'), smt.Not('y')));

// Retrieving an SMT-LIB 2.0 string to pass to Z3
let constraintStr = "";
solver.forEachStatement((stmt: string) => (constraintStr += stmt + '\n'));
```
