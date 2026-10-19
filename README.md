# Local CSV PII Masker

A local-first, browser-based tool for masking PII in CSV report packages and free text.

## Quick start

1. Open `local-csv-pii-masker-v2.7.0.html` in a recent Chromium-based browser.
2. Choose a built-in profile or create/duplicate a custom profile.
3. Add CSV files, validate the package, then mask it.
4. Review samples and diagnostics as needed.
5. Download individual masked files or all outputs as a ZIP.

No server or installation is required for core masking. Processing happens in browser memory using Web Workers.

## Masking types

- Account / organization values -> `[ACCOUNT-###]`
- Person names from configured structured fields -> `[NAME-###]`
- Email addresses -> `[EMAIL-###]`
- Phone numbers -> `[PHONE-###]`
- IPv4 / IPv6 addresses -> `[IP-###]`
- URLs -> `[URL-###]`

Structured reference values can be learned from configured fields and masked consistently across a multi-report package.

## Profiles

The public build includes generic multi-report and single-CSV templates. Built-in profiles cannot be overwritten or deleted. You can edit one as a draft and save it under a new name, create a new profile, duplicate an existing profile, or import/export profile JSON.

Custom profiles and the last active profile are stored in browser `localStorage` when available.

## Suggestion Exclusions

Free-text masking includes heuristic suggestions for possible PII. **Suggestion Exclusions** let you suppress known noisy terms or phrases from that heuristic review.

An exclusion only means "do not suggest this phrase as possible PII." It does **not** stop structured or deterministic masking. For example, if an excluded phrase is explicitly learned from a configured `ACCOUNT` field, it can still be masked as an account value.

Suggestion Exclusions are stored locally in the browser and can be exported/imported together with custom profiles using Settings export/import.

## Privacy and limitations

The core masker is designed to process content locally in the browser and does not intentionally upload CSV or text content to an external service. The GitHub author link is only followed if you click it.

**Masked does not mean PII-free.** Deterministic and configured masking can produce false positives and false negatives. Review masking samples and diagnostics when using new schemas or unfamiliar data.

Uploaded content, detected PII, token mappings, samples, and free text are not intentionally persisted by the app. Persistent browser settings are limited to configuration such as custom profiles, the active profile, and suggestion exclusions.

## Performance

The application uses Web Workers and a combined structured-value matcher to keep the UI responsive and avoid repeatedly scanning large text for each structured PII reference value. Actual performance depends on hardware, browser, file size, schema, and masking configuration.

## Author

[rbcepres](https://github.com/rbcepres)

## License

Released under the [MIT License](LICENSE).
