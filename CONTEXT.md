# CONTEXT.md

## Glossary

**Expression** — the full sequence of numbers and operators the user is building, shown in the top display line. Evaluated when user presses `=`.

**Current Input** — the number the user is actively typing, shown in the bottom display line. Replaces with result after `=`.

**Operator** — one of `+`, `-`, `*`, `/`. Binary, applied between two operands in the expression.

**Unary Op** — `√` (square root) or `+/-` (negate). Applied immediately to Current Input; no second operand needed.

**Percent** — `%` converts Current Input to a fraction of the preceding operand. `100 + 50%` evaluates as `100 + 50` (50% of 100). Not modulo.

**Error** — display state entered on: division by zero, `√` of negative number, numeric overflow. Clears on next digit or operator input.

**Evaluation** — triggered by `=`. Computes the full Expression, replaces Current Input with result, clears Expression line.

## Invariants

- Expression line always shows what has been committed (numbers + operators); Current Input shows what is being typed.
- After `=`, result becomes the seed for the next expression if user presses an operator.
- `+/-` and `√` act on Current Input only; they do not append to Expression.
- `%` acts on Current Input in context of the last operator in Expression.
