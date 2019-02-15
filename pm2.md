# pm2 

Generate a config

```pm2 ecosystem```

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
- [pm2 docs](http://pm2.keymetrics.io/docs/usage/application-declaration/)
