# TDigest

<img src="/img/tdigest.png" />

----

## Whats it for?

Quantiles

* What's the 90% percentile for GET /my/service? and 99%? <!-- .element: class="fragment" -->
* anomaly detection: trigger at some percentile threshold <!-- .element: class="fragment" -->
* quantiles per metric per user/location/etc <!-- .element: class="fragment" -->
* Normally you need the full data set for a given quantile <!-- .element: class="fragment" -->
 * You cannot calculate a quantile of quantiles - makes it hard to do streaming

Note: As soon as you calculate a quantile, you cannot use that for re-calculating quantile with new data. Also t-digest is associative

----


### How does it work?
#### Sparse representation of the cumulative distribution function

* After ingesting data, the data structure has learned the "interesting" points of the CDF, called centroids<!-- .element: class="fragment" -->

----


### How does it work?
#### Some data

<img src="/img/tdigest/distrib.png">

----


### How does it work?
#### Empirical cdf

<img src="/img/tdigest/emp_cdf.png">

----


### How does it work?
#### "Interesting" points

<img src="/img/tdigest/cdf_interest.png">

----


#### Combining

* Create a new t-Digest and treat the internal centroids of the two left-hand side digests as incoming data
* The resulting t-Digest is a only slightly larger, but more accurate

<pre>
  tDigest1 + tDigest2 =  tDigest3
  -------------------    --------
  incoming data       => new tDigest
</pre>


----

#### Querying

<img src="/img/tdigest/pareto.gif">

* 8mb of pareto-distributed data into a t-Digest
* Resulting size was 5kb<!-- .element: class="fragment" -->
 * any percentile or quantile desired
 * accuracy was on the order of 0.002%. 


----

#### Parameters

* Compression
 * tradeoff of size vs accuracy
 * depends on the implementation, some expose more params than others
 * doesn't always mean the same thing

---

