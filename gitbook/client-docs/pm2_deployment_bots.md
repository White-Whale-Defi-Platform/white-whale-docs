<!-- Docs for deployment arbitrage bot with pm2 -->
# Bot pm2 Setup
An alternative to manage multiple setups of the bot per chain to docker is process management via pm2. To do so, make sure that pm2 is correctly installed:
*   [Install pm2](https://pm2.keymetrics.io/docs/usage/quick-start/)

Navigate into the folder of the bot (usually `white-whale-bots`), but instead of starting it the usual way you will use
```start
pm2 start npm --name "app name" -- start
````
This will create a process that runs the bot called `app name`. It will also automatically try to restart the bot, if an error occurs or it holds for another reason.

## Useful prompts

```prompts
$ pm2 start app_name
$ pm2 stop app_name
$ pm2 logs app_name
```
For more sophisticated management see the linked docs above.