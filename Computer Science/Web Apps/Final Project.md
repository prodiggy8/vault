##### CSRF

A **JWT** is a string with three parts: `header.payload.signature`.
- *Header:* JSON, base64-encoded. Says what signing algorithm is used.
- *Payload:* Holds claims about the user: user_id, expiry timestamp, issued_at, etc.
- *Signature:* Only the server knows the secret key so only the server can produce a valid signature.

Server re-runs HMAC over header and payload it received.

**Access token** is short-lived, sent on every API call.
**Refresh token** is long-lived, sent only to a single endpoint to generate a new access token.

`POST /api/login` returns `{access, refresh}`.
Frontend stores both in `localStorage`.
Every outgoing call goes through `apiFetch` which reads the access token and sets as header.
On a 401, the client uses the refresh token to get a fresh access token.
No cookies are involved.

CSRF exploits the auto-attach of credentials to outgoing requests, even one the user did not intend to make.

Textbook example: `bank.com` uses session cookies. `evil.com` contains a form with target to bank account, session is automatically attached.

- Forms can't set custom headers
- A `fetch()` would be cross-origin, we have allowed origins.
- `localStorage` is partitioned by origin, can't read store from other domains.

