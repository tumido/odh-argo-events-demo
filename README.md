# Argo Events - Demo

## Setup

1. Deploy ODH Argo and Argo events
2. Deploy demo templates

    ```sh
    $ oc apply -f calendar.yml
    $ oc apply -f webhook.yml
    $ oc apply -f sensor.yml
    ```

## Webhook event source trigger

```sh
curl -X POST -d '{"message": "Hello! I am a Beluga whale!"}' http://webhook-odh-argo-demo.apps.10.0.109.139.nip.io/example
```

## Observe

### All workflow logs

```sh
for wf in `argo list -o name`; do echo -n "\n$wf:\n"; argo logs $wf; done;
```

### List workflows with labels

```sh
oc get wf --show-labels
```

## Cleanup

```sh
oc delete wf --selector "workflows.argoproj.io/completed=true"
```
