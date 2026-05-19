# Smart Safety Platform — Project Status

## Current Stack
- Single HTML file (React 18 + Babel + Supabase v2 via CDN)
- No build tools / no npm
- Hosted on Netlify (auto-deploy from GitHub `main`)
- Supabase (no RLS — custom auth with anon key)
- SHA-256 password hashing via Web Crypto API
- Session stored in localStorage under `loto_session`

## Supabase Tables
| Table | Purpose |
|-------|---------|
| `equipment` | Plant equipment registry |
| `locks` | Lock inventory and status |
| `personnel` | Users + roles + password hashes |
| `audit_log` | Every apply/remove action |
| `shift_config` | Shift start/end times |
| `audit_findings` | Finding lifecycle (Open→Closed) |
| `role_permissions` | Per-role feature permissions (JSONB) |

## Roles (12 total)
admin, hse, superintendent, auditor, ops_supervisor, operations,
mech_superintendent, mech_supervisor, mechanical,
elec_superintendent, elec_supervisor, electrical

## Plant Structure
- BOX_CONFIG: operations 8×8, mechanical 5×5, electrical 5×5
- MCC_ROOMS: 60K-A/B, 120K-A/B, UTIL with rack lists

---

## Completed Phases

### Phase 1 — Foundation ✅
- Login system + SHA-256 password hashing
- 12 roles with independent UX per role
- Equipment management (add, edit, decommission)
- Lock management (3 types: Ops / Mech / Elec)
- Visual boxes 8×8 and 5×5 with hooks board
- Personnel management

### Phase 2 — Full LOTO ✅
- Apply lock with permit + reason + expected time
- Remove lock with verification
- Photo upload on apply and remove (Supabase Storage, bucket: lock-photos)
- Box slot picker
- Full audit log
- Smart alerts (expected time + 24h + shift end)
- Smart List for Mech/Elec
- Search Equipment for all roles

### Phase 3 — Danger Tag & Reports ✅
- Print danger tag — 3 copies A4 landscape (5×10cm each)
- Shift Handover report (jsPDF)
- Equipment History log
- Overdue locks report
- Official printable PDF
- Plant Map — hierarchical 3 levels (Plant → MCC Room → Rack)

### Phase 4 — Auditor & Permissions ✅
- Auditor role with dedicated app
- Live Compliance Dashboard (no-permit, sequence violations, >24h)
- Full findings system (Open → In Progress → Resolved → Closed)
- Finding assignment to supervisors + tracking
- Permission system — Admin controls all roles
- 15 tab features + 7 action features × 3 levels (none/view/full)
- Permissions loaded from DB on login via PermsCtx React context

---

## Pending Phases

### Phase 5 — Work Operations 🔲
| Priority | Feature |
|----------|---------|
| 🔴 High | Work Permit (linked to LOTO) |
| 🔴 High | Incident Report + TRIR calculation |
| 🟡 Medium | Certification Card — quiz + digital certificate |
| 🟡 Medium | Periodic Inspections (fire extinguishers, pumps, alarms) |

### Phase 6 — Operational Intelligence 🔲
| Priority | Feature |
|----------|---------|
| 🟡 Medium | KPI Dashboard — TRIR / LTIR / Compliance % |
| 🟢 Later | Safety Walk — field observations |
| 🟢 Later | Employee Safety Score + leaderboard |
| 🟢 Later | Monthly visual reports — Trends + Charts |

---

## Project Stats
- ~3,621 lines of code
- 54 React components
- 7 Supabase tables
- 12 roles
- 22 controllable permissions
- Auto-deploy on Netlify from GitHub

## Future Vision
SaaS version (v2) — multi-tenant platform with onboarding wizard
that configures modules, roles, and KPIs per customer needs.
Target market: mid-size petrochemical and manufacturing plants
in Saudi Arabia and Gulf region (gap between enterprise systems
like SAP EHS/Cority and smaller companies with no solution).

## Development Branch
Always develop on: `claude/new-session-XXXXX`
Never push directly to `main` — merge via PR
