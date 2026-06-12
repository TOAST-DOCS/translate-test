## Log & Crash Reporting Test

This document is a short Korean sample to verify that the translation pipeline properly sends logs to Log & Crash Search after work completion.

It verifies not the quality of translation results, but whether a single line of logs containing fields like `jobId`, `sourcePrUrl`, `translationPrUrl`, `longDurationSec` reach the collection server when a job ends.