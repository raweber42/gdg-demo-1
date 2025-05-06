-> create GCP project
-> enable IAM api


kubectl create secret generic gcp-secret -n upbound-system --from-file=creds=./gcp-credentials.json

