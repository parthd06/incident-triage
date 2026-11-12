# Policy-Controlled Incident Runbook

Incident ID: parallel-small-001

Incident: search-api p95 latency above SLO: search-api p95 latency has crept from 410 ms to 690 ms over the last 2 hours (SLO 600 ms). Error rate is normal and searches still return results.

Severity: SEV3

Summary: search-api p95 latency degraded to 690 ms (exceeding the 600 ms SLO) due to deploy d-1039 reducing cache TTL from 600s to 60s, which dropped cache hit rates from 92% to 61% and quadrupled query load onto search-index.

Proposed action: Rollback deployment d-1039 to restore search result cache TTL back to 600s.

Rationale: Reverting cache TTL to the previous 600s setting will immediately increase cache hit rates and reduce search-index load, restoring latency within SLO with minimal risk to search correctness.

Model risk: low

Policy result: No high-risk policy rule matched.

Approval outcome: Not required by policy

Audit log:
- Router chose ['metrics', 'deploys']: search-api p95 latency degraded past the 600ms SLO over a 2-hour window while error rates remained normal. Metrics will reveal resource usage and latency breakdowns across search-api and search-index, while deploys will identify any recent rollouts or configuration adjustments causing the regression.
- Model combined 2 findings into one analysis.
- Policy check: No high-risk policy rule matched.
- Published runbook to runbooks/parallel-small-001.md.
