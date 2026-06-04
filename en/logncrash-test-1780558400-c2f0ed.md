## Log & Crash Report Testing

This document is a short Korean sample to verify that the translation pipeline properly sends logs to Log & Crash Search after work completion.

It verifies not the quality of translation results, but whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, and `longDurationSec` reaches the collection server when the job is completed.