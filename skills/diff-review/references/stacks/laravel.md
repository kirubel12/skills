# Laravel review checks

- Mass assignment: `$fillable` or `$guarded` correct, `create($request->all())` avoided.
- Authorization: policies or gates applied to every action, not just authentication. Form Request `authorize()` not left returning true.
- Validation on every write path. Raw queries or `DB::raw` with user input (SQL injection). Unescaped Blade output (`{!! !!}`).
- N+1 queries (use `with()`), unbounded `get()` on large tables (use chunking or pagination), missing indexes on new filters.
- Migrations: reversible, safe on large tables, never edit one that has already run in production.
- Jobs and events: idempotent, queued where slow, failure handling. Secrets read via `config()`, not `env()` outside config files.
- Tests for the new behavior, including a forbidden-user case.
