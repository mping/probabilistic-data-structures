# Count Min Sketch

<img src="/img/min.jpg" />

----

## Whats it for?

Top-K frequencies/Heavy hitters

* How many times have you seen X? <!-- .element: class="fragment" -->
 * Leaderboards
 * Stats
 * Rate limiting, packet stats, etc

Note: it is associative

----

### How does it work?
#### It's a 2d array

<img src="/img/cms/count-min-sketch.png">

----

#### Adding

<img src="/img/cms/cms-working.gif">


----

#### Querying

<img src="/img/cms/cms-explained.jpg">

* Take the minimum

----

#### Parameters

* Number of hash functions
* Size of matrix

---

