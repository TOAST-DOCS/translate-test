## Test Log & Crash reporting

This document is a short Korean-language sample to verify whether the translation pipeline correctly transmits logs to the Log & Crash Search service after completing work.

Rather than testing translation quality, it verifies whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, and `longDurationSec` reaches the collection server when the job completes.