# Start
	
	$ rm slides.md; while inotifywait -e close_write slides/*; do cat slides/*.md > slides.md; done
	$ touch slides/*; reveal-md slides.md


# Related

* https://speakerdeck.com/bdarfler/probabilistic-data-structures

# References

* cardinality: https://www.npmjs.com/package/hll
 * https://github.com/aggregateknowledge/js-hll
 * http://content.research.neustar.biz/blog/venn.html
 * http://research.neustar.biz/2012/10/25/sketch-of-the-day-hyperloglog-cornerstone-of-a-big-data-infrastructure/
* quantile: https://github.com/welch/tdigest
 * http://dataorigami.net/blogs/napkin-folding/19055451-percentile-and-quantile-estimation-of-big-data-the-t-digest
* membership: https://www.jasondavies.com/bloomfilter/
* frequency: https://github.com/mikolalysenko/count-min-sketch


# Applications

* web analytics, data streaming
 * distinct visitors (hll)
 * advertising (hll per feature)
* real-time auditing/probing
 * ex: number of requests per ip (cm-sketch)
* bigdata processing
 * estimation (ex: presto) (hll)
* space-efficient optimizations
 * cassandra avoid costly IO lookups (bloom)

# PipelineDB
* http://docs.pipelinedb.com/
* https://github.com/armon/hlld


# Refs
* http://kellabyte.com/2013/01/24/using-a-bloom-filter-to-reduce-expensive-operations-like-disk-io/
* http://research.neustar.biz/2012/02/02/choosing-a-good-hash-function-part-3/
* http://dataorigami.net/blogs/napkin-folding/19055451-percentile-and-quantile-estimation-of-big-data-the-t-digest



# Code sample

## 
> mkdir -p /mnt/ram
> mount -t ramfs -o size=20m ramfs /mnt/ram