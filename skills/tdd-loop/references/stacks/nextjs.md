# Next.js test seams

| Behavior lives in | Test type | Notes |
|---|---|---|
| Pure functions, utilities | Unit test (Vitest or Jest) | Use whichever the repo already has |
| Client components | Testing Library (`@testing-library/react`) | Query by role and label, assert on what the user sees |
| Route handlers and server actions | Call the handler with a `Request`, or integration-test the route | Assert status and body. Mock the database or use a test database |
| Network calls from the browser | MSW at the boundary | Mock the network, not your own modules |
| Whole user flows | Playwright | Few, slow, on critical paths |

Run the profile's test command. Traps: server components cannot be rendered by plain Testing Library (test their data functions, or use e2e), hidden dependence on env vars, date and random values leaking into assertions.
