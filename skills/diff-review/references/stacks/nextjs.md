# Next.js review checks

- Server and client boundary: secrets or server-only imports reachable from a `"use client"` file. `NEXT_PUBLIC_` used for anything secret.
- Authentication and authorization checked inside every route handler and server action, not only in the UI or middleware.
- Input validation on route handlers and server actions (schema validation). User input reaching SQL, shell or `dangerouslySetInnerHTML`.
- Caching: stale data from fetch, route or data cache settings for the installed Next version. Missing revalidation after mutations.
- Hydration risks: `window`, `Date.now`, `Math.random` or locale formatting during render.
- Bundle: large client-side imports, images without `next/image` sizing, blocking third-party scripts.
- Type errors hidden by `any` or non-null assertions. Missing error and loading boundaries.
