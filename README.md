# inline-c

is a simple module for defining C code inside Carp code.

## Installation

```clojure
(load "https://veitheller.de/git/carpentry/inline-c@0.0.3")
```

## Usage

This module only provides one function, `inline-c` (it is a macro, actually
:shrug:). This function enables you to write C code inline as a string, to
express those things that are just kind of awkward in Carp (like complex
bit-twiddling) without having to include a helper every time.

```clojure
(load "https://veitheller.de/git/carpentry/inline-c@0.0.3")

(inline-c "int count_set_bits(int n) {
  int count = 0;
  while (n) {
    count += n & 1;
    n >>= 1;
  }
  return count;
}")
(register count-set-bits (Fn [Int] Int) "count_set_bits")

(defn main [] (println* &(count-set-bits 462)))
```

The function is safe to be called multiple times, but it’s better to not call
it at all if it’s avoidable. Inlining your C in Carp does not magically make it
safe, naturally.

<hr/>

Have fun!
