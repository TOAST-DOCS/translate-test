## Log & Crash Reporting Test

This document is a short Korean sample to verify that the translation pipeline properly sends logs to Log & Crash Search after job completion.

It validates whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, `longDurationSec` reaches the collection server when a job finishes, rather than the quality of the translation results.