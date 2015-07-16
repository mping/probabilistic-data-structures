# Probabilistic Data Structures

----

## Intro

What is a Probabilistic Data Structure


----

### Tradeoffs

* Trade **accuracy** for **speed** 
 * meaning: they do not give 100% accurate results <!-- .element: class="fragment" -->
* Have less space requirements, also called sublinear <!-- .element: class="fragment" -->
 * meaning: to count N distinct items, the required space is less than N <!-- .element: class="fragment" -->
* Bonus: are associative <!-- .element: class="fragment" -->

----

### Good enough

* A query may return a wrong answer <!-- .element: class="fragment" -->
 * But the answer is good enough (ex: count=1355, real count = 1299)
* Usually for BigData(tm) whatever that is <!-- .element: class="fragment" -->

---

