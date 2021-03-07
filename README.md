# Pragmatic GitOps: Part 1 - Kustomize

## Introduction

This is a companion repository that goes along with my "Pragmatic Gitops: Part 1 - Kustomize" blog post.

Here, you can find everything you need to start with the same project in the "gitops-demo" namespace so you can try to replciate the process yourself.

There is also the final "base" and "overlays" directories, so you can see what the finished product should look like.

## Deploying the "gitops-demo" Project

If you want to start off with the same setup used in the blog, login to your OpenShift cluster (4.5+) with the `oc` command line tool and run the following:

```
$ git clone https://github.com/pittar-demos/pragmatic-gitops-01-kustomize.git
$ cd pragmatic-gitops-01-kustomize
$ oc new-project gitops-demo
$ oc apply -f demo
```

This will spin up the same app and database from the blog post.  If the petclinic app starts before the MySQL database initializes, you will have to scale the app down to zero, then back up again (or just kill the pod) in order for the app to start properly once the database is ready.

## Deploying the DEV and PROD Environments

If you just want to deploy the resulting DEV and PROD environments, then first login to your OpenShift cluster with the `oc` command line tool.  You should be logged in as a user than can create new namespaces.  Then, run the following commands.  You can use either `kubectl` of `oc` to run the `apply` commands.  

```
$ git clone https://github.com/pittar-demos/pragmatic-gitops-01-kustomize.git
$ cd pragmatic-gitops-01-kustomize
$ kubectl apply -k overlays/dev
$ kubectl apply -k overlays/prod
```

This will create the `gitops-dev` and `gitops-prod` namespaces and deploy the app in both.

Don't want to have to clone this repository?  No problem!  Making sure you have cli access to your OpenShift cluster, run the following commands (you can also substitute `oc` for `kubectl` if you like):

```
$ kubectl apply -k https://github.com/pittar-demos/pragmatic-gitops-01-kustomize/overlays/dev?ref=main
$ kubectl apply -k https://github.com/pittar-demos/pragmatic-gitops-01-kustomize/overlays/prod?ref=main
```


## Next Steps

The next part in the series will use [Argo CD](https://argoproj.github.io/argo-cd/) to deploy the application and provide lifecycle capabilities.