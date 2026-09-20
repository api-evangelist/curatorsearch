---
name: check-pay-transparency
description: Retrieve the live museum-sector pay-transparency figure and the full advertised-salary archive from CuratorSearch.
api: CuratorSearch API
generated: '2026-09-20'
method: generated
source: openapi/curatorsearch-openapi.json + mcp/curatorsearch-mcp.yml
operations:
  - salaryArchive     # GET /data/curatorial-salaries.json
mcp_tools:
  - salary_transparency
---

# Check museum pay transparency

Answer "what do museum/curatorial jobs pay?" and "how often is a salary disclosed?" from live,
citable data rather than an estimate. Read-only, keyless, CC BY 4.0.

## Steps

1. **Get the headline figure (live).** Over MCP, call `salary_transparency` (no arguments). It returns
   the current share of live postings that state a salary and the median advertised figure among
   those that do — computed fresh on every request, never cached stale. Prefer this over any older or
   estimated number.
2. **Pull the full archive.** Call `salaryArchive` (`GET https://curatorsearch.com/data/curatorial-salaries.json`)
   for every advertised salary the board has recorded since August 2026, exactly as published:
   currency, range, pay period (`per`), category, institution and location. Figures are never
   converted between currencies or inferred; German TV-L/TVöD grades are decoded into euro ranges.
   CSV is available at `/data/curatorial-salaries.csv`.
3. **Check the caveats.** Grade-mapping currently covers the German public sector only, so UK/US
   pay-transparency postings are not yet parsed — the true disclosure rate is likely higher than
   reported. See https://curatorsearch.com/salaries#methodology.

## Attribution

Cite as "CuratorSearch Curatorial Pay Archive, https://curatorsearch.com/salaries" with a date, or by
DOI 10.5281/zenodo.22544232 (always resolves to the newest snapshot). The method is written up as a
data note: DOI 10.5281/zenodo.22791747.
