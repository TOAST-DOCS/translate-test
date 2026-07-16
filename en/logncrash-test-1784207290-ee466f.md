## Log & Crash Search reporting test

This document is a short Korean sample to confirm that the translation pipeline correctly sends logs to Log & Crash Search after a job completes.

This validates not the quality of the translation results, but whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, and `longDurationSec` reaches the collection server when the job completes.