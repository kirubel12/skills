# Laravel release items

- Maintenance mode plan if downtime is possible (`php artisan down` / `up`).
- Migrations: `php artisan migrate --pretend` reviewed. Backup taken. Reversible or an explicit forward-fix plan.
- Caches rebuilt after deploy: `config:cache`, `route:cache`, `view:cache`. Queue workers restarted (`php artisan queue:restart`) so they run the new code.
- `.env` differences reviewed. `APP_DEBUG=false`, `APP_ENV=production`, keys and storage link present.
- `composer audit` reviewed. `composer install --no-dev --optimize-autoloader` in the build.
- Scheduler and queue configuration unchanged or intentionally changed. Failed-jobs table checked.
- Rollback: previous release directory or tag, plus the migration plan.
