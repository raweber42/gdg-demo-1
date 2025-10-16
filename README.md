## Prerequisites
- Create GCP project
- Enable IAM API

## Setup Steps

### 1. Create Kubernetes Cluster
Create cluster (see [kubernetes-sandbox](https://github.com/raweber42/kubernetes-sandbox))

### 2. Install Crossplane
Install crossplane (also see above repository)

### 3. Install GCP Storage Provider
Since there are many components, there are separate providers for all kinds of GCP domains:
```bash
kubectl apply -f provider-gcp-storage.yml
```

### 4. Setup GCP Authentication
Create a GCP project, service account with necessary permissions and get credentials for Crossplane:

- Create project
- Service account → Create service account → Give permission (e.g. storage owner) → Click manage keys → Add key → JSON 

### 5. Create Kubernetes Secret
Create a Kubernetes secret with credentials for Crossplane to authenticate against the API:

```bash
kubectl create secret generic gcp-secret -n crossplane-system --from-file=creds=./gcp-credentials.json
```

### 6. Apply Provider Configuration
Create the provider configuration, referencing the secret:

```bash
kubectl apply -f provider-config-gcp-storage.yml
```

See: [provider-config-gcp-storage.yml](provider-config-gcp-storage.yml)

### 7. Create Google Cloud Bucket
Apply the manifest to create your bucket:

```bash
kubectl apply -f demo-bucket.yml
```

See: [demo-bucket.yml](demo-bucket.yml)

## Presentation

For more details, see the [presentation slides](https://docs.google.com/presentation/d/1Q3QCwRUwk7oKP8mUtbM3THN5SCTWZW1GaFltpqU4KD0/edit?usp=sharing).
