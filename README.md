# Prometheus Best Practices and Common Questions

This is a list of best practices I've found as I've learned more and more about Prometheus.

## Metric Creation

**Q: When measuing something, what units should I use? (eg, milliseconds or seconds?)**

Try to stick to the base units presented by Prometheus for better compatibility, in the case of time `seconds` is recommended.

> Prometheus does not have any units hard coded. For better compatibility, [base units](https://prometheus.io/docs/practices/naming/#base-units) should be used.

[Source](https://prometheus.io/docs/practices/naming/#base-units)

---

**Q: Should a metrics such as database read/writes be represented as separate metrics, or a single metric split by labels (ie `operation="read|write"`)?**

> Read/write and send/receive are best as separate metrics, rather than as a label. This is usually because you care about only one of them at a time, and it is easier to use them that way.  
>
> The rule of thumb is that one metric should make sense when summed or averaged. 

[Source](https://prometheus.io/docs/instrumenting/writing_exporters/#labels)

That said, the [Prometheus documentation](https://prometheus.io/docs/practices/naming/#labels) does say:

> Use labels to differentiate the characteristics of the thing that is being measured:
> 
> - `api_http_requests_total` - differentiate request types: `operation="create|update|delete`"  
> - `api_request_duration_seconds` - differentiate request stages: `stage="extract|transform|load`"

---

**Q: Are there common conventions for metric names?**

Yes, Prometheus has a [conventions page](https://prometheus.io/docs/practices/naming/#metric-names) that gives examples of metric names that you should follow, for instance:

> Metric should have a suffix describing the unit, in plural form.
> 
> Note that an accumulating count has total as a suffix, in addition to the unit if applicable.
> - `http_request_duration_seconds`  
> - `node_memory_usage_bytes`
> - `http_requests_total` (for a unit-less accumulating count)
> - `process_cpu_seconds_total` (for an accumulating count with unit)
> - `foobar_build_info` (for a pseudo-metric that provides metadata about the running binary)

[Source](https://prometheus.io/docs/practices/naming/#metric-names)

---

**Q: What kind of values or data can I use for my labels?**

Labels values are flexible, however it's important to ensure the the values are of a known size

> Label names may contain ASCII letters, numbers, as well as underscores. They must match the regex [a-zA-Z_][a-zA-Z0-9_]*. Label names beginning with __ are reserved for internal use.
>
> Label values may contain any Unicode characters.
> 
> A label with an empty label value is considered equivalent to a label that does not exist.

## Useful Links:

- https://prometheus.io/docs/instrumenting/writing_exporters/ (even though it's about writing exporters, a lot of it is relevant to implementing metrics)
- https://prometheus.io/docs/practices/naming/#metric-and-label-naming
