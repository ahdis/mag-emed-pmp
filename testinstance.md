get soap logs
=============

get pod from number from https://console.cloud.google.com/kubernetes/deployment/europe-west6-a/cluster-ch-01/default/mag-pmp/overview?authuser=1&project=fhir-ch&pageState=(%22savedViews%22:(%22i%22:%22eaf155a238e34077b2696fd3ca9c8bf5%22,%22c%22:%5B%5D,%22n%22:%5B%5D),%22deployment_overview_active_revisions_table%22:(%22r%22:50))

```
gcloud container clusters get-credentials cluster-ch-01 --zone europe-west6-a --project fhir-ch \
kubectl cp mag-pmp-6979c45c9d-76hv4:logs ./pmplogs/

```