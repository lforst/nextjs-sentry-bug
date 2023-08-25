# Repro

1. `rm -rf .next && npm run build && npm run start`
2. `curl http://localhost:3000/api/endpoint-behind-middleware`

Examine `TypeError: Cannot read properties of null (reading 'useContext')` in stdout.

## Some background:

We found this behaviour in our canary tests for new Next.js versions for the Sentry Next.js SDK from version `next@13.4.20-canary.2` (could be earlier, it was just the first canary test we noticed it on).

The repro app doesn't really do anything besides throwing inside middleware.

Good part: This behaviour only happens when the application state is already panicking.
Bad part: It appears to affect the Sentry SDK, which does a bunch of stuff when errors happen.
