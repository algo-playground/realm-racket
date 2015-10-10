<!-- toc -->

# Guess Game, Realm of Racket

> start: 2015-10-10
> [Realm of Racket], p30
> https://github.com/algo-playground/realm-racket/guess_game/guess_game.rkt
Convinced by my friend Yushi to start learning functional programming officially today. Just try to go out of my comfort zone a bit :alien:

For example, in Racket, functions are defined with `define`:

```lisp
(define (function-name argument-name ...)
	function-body-expression
	function-body-expression)
```

## Objective
It can be thought of a binary search. We have 3 modules: `guess`, `smaller`, and `bigger`:
* Determine or set the upper and lower limits of the player's number. 
* Guess a number halfway between those two numbers
* If the player says the number is smaller, lower the upper limit. 
* If the player says the number is bigger, raise the lower limit. 

## A function for guessing

```lisp
(define lower 1)
(define upper 100)

(define (guess)
	(quotient (+ lower upper) 2))
```

## Functions for closing in

```lisp
(define (smaller)
	(set! upper (max lower (sub1 (guess))))
	(guess))
```

A `set!` expression has the following shape:
```lisp
(set! variable expression)
```

The purpose of `set!`, pronounced "set bang", is to evaluate the `expression` and set the `variable` to the resulting value. 

```lisp
(define (bigger)
	(set! lower (min upper (add1 (guess))))
	(guess))
```

## The main function

```lisp
(define (start n m)
	(set! lower (min n m))
	(set! upper (max n m))
	(guess))
```

