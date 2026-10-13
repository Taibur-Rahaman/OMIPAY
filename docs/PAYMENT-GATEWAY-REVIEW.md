# OMIPAY Payment Gateway Code Review — Initial Findings

**Review scope:** Static inspection of selected gateway files on the default branch. This is not a complete audit, runtime test, or certification.

## Finding 1 — SSLCommerz TLS certificate verification is disabled

**File:** `pp-content/pp-modules/pp-gateways/sslcommerz/class.php`  
**Location:** `process_payment()`, cURL options near the payment initialization request  
**Evidence:** The request sets `CURLOPT_SSL_VERIFYPEER` to `false` without restricting this behavior to sandbox mode.

**Risk:** A connection may fail to authenticate the remote TLS certificate, increasing exposure to man-in-the-middle attacks. This matters because the request includes merchant credentials and payment details.

**Recommended remediation:** Remove the disabling option or explicitly enable peer verification; set `CURLOPT_SSL_VERIFYHOST` to `2`; configure connection/overall timeouts; handle cURL errors and non-2xx responses. Verify the behavior in sandbox and live environments before release.

## Finding 2 — Raw gateway response is rendered into HTML

**File:** `pp-content/pp-modules/pp-gateways/sslcommerz/class.php`  
**Location:** `process_payment()`, error branch after the initiation request  
**Evidence:** The error branch directly concatenates the raw gateway response into an HTML response.

**Risk:** If response content can contain attacker-controlled markup, it may create a cross-site scripting risk in the checkout context.

**Recommended remediation:** Do not render raw provider responses to the browser. Log a sanitized diagnostic server-side and show a fixed generic error message to the customer.

## Finding 3 — Gateway redirect URL is inserted into JavaScript

**File:** `pp-content/pp-modules/pp-gateways/sslcommerz/class.php`  
**Location:** `process_payment()`, successful initiation branch  
**Evidence:** The provider-returned `GatewayPageURL` is concatenated into a JavaScript string and used for navigation.

**Risk:** Untrusted or malformed provider response data can break out of the JavaScript string or redirect users to an unexpected destination.

**Recommended remediation:** Validate that the URL is HTTPS and belongs to the provider's documented checkout host(s), then safely encode the URL for the output context. Prefer a server-side HTTP redirect if supported by the checkout architecture.

## Finding 4 — Stripe checkout error handling and webhook flow need further verification

**File:** `pp-content/pp-modules/pp-gateways/stripe/class.php`

**Observed:** The gateway creates a Checkout Session and verifies payment status by retrieving the session and PaymentIntent during the return callback. A `webhook_secret` field is configured, but the reviewed file does not show webhook signature verification.

**Risk / limitation:** This does not prove webhook handling is absent elsewhere. The wider request router and callback architecture must be inspected before making a final conclusion. HTTP status codes, cURL errors, currency/amount consistency, and duplicate callback behavior also need tests.

**Recommended remediation:** Trace the full webhook/request routing path; verify signatures against the raw request body if webhook events are used; enforce amount, currency, session, invoice, and account consistency; make status updates idempotent; and avoid trusting browser redirects alone.

## Priority order

1. Fix and test TLS verification in the SSLCommerz request path.
2. Remove raw provider-response HTML output and safely handle provider redirect URLs.
3. Trace Stripe callback/webhook routing and test idempotency and transaction matching.
4. Review all gateway modules with the same checklist and run sandbox integration tests.

**Do not enable live transactions based on this static review alone.** These findings should be validated with tests in a controlled environment, and the original upstream license and notices must remain intact.
