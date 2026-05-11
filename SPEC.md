# Spec: London Marathon 2026 Redirect Site

## 1. Objective

A minimal static site deployed on Netlify whose sole purpose is to redirect visitors to the new fundraising page on Route Raiser. The site replaces the previous London Marathon fundraising site and makes it clear to any visitor (or anyone who reads the source) that the content has permanently moved.

**Target users:** Anyone navigating to the old London Marathon fundraising URL via a saved link, search result, or bookmark.

**Destination:** `https://routeraiser.curtiscode.dev/page/curtis`

---

## 2. Core Features & Acceptance Criteria

| # | Feature | Acceptance criteria |
|---|---------|-------------------|
| 1 | Redirect via `<meta http-equiv="refresh">` | Browser is sent to the destination URL with zero delay |
| 2 | Redirect via JavaScript `window.location.replace()` | JS-capable browsers redirect before the page is rendered |
| 3 | Visible fallback link | A plain-text link to the destination is visible if both mechanisms fail |
| 4 | README | States the site has moved, includes the destination URL |

---

## 3. Project Structure

```
/
├── index.html          # Redirect page (meta refresh + JS + fallback link)
├── README.md           # Human-readable notice that the site has moved
└── SPEC.md             # This file
```

No build step, no package manager, no framework. All files are static and committed directly.

---

## 4. Code Style

- Pure HTML5, no CSS frameworks, no JavaScript libraries.
- `index.html` must be valid HTML5 (`<!DOCTYPE html>`).
- No inline styles beyond what is strictly necessary for the fallback link to be readable.
- No comments in the HTML beyond what aids comprehension of the redirect mechanism.

---

## 5. Deployment

- **Platform:** Netlify, connected to this GitHub repo.
- **Branch to deploy:** `main`
- **Publish directory:** `/` (repo root)
- **Custom domain:** to be configured in Netlify DNS settings by the user — not part of this repo.
- No `netlify.toml` or `_redirects` file required; the HTML-level redirect handles everything.

---

## 6. Testing Strategy

Manual only — no automated tests are warranted for a single-file redirect site.

| Check | How to verify |
|-------|--------------|
| Meta refresh fires | Open `index.html` in a browser with JS disabled; confirm redirect occurs |
| JS redirect fires | Open `index.html` with JS enabled; confirm instant redirect |
| Fallback link present | View page source; confirm `<a href="...">` link is present and correct |
| README accuracy | Read `README.md`; confirm URL matches destination |

---

## 7. Boundaries

**Always do:**
- Keep the destination URL (`https://routeraiser.curtiscode.dev/page/curtis`) consistent across `index.html` and `README.md`.
- Use a `0` second delay on the meta refresh (no countdown).
- Use `window.location.replace()` (not `assign()`) so the redirect does not add to browser history.

**Never do:**
- Add any tracking scripts, analytics, or third-party resources.
- Add any page content beyond the redirect mechanism and fallback link.
- Add a build system, package manager, or framework dependencies.
