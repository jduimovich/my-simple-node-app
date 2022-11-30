
# Using Actions with App Studio 

This repository uses Github Actions to build and deploy an application to App Studio.

The action builds an image and deploys to the internal ghcr.io registry with no additional configuation. You can redirect to quay.io or your preferred registry by updating the workflow.

The image built will be updated in App Studio via a component update which will take care of deployment into App Studio via built-in Gitops.

Install the creds with the following script. You need to be logged into App Studio in your terminal and have the GH command line tool
```

ROOT=~/.kube
if [ -n "$KUBECONFIG" ]
then
    ROOT=$(dirname "$KUBECONFIG") 
fi 
oc config use-context appstudio
oc get cm
KUBE_CONFIG=$(cat $ROOT/config | base64)

pushd $(pwd)
cd $ROOT/cache
tar cfv oidc.tar ./oidc-login/*
OIDC=$(cat oidc.tar | base64)
rm oidc.tar
popd

gh secret set KUBE_CONFIG -b "$KUBE_CONFIG"
gh secret set OIDC -b "$OIDC"
gh secret set MY_GITHUB_TOKEN -b "$MY_GITHUB_TOKEN"

```
