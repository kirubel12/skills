# Next.js release items

- `next build` passes with the production env. No build warnings that hide type or lint failures.
- Environment variables exist on the host for every environment (build-time and runtime are different), and no secret is `NEXT_PUBLIC_`.
- Database migrations run before the new code serves traffic, and the old code tolerates the new schema during rollout.
- Preview deployment checked on the critical paths. Caching and revalidation behave as intended after deploy.
- Source maps, error reporting and analytics configured. Redirects, headers and CSP reviewed.
- Rollback: redeploy the previous build (state how), and confirm the migration is backward compatible.
- `npm audit` or the package manager's audit reviewed.
