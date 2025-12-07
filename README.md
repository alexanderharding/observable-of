# @xan/observable-of

A utility function that creates an [`Observable`](https://jsr.io/@xan/observable/doc/~/Observable)
that emits a sequence of values in order on
[`subscribe`](https://jsr.io/@xan/observable/doc/~/Observable.subscribe) and then
[`returns`](https://jsr.io/@xan/observer/doc/~/Observer.return).

## Build

Automated by [JSR](https://jsr.io/).

## Publishing

Automated by `.github\workflows\publish.yml`.

## Running unit tests

Run `deno task test` or `deno task test:ci` to execute the unit tests via
[Deno](https://deno.land/).

## Example

```ts
import { of } from "@xan/observable-of";

const controller = new AbortController();

of(1, 2, 3).subscribe({
  signal: controller.signal,
  next: (value) => console.log(value),
  return: () => console.log("return"),
  throw: (value) => console.log("throw", value),
});

// console output:
// 1
// 2
// 3
// return
```

@example

```ts
import { of } from "@xan/observable-of";

let count = 0;
const controller = new AbortController();
controller.abort();

of(1, 2, 3).subscribe({
  signal: controller.signal,
  next(value) {
    if (value === 2) controller.abort();
    console.log(value);
  },
  return: () => console.log("return"),
  throw: (error) => console.error(error),
});

// console output:
// 1
// 2
```

# Glossary And Semantics

- [@xan/observable](https://jsr.io/@xan/observable#glossary-and-semantics)
