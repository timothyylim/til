# pm2 

Generate a config

```pm2 ecosystem```

Run using a specific config 

```
pm2 start ecosystem.config.js # uses variables from `env`
pm2 start ecosystem.config.js --env production # uses variables from `env_production`
```

Run a cron job

Use the --cron option:

```
-c --cron <cron_pattern>
````

For example:

```
pm2 start sendMail.js --cron "*/15 * * * *"
```

[Cron in English](https://crontab.guru)

Resources:
- [pm2 docs](https://pm2.io/doc/en/runtime/guide/ecosystem-file/?utm_source=pm2&utm_medium=website&utm_campaign=rebranding)
