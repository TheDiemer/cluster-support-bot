# Setup in OpenShift

```sh
oc new-app https://github.com/<project>/cluster-support-bot.git \
  -e APP_FILE=cluster-support-bot.py \
  -e BOT_ID=<bot ID -- hover over the bot name in Slack to get this> \
  -e SLACK_BOT_TOKEN=<token from https://api.slack.com/apps/XXXXXX/install-on-team?> \
  -e HYDRA_USER=<FIXME: how to get one of these> \
  -e HYDRA_PASSWORD=<FIXME: how to get one of these> \
  -e TELEMETRY_URI=https://FIXME.example.com/your-telemetry-query-uri \
  -e TELEMETRY_TOKEN=<token from https://help.datahub.redhat.com/docs/interacting-with-telemetry-data> \
  -e DASHBOARDS=https://FIXME.example.com/somewhere-users-can-see-cluster-details?cluster-id=
```

`DASHBOARDS` can have multiple, space-delimited URIs, in which case links to all of them will be provided when rendering summaries.

Optionally set `TELEMETRY_CA_CERT` to a URI serving PEM for a CA cert
to use when validating Telemetry requests.

Test by using `oc logs -f <podname>`to make sure it's running.

## Expose the route
```sh
oc create route edge --service=cluster-support-bot
```
