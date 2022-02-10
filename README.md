# Prometheus Best Practices and common questions

This is a list of best practices I've found as I've learned more and more about Prometheus.

## Metric Names

Q: Should a metrics such as database read/writes be represented as separate metrics, or a single metric split by labels (ie `operation="read|write"`)?

> Read/write and send/receive are best as separate metrics, rather than as a label. This is usually because you care about only one of them at a time, and it is easier to use them that way.

[Source](https://prometheus.io/docs/instrumenting/writing_exporters/#labels)


Useful Links:

- https://prometheus.io/docs/instrumenting/writing_exporters/ (even though it's about writing exporters, a lot of it is relevant to implementing metrics)
