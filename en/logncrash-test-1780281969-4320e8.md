## Log & Crash Report Test

This document is a short Korean sample to verify whether the translation pipeline properly sends logs to Log & Crash Search after job completion.

It validates whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, and `longDurationSec` reaches the collection server when a job finishes, rather than the quality of translation results.