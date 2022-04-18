# NJU Health Checkin

> NJU daily health checkin, with features of fake locations and tgbot info, bypasses CAPTCHA using cookies.
>
> Used to be a fork from [forewing/nju-health-checkin](https://github.com/forewing/nju-health-checkin).
>
> **This project is only for learning. Developers will not be responsible for the consequences of the project.**

## Requirements

```
python3 -m pip install requests
```

## Run with Github Actions

If use Github Actions, you need to:

* fork this project.
* Find `secret` in your project settings, and go to `Actions secrets`, create environment secrets with name `NJU_COOKIE`. If use telegram bot to send info, also create `TELEGRAM_TO` and `TELEGRAM_TOKEN`.
* Go to `Actions` -> `workflows` -> `Checkin`, run it manually to test if it is working.

## Run with Crontab

You can also deploy it on your server.

This script provides features of sending checkin info using telegram-bot, and manually specifying fake location. You can feel free to use all of these two features or neither of them.

if use telegram bot, `crontab -e` and write:

```crontab
0 21 * * * /usr/bin/env http_proxy=url:port https_proxy=url:port bottoken=xxx tgid=yyy bash run.sh # run at 9pm everyday. the http_proxy and https_proxy are for telegram bot
```

If you don't need to send checkin message via telegram bot, write:

```crontab
0 21 * * * /usr/bin/env bash run.sh # run at 9pm everyday
```

Note:

* Complete your own `config.ini` file. You need to complete **cookie** of these two fields: `CASTGC` and `AUTHTGC`. No other fields are needed. DON'T write any other field in config file.
* If **always use the location in the last checkin**, just left `location` blank. If checkin requests do not use proxy, left `proxy` blank. Otherwise specify the proxy url and port explicitly in `config.ini` (`checkin.py` ignores proxy setting in env!)

## Contributions

- Previous: [checkin.py](checkin.py)  by [Maxwell Lyu](https://github.com/Maxwell-Lyu). Rewrite by [Antares](https://github.com/Antares0982).

* `run.sh` by [Antares](https://github.com/Antares0982).
