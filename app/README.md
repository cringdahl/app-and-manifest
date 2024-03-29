# GitOps & GitHub Actions CI/CD Example

This repository works in concert with the manifest repository to create a continuous delivery pipeline (based on Argo CD).

Code changes in this repository will trigger a workflow that builds this application into a Github container registry. Once the build is complete, it will trigger a workflow that creates a PR in the manifest repository that updates the deployment manifests to use the new container image tag. Merging that PR will automatically deploy the new container image on your OpenShift or Kubernetes cluster.

## Configure the Build

Enabling the end-to-end CI/CD process requires setting the MANIFEST_PAT variable in the */settings/secrets/actions* page of this repository.

The `MANIFEST_PAT` is a fine-grained GitHub personal access token. Create a MANIFEST_PAT from
your [Developer Settings](https://github.com/settings/tokens?type=beta) page.
While creating the MANIFEST_PAT, you should:

1. Set **Repository access** to your fork of the manifest repository.
1. Configure **Permissions** to enable **Read and Write** access to **Actions**.

## Local Development

```bash
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application in a browser.
