# HyperLogLog

<img src="/img/hll.jpg" height="500" />

----

## Whats it for?

Cardinality Estimation

* How many distinct ITEMS are there today? and yesterday? and the two days?<!-- .element: class="fragment" -->
 * ex: unique visitors
* group-by/count without keeping all the data<!-- .element: class="fragment" -->

Note: it is associative

----

### How does it work?
#### It's complicated

<blockquote>
  ...The observation that the cardinality of a multiset of uniformly-distributed random numbers can be estimated by calculating the maximum number of leading zeros in the binary representation of each number in the set. 

  If the maximum number of leading zeros observed is n, an estimate for the number of distinct elements in the set is 2^n.
</blockquote>

----

<img src="/img/hll/wtf.jpg">

----

#### Real slow now

* In a random stream of integers
 * ~50% of the numbers (in binary) starts with "1"<!-- .element: class="fragment" -->
 * 25% starts with "01"<!-- .element: class="fragment" -->
 * 12,5% starts with "001"<!-- .element: class="fragment" -->

 If you observe a random stream and see a "001", there is a higher chance that this stream has a cardinality of 8.<!-- .element: class="fragment" -->

----

#### Bucketing

* number: 13,200,393
* hash: 2,005,620,294
* bits: [100010110101011001000110]

<pre>
                        100010110101011001 000110
                           ---------------|------
                           value            index
</pre>

* value: number of zeros +1 (rtl)<!-- .element: class="fragment" -->
* index:  The lowest b bits used to determine the index of the register whose value is to be updated. (m=2b)<!-- .element: class="fragment" -->
 * each bucket will serve as an "estimator"<!-- .element: class="fragment" -->

----

#### Estimating

* LogLog:
 * In order to compute the number of distinct values in the stream you would just take the average of all of the m buckets
 * <pre>distinct vals = constant * m * 2^(avg R)</pre>
* HyperLogLog uses<!-- .element: class="fragment" -->
 * large range correction (??) 
 * <i>Harmonic Mean </i> which tends to behave better for extreme values

----


## Harmonic Wut?

<img src="/img/hll/harm.jpg">

----

#### Example

http://content.research.neustar.biz/blog/hll.html


----

#### Unions/Intersections

<blockquote>
  How many distinct visitors we had in Monday AND Tuesday?
</blockquote>

* Are lossless (for same HLL size)
 * Some guys tried to combine different HLL with different sizes

----

#### Parameters

* number of buckets/registers
 * theoretical HLL error bounds (1.04 / sqrt(m))

----

#### This is HUGE

Who's using?

* Node, Java, C, etc etc
* Postgres
* Redis
* Twitter Algebird, Scalding
* Druid (MPP)
* Basically anyone who needs to count distinct/group-by 

---

