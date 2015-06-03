# SmartSeeder for Laravel

*Note*: This is a fork of slampenny's SmartSeeder which is currently being developed to work with Laravel 5. I happen to need it to be working ASAP. Not wanting to wait around for the original maintainer to approve my patches, I made a new branch called `5.0-plinth` where I merge all my pull request into. They are not yet thoroughly tested and shouldn't be used in the production environment (irony).

Seeding as it is currently done in Laravel is intended only for dev builds, but what if you want to seed a production database with different data from what you use in development? What if you want to seed a table you've added to a database that is currently in production with new data?

Features
========

- Allows you to seed databases in different environments with different values. Environment can be specified through `--env` option. If none is specified, it will read your `.env` file.
- Allows you to "version" seeds the same way that Laravel currently handles migrations. Running `php artisan seed` will only run seeds that haven't already been run.
- Prompts you if your database is in production.
- Allows you to run multiple seeds of the same model/table
- Overrides Laravel's seeding commands. SmartSeeder will fire when you run
    ```
    php artisan db:seed
    ```
     or
    ```
    php artisan migrate:refresh --seed
    ```

Use
=====
When you install SmartSeeder, various artisan commands are made available to you which use the same methodology you're used to using with Migrations.

<table>
<tr><td>seed:run</td><td>Runs all the seeds in the smartSeeds directory that haven't been run yet.</td></tr>
<tr><td>seed:make</td><td>Makes a new seed class in the environment you specify.</td></tr>
<tr><td>seed:rollback</td><td>Rollback doesn't undo seeding (which would be impossible with an auto-incrementing primary key). It just allows you to re-run the last batch of seeds.</td></tr>
<tr><td>seed:reset</td><td>Resets all the seeds.</td></tr>
<tr><td>seed:refresh</td><td>Resets and re-runs all seeds.</td></tr>
<tr><td>seed:install</td><td>You don't have to use this... it will be run automatically when you call "seed"</td></tr>
</table>

Installation
============

- Since I didn't register my package with composer, you will want to run git clone to grab my file into your vendor folder then dump the autoload manually.
- Add 'Jlapp\SmartSeeder\SmartSeederServiceProvider' to your providers array in config/app.php
- Run `php artisan config:publish mayppong/smart-seeder` to push config files to your app folder if you want to override the name of the seeds folder or the name of the table where seeds are stored
