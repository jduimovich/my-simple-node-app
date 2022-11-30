
# Using Actions with App Studio 

This repository uses Github Actions to build and deploy an application to App Studio.

The action builds an image and deploys to the internal ghcr.io registry with no additional configuation. You can redirect to quay.io or your preferred registry by updating the workflow.

The image built will be updated in App Studio via a component update which will take care of deployment into App Studio via built-in Gitops.

Simply fork this repo, provide your oidc creds via the `configure-oidc` script and push a change. The rest is automatic. 
