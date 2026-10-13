# OMIPAY SaaS Readiness Audit

**Status:** Initial checklist — not a security certification or launch approval  
**Repository:** https://github.com/Taibur-Rahaman/OMIPAY  
**Current posture:** Educational/development preview. Do not process live customer payments until the checks below are completed.

## 1. Repository and release integrity

- [ ] Confirm the complete upstream application source is present in this repository.
- [ ] Record the upstream PipraPay version/commit and the exact OMIPAY changes.
- [ ] Keep upstream copyright notices, license files, and third-party notices.
- [ ] Review AGPL-3.0 obligations for modified versions offered over a network; provide corresponding source as required.
- [ ] Add a reproducible release/build process and dependency lockfiles.

## 2. Payment security

- [ ] Use sandbox credentials until provider approval and end-to-end tests are complete.
- [ ] Keep API secrets in environment variables or a managed secret store, never in Git.
- [ ] Verify webhook signatures and reject invalid, expired, or replayed events.
- [ ] Make webhook processing idempotent; handle retries and out-of-order events safely.
- [ ] Validate amount, currency, merchant/account mapping, and transaction state server-side.
- [ ] Never treat a browser redirect alone as proof of payment.
- [ ] Avoid storing raw card data; follow provider requirements and applicable PCI scope.
- [ ] Add rate limits, request validation, secure session settings, CSRF protection where applicable, and authorization checks.

## 3. SaaS tenant isolation

- [ ] Define tenant/account boundaries and ownership rules.
- [ ] Prove every tenant-scoped query and API endpoint enforces tenant authorization.
- [ ] Separate tenant credentials and prevent cross-tenant secret or transaction exposure.
- [ ] Add role-based access control, audit logs, and secure account recovery.
- [ ] Define plan limits, usage metering, suspension, cancellation, and data export/deletion behavior.

## 4. Reliability and operations

- [ ] Configure HTTPS, secure production headers, and least-privilege server permissions.
- [ ] Set up encrypted backups and test restoration.
- [ ] Add monitoring, error alerting, audit trails, and incident-response procedures.
- [ ] Document key rotation, failed payment reconciliation, refunds, disputes, and provider outages.
- [ ] Run dependency, static-analysis, and penetration/security tests before launch.

## 5. Business and compliance

- [ ] Confirm each payment provider permits the intended platform/aggregator business model.
- [ ] Review Bangladesh and target-market legal, tax, privacy, consumer-protection, and payment regulations with qualified advisers.
- [ ] Publish clear terms, privacy notice, refund/cancellation policy, support contacts, and service-level expectations.
- [ ] Do not claim regulatory approval, PCI compliance, or production readiness without evidence.

## 6. Current verification notes

The initial GitHub review confirmed the OMIPAY README, license, branding assets, system requirements page, and admin shell file. The repository paths checked for common settings, gateway, webhook, and subscription pages were not found at those exact paths. This does **not** prove those features are absent; the full source tree and actual route/file structure must be confirmed before implementation or a security conclusion.

## Recommended next step

Import/verify the complete application source and identify the actual payment gateway, webhook, user/account, and configuration code paths. Then audit those specific files before adding subscription billing or enabling live transactions.
