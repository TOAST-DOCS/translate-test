## Log & Crash Reporting Test

This document is a short Korean sample to verify that the translation pipeline correctly sends logs to Log & Crash Search after job completion.

Rather than the quality of translation results, it validates whether a single-line log containing fields such as `jobId`, `sourcePrUrl`, `translationPrUrl`, and `longDurationSec` reached the collection server when the job completed.