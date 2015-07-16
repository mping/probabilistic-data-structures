# Bloom Filters

<img src="/img/bloom.jpg" />

----

## Whats it for?

Membership tests

Does this SET contains a particular ELEMENT?

Note: it is associative, for same params

----

### False positives are POSSIBLE <!-- .element: class="fragment" -->
### False negatives NEVER happen <!-- .element: class="fragment" -->

An element is either MAYBE on the set, or IS NOT

----

### How does it work?

#### It's a bit set

<img src="/img/bloom/bloomfilter_empty.jpg">

----

#### Adding

Note that a very long string still occupies the same couple of bits.

<img src="/img/bloom/bloomfilter_adding.jpg">

Note: If you would use a Set[String], sizeof(set) === sizeof(unique elements)

----

#### Querying

<img src="/img/bloom/bloomfilter_querying.jpg">

----

### Parameters

* Bitfield size (m) <!-- .element: class="fragment" -->
* Number of hash functions (k) <!-- .element: class="fragment" -->
 * insertion and membership are O(k)

----

### Rules
* One byte per item in the input set gives about a 2% false positive rate <!-- .element: class="fragment" -->
 *  1024 elements to a 1KB Bloom Filter, about a 2% false positives
* The optimal number of hash functions is about 0.7 times the number of bits per item <!-- .element: class="fragment" -->
 * 3 at a 10% false positive rate
 * 13 at a 0.01% false positive rate
* The number of hashes dominates performance <!-- .element: class="fragment" -->

----

#### Cassandra

<img src="/img/bloom/bloomfilter_application.jpg">

----

## Diatribe: hashing

### Just use Murmur3


----

Fraction of keys hashed without collision (64 bits)
<img src="/img/hash/fraction_collision.png">

----

* V{n,i} = Number of items of namespace n hashed to the i-th bin
* Variance vs Mean for random distribution

<img src="/img/hash/vm_plot.png">

Note: each point is a "namespace". I have 251 namespaces, each of which has a variable number of 192 and 256 bit keys associated with it. All told I have in the neighborhood of 66 million datapoints of the form (namespace, key). Only the key portion of these tuples actually gets hashed, however

----

#### Black=50% flip-probability, bright green=output bit is “stuck” - doesn’t ever vary
<img src="/img/hash/avalanche_diagram.png">

Note: flip a bit, check if the output changes. Black indicates the desired 50% flip-probability, bright green indicates that the output bit is “stuck” - doesn’t ever vary as a result of flipping just that bit

---

