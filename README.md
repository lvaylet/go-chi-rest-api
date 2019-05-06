# Running a Simple Golang Chi REST API on Google Cloud Run

> Forked from https://github.com/go-chi/chi REST example, adapted for Google Cloud Run

## Build and Deploy to Google Cloud Run

Build and deploy the Dockerfile with:

```
PROJECT=<YOUR_GCP_PROJECT_ID>
SERVICE=go-chi-rest-api
gcloud config set projet ${PROJECT}
gcloud builds submit --tag gcr.io/${PROJECT}/${SERVICE}
gcloud beta run deploy --image gcr.io/${PROJECT}/${SERVICE} --region us-central1
```

Retrieve the exposed endpoint with:

```
ENDPOINT=$(gcloud beta run services describe ${SERVICE} --region us-central1 --format "value(status.address.hostname)")
```

## Query the Endpoint

```
curl ${ENDPOINT}/articles
curl ${ENDPOINT}/articles/1
curl -X DELETE ${ENDPOINT}/articles/1
curl ${ENDPOINT}/articles/1
curl -X POST -d '{"id":"will-be-omitted","title":"awesomeness"}' ${ENDPOINT}/articles
curl ${ENDPOINT}/articles/91
curl ${ENDPOINT}/articles
```

## References

- https://github.com/go-chi/chi/tree/master/_examples/rest
- https://github.com/lvaylet/multi-stage-golang-docker
