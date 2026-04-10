---
title: An Introduction to Kustomize - Scott's Weblog - The weblog of an IT pro focusing on cloud computing, Kubernetes, Linux, containers, and networking
source: https://blog.scottlowe.org/2019/09/13/an-introduction-to-kustomize/
author:
  - "[[Scott Lowe]]"
published: 2019-09-13
created: 2026-02-09
description: kustomize is a tool designed to let users “customize raw, template-free YAML files for multiple purposes, leaving the original YAML untouched and usable as is” (wording taken directly from the kustomize GitHub repository). Users can run kustomize directly, or—starting with Kubernetes 1.14—use kubectl -k to access the functionality (although the standalone binary is newer than the functionality built into kubectl as of the Kubernetes 1.15 release). In this post, I’d like to provide an introduction to kustomize.
tags:
  - clippings
  - k8s
  - kustomize
---
[`kustomize`](https://kustomize.io/) is a tool designed to let users “customize raw, template-free YAML files for multiple purposes, leaving the original YAML untouched and usable as is” (wording taken directly from [the `kustomize` GitHub repository](https://github.com/kubernetes-sigs/kustomize)). Users can run `kustomize` directly, or—starting with [Kubernetes](https://kubernetes.io/) 1.14—use `kubectl -k` to access the functionality (although the standalone binary is newer than the functionality built into `kubectl` as of the Kubernetes 1.15 release). In this post, I’d like to provide an introduction to `kustomize`.

In its simplest form/usage, `kustomize` is simply a set of resources (these would be YAML files that define Kubernetes objects like Deployments, Services, etc.) plus a set of instructions on the changes to be made to these resources. Similar to the way `make` leverages a file named `Makefile` to define its function or the way Docker uses a `Dockerfile` to build a container, `kustomize` uses a file named `kustomization.yaml` to store the instructions on the changes the user wants made to a set of resources.

Here’s a simple `kustomization.yaml` file:

```yaml
resources:
- deployment.yaml
- service.yaml
namePrefix: dev-
namespace: development
commonLabels:
  environment: development
```

This article won’t attempt to explain *all* the various fields that could be present in a `kustomization.yaml` file (that’s well handled [here](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/fields.md)), but here’s a quick explanation of this particular example:

- The `resources` field specifies which things (resources) `kustomize` will modify. In this case, it will look for resources inside the `deployment.yaml` and `service.yaml` files in the same directory (full or relative paths can be specified as needed here).
- The `namePrefix` field instructs `kustomize` to prefix the name attribute of all resources defined in the `resources` field with the specified value (in this case, “dev-”). So, if the Deployment specified a name of “nginx-deployment”, then `kustomize` would change the value to “dev-nginx-deployment”.
- The `namespace` field instructs `kustomize` to add a namespace value to all resources. In this case, the Deployment and the Service are modified to be placed into the “development” namespace.
- Finally, the `commonLabels` field includes a set of labels that will be added to all resources. In this example, `kustomize` will label the resources with the label name “environment” and a value of “development”.

When a user runs `kustomize build .` in the directory with the `kustomization.yaml` and the referenced resources (the files `deployment.yaml` and `service.yaml`), the output is the customized text with the changes found in the `kustomization.yaml` file. Users can redirect the output if they want to capture the changes:

```shell
kustomize build . > custom-config.yaml
```

The output is deterministic (given the same inputs, the output will always be the same), so it may not be necessary to capture the output in a file. Instead, users could pipe the output into another command:

```shell
kustomize build . | kubectl apply -f -
```

Users can also invoke `kustomize` functionality with `kubectl -k` (as of Kubernetes 1.14). However, be aware that the standalone `kustomize` binary is more recent than the functionality bundled into `kubectl` (as of the Kubernetes 1.15 release).

Readers may be thinking, “Why go through this trouble instead of just editing the files directly?” That’s a fair question. In this example, users *could* modify the `deployment.yaml` and `service.yaml` files directly, but what if the files were a fork of someone else’s content? Modifying the files directly makes it difficult, if not impossible, to rebase the fork when changes are made to the origin/source. However, using `kustomize` allows users to centralize those changes in the `kustomization.yaml` file, leaving the original files untouched and thereby facilitating the ability to rebase the source files if needed.

The benefits of `kustomize` become more apparent in more complex `kustomize` use cases. In the example shown above, the `kustomization.yaml` and the resources are in the same directory. However, `kustomize` supports use cases where there is a “base configuration” and multiple “variants”, also known as *overlays*. Say a user wanted to take this simple Nginx Deployment and Service I’ve been using as an example and create development, staging, and production versions (or variants) of those files. Using overlays with shared base resources would accomplish this.

To help illustrate the idea of overlays with base resources, let’s assume the following directory structure:

```yaml
- base
  - deployment.yaml
  - service.yaml
  - kustomization.yaml
- overlays
  - dev
    - kustomization.yaml
  - staging
    - kustomization.yaml
  - prod
    - kustomization.yaml
```

In the `base/kustomization.yaml` file, users would simply declare the resources that should be included by `kustomize` using the `resources` field.

In each of the `overlays/{dev,staging,prod}/kustomization.yaml` files, users would reference the base configuration in the `resources` field, and then specify the particular changes for *that environment*. For example, the `overlays/dev/kustomization.yaml` file might look like the example shown earlier:

```yaml
resources:
- ../../base
namePrefix: dev-
namespace: development
commonLabels:
  environment: development
```

However, the `overlays/prod/kustomization.yaml` file could look very different:

```yaml
resources:
- ../../base
namePrefix: prod-
namespace: production
commonLabels:
  environment: production
  sre-team: blue
```

When a user runs `kustomize build .` in the `overlays/dev` directory, `kustomize` will generate a development variant. However, when a user runs `kustomize build .` in the `overlays/prod` directory, a production variant is generated. All without *any* changes to the original (base) files, and all in a declarative and deterministic way. Users can commit the base configuration and the overlay directories into source control, knowing that repeatable configurations can be generated from the files in source control.

There’s a *lot* more to `kustomize` that what I’ve touched upon in this post, but hopefully this gives enough of an introduction to get folks started.

## Additional Resources

There are quite a few good articles and posts written about `kustomize`; here are a few that I found helpful:

[Change base YAML config for different environments prod/test using Kustomize](https://levelup.gitconnected.com/kubernetes-change-base-yaml-config-for-different-environments-prod-test-6224bfb6cdd6)

[Kustomize - The right way to do templating in Kubernetes](https://blog.stack-labs.com/code/kustomize-101/)

[Declarative Management of Kubernetes Objects Using Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/)

[Customizing Upstream Helm Charts with Kustomize](https://testingclouds.wordpress.com/2018/07/20/844/)

[RFC 6902](https://tools.ietf.org/html/rfc6902) (useful when using JSON patches with Kustomize)

[Examples from the Kustomize GitHub repository](https://github.com/kubernetes-sigs/kustomize/tree/master/examples)

If anyone has questions or suggestions for improving this post, I’m always open to reader feedback. Feel free to [contact me via Twitter](https://twitter.com/scott_lowe), or hit me up on [the Kubernetes Slack instance](https://kubernetes.slack.com/). Have fun customizing your manifests with `kustomize`!

### Metadata and Navigation

Be social and share this post!