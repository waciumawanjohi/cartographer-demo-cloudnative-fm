# CloudNative.FM Cartographer Demo

## Intro

These are the example files used in the [CloudNative.FM episode highlighting
Cartographer](https://www.youtube.com/watch?v=RJCbQ1zQSBs). Cartographer is an open
source project allowing you to get your code to production using Kubernetes Resources as your primitives, rather
than executable files. Leave bash scripting behind and make your software supply chain cloud native!

## Pre-reqs

There are two prerequisites to running the full supply chain example:

1. A registry to which you have write permissions. E.g. dockerhub or gcr.
2. In the [kpack-boilerplate](full-supply-chain/kpack-boilerplate.yaml) file, alter the tag field of the cluster
   builder. E.g. change `index.docker.io/waciumawanjohi/example-gitwriter-sc-go-builder` to
   `YOUR_REGISTRY/YOUR_PROJECT/example-gitwriter-sc-go-builder`
3. In the [supply chain](full-supply-chain/supply-chain.yaml), alter the `image-builder`'s `image-prefix` param to
   point to your registry. E.g. change `index.docker.io/waciumawanjohi/example-gitwriter-sc-` to
   `YOUR_REGISTRY/YOUR_PROJECT/example-gitwriter-sc-`
4. Create a secret with credentials to write to that repository. This secret must be named `registry-credentials`.
   E.g. apply the following to your cluster after having entered your credentials.

```yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: registry-credentials
  annotations:
    kpack.io/docker: https://index.docker.io/v1/
type: kubernetes.io/basic-auth
stringData:
  username: "SOME_USERNAME"
  password: "SOME_PASSWORD"
```

## Learn More

There are many resources to learn about Cartographer. [Our project website](https://cartographer.sh/) includes:

- [Documentation](https://cartographer.sh/docs/v0.3.0/)
- [Tutorials](https://cartographer.sh/docs/v0.3.0/tutorials/first-supply-chain/)
- [Blog Posts](https://cartographer.sh/blog/)
- [Presentations](https://cartographer.sh/resources/)

[Join us on the Kubernetes Slack server!](https://kubernetes.slack.com/archives/C02HKPSEKV1)
