## Log & Crash Reporting Test

This document is a short Korean sample to verify that the translation pipeline properly sends logs to Log & Crash Search after completing tasks.

It verifies not the quality of translation results, but whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, `longDurationSec` reaches the collection server when a job is completed.