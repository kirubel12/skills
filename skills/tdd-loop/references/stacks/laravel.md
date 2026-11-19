# Laravel test seams

| Behavior lives in | Test type | Notes |
|---|---|---|
| HTTP endpoints, policies, validation | Feature test (Pest or PHPUnit) | `$this->postJson(...)`, assert status, JSON and database state. Use `RefreshDatabase` and factories |
| Business logic in services or actions | Unit test | Plain PHP, inject collaborators |
| Jobs, mail, events, notifications | `Queue::fake()`, `Mail::fake()`, `Event::fake()` | Assert dispatched, then test the job body separately |
| External HTTP | `Http::fake()` | The system boundary |

Run: `php artisan test --filter=<name>`. Traps: asserting on the framework instead of your behavior, shared database state between tests, testing authorization only as an admin.
