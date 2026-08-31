# OOKASupport

> 3LI Global — AIR Global integration estate. Generated 2026-08-31 by the US-Infrastructure audit. Facts below are drawn from this repo's code; anything not directly evidenced is marked _unverified_.

## Connected Resource
- **Azure resource:** none — static HTML/CSS/JS page (no `.github/workflows`, no Azure config in the repo)
- **Deploy trigger:** _unverified_ — no CI/CD workflow is committed; hosting is external to this repo
- **Talks to:**
  - **Zoho Forms** — the form `POST`s (multipart) to `https://forms.zohopublic.com/airglobal/form/OOKASupportForm/formperma/sUHkjiOZw8Ik7igJM--eGP7HLmpz-6whYbLbvSTedgk/htmlRecords/submit`, feeding the AIR Global (`airglobal`) Zoho tenant / Zoho CRM

## What It Does
A public "Send us a message" support/contact form for the OOKA brand. Visitors submit name, company, email and a message, and the entry is captured in AIR Global's Zoho Forms/CRM.

## Why It Exists
It is the customer-facing OOKA support intake, styled for embedding on an OOKA web property (Roboto web font, custom `css/form.css`) rather than served as a bare Zoho form. It is the **styled twin** of `OOKASupportForm` in this estate — both point at the identical Zoho form `formperma` (`OOKASupportForm` / `sUHkjiOZw8Ik...`); this repo is the presentation-polished version.

## How It Works
1. `index.html` (titled "OOKA Support Form", header "SEND US A MESSAGE") is a Zoho Forms HTML export; Zoho-generated field `name` attributes must be preserved or values submit empty.
2. `js/validation.js` provides `zf_ValidateAndSubmit()`, invoked on submit.
3. The browser `POST`s directly to the Zoho `formperma` submit URL; Zoho stores the record (and can relay to Zoho CRM per the form→CRM integration).
4. Hidden fields `zf_referrer_name`, `zf_redirect_url`, `zc_gad` are present but empty.
- **Operator note:** submit URL and field names are hard-wired to the Zoho form; edits to the form in Zoho require re-exporting the HTML. jQuery is loaded from the googleapis CDN.

---
_Environment:_ Production (single public form; no environment suffix in the repo — inferred)
_Runtime:_ static HTML/CSS/JS (jQuery via CDN; no server component)
