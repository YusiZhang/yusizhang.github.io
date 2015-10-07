---
layout: post
title: "Clojure Cheatsheet"
date: 2015-10-06 13:23:46 -0700
comments: true
categories: clojure
---

## Define Function

Write a function which returns a personalized greeting.
(= (__ "Dave") "Hello, Dave!")

[Hello World](https://www.4clojure.com/problem/16)

```
(fn [name] (str "Hello, ", name, "!"))
```
or

"#(str "Hello, " % "!")"

<!-- more -->

## Filter

```
(filter #(> % 5) '(3 4 5 6 7))
```
returns '(6 7)

## Local Bindings
Clojure lets you give local names to values using the special **let-form**.

Sample1
```
(let [x 5] (+ 2 x))
```
In Java something like:

```
int x = 5;
x + 2;
```

Sample2	
```
(let [x 3, y 10] (- y x))
```

In Java something like:
```
int x = 3, y = 10;
y - x;
```

## Recursion
A recursive function is a function which calls itself. This is one of the fundamental techniques used in functional programming.

```
(defn recursionFn [x]
  (when (> x 0)
    (conj (recursionFn (dec x)) x)))

=>(recursion 5)
=>[5 4 3 2 1]
```
## Rearranging Code "->" vs "->>"
These two lines are the same
```
(sort (rest (reverse [2 5 4 1 3 6])))

(-> [2 5 4 1 3 6] (reverse) (rest) (sort))
```

I like this explaination:

{% blockquote deddu https://clojuredocs.org/clojure.core/-%3E%3E#example-55416db5e4b01bb732af0a8c %}
;; let's compare thread first (->) and thread last ( ->> )
user=> (macroexpand '(-> 0 (+ 1) (+ 2) (+ 3)))
(+ (+ (+ 0 1) 2) 3)
user=> (macroexpand '(->> 0 (+ 1) (+ 2) (+ 3)))
(+ 3 (+ 2 (+ 1 0)))
{% endblockquote %}

## Loop and recur

(loop [bindings*] exprs*)

```
=>(loop [x 10]
	(when (> x 0)
		(if (> x 5)
			(print x)
			(print (* -1 x)))
		(recur (- x 1))))

=>-10-9-8-7-6-54321
```




