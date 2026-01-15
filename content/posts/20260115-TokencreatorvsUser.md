---
title: "Service Account User vs Service Token Creator"
summary: 
date: 2026-01-15
series: ["PaperMod"]
weight: 1
aliases: ["/token-vs-account-user"]
tags: ["token creator"]
author: ["Carlos A"]
---

The Service Account User and Service Token Creator roles are two roles within Google Cloud that I find confusing. 

In IT and Computing, service accounts are made for workloads that are not intended to represent a human identity. Service accounts are different to user accounts, which are accounts created for the use of an individual. 

For example- if you were building a production CI/CD pipeline, you might use a service account to authenticate to your cloud provider and make changes. You could authenticate with a user account in this example, but this isn't considered best practice. Consider a situation where user credentials are used within a CI/CD pipeline to make changes to the cloud. If the person whose account is being used would leave the company, you would need to make sure this is changed before their accounts are shut down. Deploying services authenticated as users works fine during the development stage, but is not suitable for production. 

In Google Cloud, user and service accounts can be assigned roles which grant specific sets of permissions on the accounts. Service Account User and Service Account Token Creator are examples of these.

## Service Account User

As mentioned earlier, it's best practice to use service accounts for non-human workloads e.g. Compute Engine VMs, Cloud Functions, Cloud Run. In order to assign these service accounts to workloads you need the Service Account User role. This can be confusing because the documentation's description for the role is "Run operations as the service account". Whilst this is correct, it perhaps sounds a bit vague as it does not specify that this is done by attaching the account to the workload. On the other hand, the description for Service Account Token Creator is much more precise. 

## Service Account Token Creator 

In some cases, a user might need permissions to assume or 'impersonate' a service account. This is what the Service Account Token Creator role is for.

"Impersonate service accounts (create OAuth2 access tokens, sign blobs or JWTs, etc)." - GCP IAM reference

This role allows you to create short lived credentials for a service account e.g. Oauth 2.0 access tokens, OIDC tokens and Signed JSON web tokens.

When granted this role, you can use the --impersonate-service-account flag for gcloud commands which automatically generates short-lived credentials for that service account.


