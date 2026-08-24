<div align="center">

# pushinbr/pam-testing

## Compatibility package — do not use in new applications

This repository exists so older Composer projects keep installing safely. The maintained product is **[PAM HTTP Testing](https://github.com/push-in/pam-http-testing)**.

[![Replacement](https://img.shields.io/badge/replacement-pushinbr/pam--http--testing-2563eb?style=flat-square)](https://packagist.org/packages/pushinbr/pam-http-testing)
![Status](https://img.shields.io/badge/status-migration%20only-f59e0b?style=flat-square)

</div>

---

## Use this instead

```bash
pam composer require --dev pushinbr/pam-http-testing
```

[PAM HTTP Testing](https://github.com/push-in/pam-http-testing) contains the active documentation, API examples, releases, issue tracker, and production guidance.

## Why the name changed

The test helpers exercise PAM HTTP applications; the new name makes that scope explicit and leaves room for Native and other testing products.

## Migrate an existing project

Commit your current `composer.json` and `composer.lock`, then run:

```bash
pam composer remove pushinbr/pam-testing
pam composer require --dev pushinbr/pam-http-testing
pam doctor
```

Run the application test suite before committing the new lockfile. Composer may continue to resolve this bridge transitively during a staged migration; application code should target the replacement package directly.

## Support policy

- No new features are added here.
- Security or resolution fixes may be published only to preserve migration safety.
- New documentation and issues belong to [PAM HTTP Testing](https://github.com/push-in/pam-http-testing).
- The package is marked abandoned on Packagist in favor of `pushinbr/pam-http-testing`.

This explicit compatibility repository is intentional: old installs remain understandable without making the current PAM ecosystem ambiguous.
