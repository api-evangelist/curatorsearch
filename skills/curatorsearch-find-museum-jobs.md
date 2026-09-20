---
name: find-museum-jobs
description: Search live museum, gallery and curatorial vacancies on CuratorSearch and pull one listing in full.
api: CuratorSearch API
generated: '2026-09-20'
method: generated
source: openapi/curatorsearch-openapi.json + mcp/curatorsearch-mcp.yml
operations:
  - searchJobs        # GET /api/jobs
  - getJob            # GET /api/jobs/{slug}
mcp_tools:
  - search_jobs
  - get_job
  - institution_jobs
---

# Find museum & curatorial jobs

Search the live CuratorSearch board and retrieve a single role in full. Keyless — send a descriptive
`User-Agent` header identifying your project. All operations are read-only.

## Steps

1. **Search the board.** Call `searchJobs` (`GET https://curatorsearch.com/api/jobs`) with any of:
   - `q` — free text matched against title, institution and location (e.g. `curator Berlin`).
   - `category` — one of: Leadership, Curatorial, Education & Public Programmes, Archives,
     Collections, Conservation, Intern & Fellowship, Open Call & Residency, Production, Other.
   - `region` — one of: North America, UK & Ireland, Europe, Asia-Pacific, Middle East,
     Latin America, Africa, International.
   - `limit` — 1 to 20 (max 20 results per call; the response `total` reveals how many matched beyond
     the returned slice).
2. **Read the results.** Each item is a `Job`: `title`, `institution`, `location`, `category`,
   `region`, `salary` (exactly as advertised, or `null`), `deadline`, `posted`, `url` (the permanent
   listing page) and `source` (the institution's original posting).
3. **Open one listing in full.** Take the slug from a `curatorsearch.com/opportunities/<slug>` URL and
   call `getJob` (`GET https://curatorsearch.com/api/jobs/{slug}`) to get the full `description`. A
   404 means the slug matches no listing.
4. **All open roles at one institution.** Over MCP, use `institution_jobs` with the institution name
   (e.g. `Philadelphia Museum of Art`); near-misses resolve. There is no dedicated REST equivalent —
   use a free-text `searchJobs` query by institution name over REST.

## Conventions & attribution

- No cursor/offset paging; the board surfaces newest matches within the 20-row cap.
- Link to the role's `url` rather than republishing the description text.
- Cite as "CuratorSearch, curatorsearch.com". See conventions/curatorsearch-conventions.yml.
