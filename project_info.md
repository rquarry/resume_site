# Project Context: Resume Site

## Purpose

This repository is Ryan T. Quarry's public professional resume website. Its primary audience is recruiters, hiring managers, professional contacts, and others evaluating Ryan's cybersecurity leadership background.

The project currently has three related goals:

1. Present a concise, responsive professional profile centered on cybersecurity operations, technical leadership, U.S. Coast Guard experience, education, certifications, and core competencies.
2. Provide a small capture-the-flag (CTF) challenge through clues embedded in the page, repository history, and image assets.
3. Serve as a simple learning project for deploying a framework-free website with Microsoft Azure Static Web Apps and GitHub Actions.

The site is based on the MIT-licensed Start Bootstrap Resume template and has been customized with Ryan's content, profile image, metadata, and CTF section.

## Current User Experience

The application is a single-page resume with a fixed sidebar on desktop and a collapsible top navigation bar on smaller screens. Navigation links scroll to these sections:

- About
- Experience
- Education
- Skills
- Interests
- CTF

The page includes LinkedIn and GitHub links, a profile photo, a TryHackMe badge, and JSON-LD structured data describing the page owner, experience domain, education, credentials, and repository.

## Technology Stack

### Core

- HTML5: all page structure, resume content, metadata, and JSON-LD are in `index.html`.
- CSS/SCSS: custom styles originate in `scss/` and compiled files are committed under `css/`.
- JavaScript: a small jQuery script provides smooth anchor scrolling, mobile-menu closing, and Bootstrap ScrollSpy behavior.
- No frontend framework, backend, database, API, authentication, or server-side rendering is present.

### Libraries and Assets

- Start Bootstrap Resume template v5.0.2.
- Bootstrap v4.1.3, vendored in `vendor/bootstrap/`.
- jQuery v3.3.1, vendored in `vendor/jquery/`.
- jQuery Easing, vendored in `vendor/jquery-easing/`.
- Font Awesome Free v5.3.1, vendored in `vendor/fontawesome-free/`.
- Google Fonts loaded at runtime: Muli and Saira Extra Condensed.
- TryHackMe badge loaded from an external script in the Skills section.
- JPEG profile/history images stored in `img/`.

The repository has no root `package.json`, lockfile, build script, test runner, formatter configuration, or lint configuration. Dependencies are checked into source control and the deployed site can be served directly from the repository root.

## Architecture and Important Files

- `index.html`: the entire production page, resume content, SEO metadata, schema.org JSON-LD, navigation, external integrations, and CTF clues.
- `scss/resume.scss`: SCSS entry point that imports the partials below.
- `scss/_variables.scss`: Bootstrap-like colors and the fixed desktop sidebar width. The primary accent is `#BD5D38`.
- `scss/_mixins.scss`: body and heading font stacks.
- `scss/_global.scss`: typography, responsive body spacing, social icons, and general visual rules.
- `scss/_nav.scss`: fixed/collapsible navigation and profile-image styling.
- `scss/_resume-item.scss`: section sizing and date-column behavior.
- `scss/_bootstrap-overrides.scss`: primary color and link overrides.
- `css/resume.css`: readable compiled production CSS referenced by `index.html`.
- `css/resume.min.css`: minified CSS artifact; currently committed but not referenced by `index.html`.
- `js/resume.js`: readable JavaScript source.
- `js/resume.min.js`: minified production JavaScript referenced by `index.html`.
- `img/IMG_2255-3.jpg`: current displayed profile photo.
- `img/profile.jpg`: older image retained as part of the repository history/CTF trail.
- `resume/`: local resume research and document variants. This directory is now ignored by Git and should be treated as working/source material rather than deployed site content.
- `README.md`: brief deployment notes and upstream-template attribution.
- `.github/workflows/azure-static-web-apps-red-desert-0a84e060f.yml`: Azure deployment workflow.
- `LICENSE`: MIT license inherited from the original template.

## Content Sources and Synchronization

Resume information exists in more than one form:

- `index.html` is the current source of truth for what visitors see.
- `resume/resume.md` is the source of truth for updates to `index.html`. This file should be checked during each agent run. Do not make edits to the html page without permission. 
- `resume/Job Data for Resume.md` contains extensive career source material and accomplishment details that are summarized in `resume.md`
- Multiple DOCX files and one PDF in `resume/` represent additional resume variants.

Future changes must not assume these sources are synchronized. When updating professional facts, compare the relevant sources, preserve precise metrics and dates, and ask for confirmation when they disagree. Avoid silently replacing concise web copy with all available source material; the website is meant to remain scannable.

The JSON-LD block in `index.html` duplicates several visible facts. Any change to the name, summary, current role, contact details, profile image, expertise, education, certifications, or repository URL should update both visible content and structured metadata as applicable.

## Styling and Interaction Conventions

- Preserve the one-page anchored-section model unless a broader redesign is explicitly requested.
- Maintain responsive behavior at Bootstrap's existing breakpoints, especially the fixed 17rem sidebar at widths of 992px and above.
- Use Bootstrap 4 utility and layout conventions when making small changes to the current implementation.
- Keep source and generated assets aligned: edit `scss/` and regenerate `css/resume.css`/`css/resume.min.css`; edit `js/resume.js` and regenerate `js/resume.min.js`.
- Do not edit vendored dependencies for application-specific behavior.
- Preserve the current professional, restrained visual tone and keep the resume easy to scan.
- Retain semantic headings, meaningful link labels, keyboard accessibility, mobile usability, and sufficient color contrast.

## CTF Behavior

The CTF section is intentional, not placeholder copy. It asks visitors to discover:

- The GitHub repository associated with the site.
- The city shown in the original profile image.

Relevant clues include an encoded HTML comment near the end of `index.html`, repository/image history, and the retained older image. Future cleanup, metadata changes, image replacement, history rewriting, or removal of apparently unused assets can break the challenge. Preserve these clues unless the user explicitly asks to revise or remove the CTF.

Do not publish the solutions directly in normal page copy or in future AI context files.

## Deployment

GitHub Actions deploys the site to Azure Static Web Apps on pushes and pull requests targeting the `html` branch.

Deployment settings:

- App location: `/`
- API location: empty
- Output location: `.`
- Build preset: effectively custom/no application build
- Azure deploy action: `Azure/static-web-apps-deploy@v1`
- Required secret: `AZURE_STATIC_WEB_APPS_API_TOKEN_RED_DESERT_0A84E060F`

The workflow also closes the Azure preview environment when a pull request is closed. The active Git branch at the time this document was created was `html`.

## Validation Guidance

There is no automated test suite. For future changes, validation should be proportional to the edit and should normally include:

1. Serve the repository root with a simple local static web server.
2. Check the page at desktop and mobile widths.
3. Verify every navigation link reaches the matching section and updates ScrollSpy state.
4. Verify the mobile menu opens, closes, and collapses after selecting a section.
5. Confirm profile images, Font Awesome icons, local CSS/JS, Google Fonts, and the TryHackMe badge load as expected.
6. Validate HTML and the JSON-LD structure after metadata or content edits.
7. Check external links, email links, accessible image text, keyboard focus, and color contrast.
8. Confirm SCSS/JavaScript source files still match their compiled or minified artifacts.
9. Review the Azure workflow if paths, branches, or build tooling change.
10. Confirm that intentional CTF clues still work without exposing their answers.

## Known Constraints and Improvement Opportunities

- The stack is functional but old; Bootstrap, jQuery, Font Awesome, and workflow action versions should be upgraded only as a deliberate, tested migration.
- There is no documented reproducible asset-build process despite committed SCSS and minified files.
- Resume content is duplicated across HTML, JSON-LD, Markdown, Word, and PDF sources, creating drift risk.
- The displayed profile image currently has an empty `alt` attribute; accessibility intent should be reviewed.
- Runtime third-party resources (Google Fonts and TryHackMe) affect privacy, availability, performance, and Content Security Policy options.
- Personal contact and career information is public by design, but future additions should be reviewed for privacy and operational-security concerns before deployment.
- The repository has no automated HTML, accessibility, link, visual-regression, or deployment tests.
- The current architecture is appropriate for a small static site. Introduce a framework or CMS only if concrete content-management or interaction requirements justify the added complexity.

## Rules for Future AI Work

- Inspect the current Git status before editing and preserve unrelated user changes.
- Treat `index.html` as the deployed application and verify whether supporting resume files are intentionally local/ignored before modifying them.
- Keep professional claims factual; do not invent achievements, metrics, dates, credentials, employers, or technologies.
- Ask for clarification when resume sources conflict or when a change could alter the CTF solution path.
- Update duplicated visible and structured metadata together.
- Keep generated CSS/JS artifacts synchronized with their readable sources.
- Avoid modifying files under `vendor/` unless performing an explicit dependency upgrade.
- Never commit secrets or embed the Azure deployment token.
- Preserve template/license attribution and the repository's MIT license requirements.
- Test responsive behavior and core navigation after any visual, structural, dependency, or content change.
