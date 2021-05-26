---
layout: classic-docs
title: ""
category:
  - administration
order: 5
description: "CircleCI "
---

CircleCI 

-  
{:toc}

## 

CircleCI  CircleCI   GPG  (ID0x4013DDA73CD2 A48F 2071 61C0 B9B7 1AE2 6170 15B8 4013 DDA7) <security@circleci.com> 

## 

CircleCI CircleCI  HTTPS  SSH  Services Services  Builder Builder   CircleCI  CircleCI  SSL  TLS 

CircleCI  CircleCI  (Docker  VM)   SSH  Git     1  [HashiCorp  Vault](https://www.vaultproject.io/)  AES256-GCM96 CircleCI 

## 

CircleCI   Builder boxes          ()  1  CircleCI   SSH     CircleCI 

## 

CircleCI    

- **WebSocket:** CircleCI  WebSocket  [Pusher](https://pusher.com/)   slanger Pusher  CircleCI    1   WebSocket  (SSL  CircleCI SSL )

- **Replicated:** CircleCI Server  [Replicated](http://www.replicated.com/)   CircleCI  CircleCI Serv Replicated   Replicated CircleCI  Replicated 

- **:** CircleCI GitHub EnterpriseGitHub.com  CircleCI   GitHub  CircleCI    CircleCI GitHub CircleCI  CircleCI Git  Web  CircleCI  1  Git  Builder  

- **:**  CircleCI Amazon VPC    S3    

- **:** S3  

- **iOS :** CircleCI  iOS macOS      CircleCI  iOS 

- **Docker:** Docker Docker Engine Docker  [seccomp (  ) ](https://github.com/docker/engine/blob/e76380b67bcdeb289af66ec5d6412ea85063fc04/profiles/seccomp/default.json) CircleCI Docker  `seccomp`  

{% raw %}
```yaml
[
  {
    "comment": "",
    "names": [
      "clone",
      "setns",
      "unshare"
    ],
    "action": "SCMP_ACT_ALLOW",
    "args": [],
    "includes": {},
    "excludes": {}
  }
]
```
{% endraw %}

## 

  CircleCI 

CircleCI    

 [Audit Log ()]  CSV    JSON BLOB 

**:**   `id` 

###  
{:.no_toc}

<!-- TODO: automate this from event-cataloger -->     

`action` 

- context.create
- context.delete
- context.env_var.delete
- context.env_var.store
- project.env_var.create
- project.env_var.delete
- project.settings.update
- user.create
- user.logged_in
- user.logged_out
- workflow.job.approve
- workflow.job.finish
- workflow.job.scheduled
- workflow.job.start

###  
{:.no_toc}

- **action:**   ASCII   `workflow.job.start` 
- **actor:**   CircleCI   JSON BLOB `id`  `type`  `name` 
- **target:**   ()  JSON BLOB `id`  `type`  `name` 
- **payload:**  JSON BLOB payload  `action`  `version` 
- **occurred_at:**  UTC  9  ISO-8601  ('2017-12-21T13:50:54.474Z')
- **metadata:**   
- **id:**  UUID 
- **version:**   1 
- **scope:**  CircleCI    ID   JSON BLOB `id`  `type`  `name` 
- **success:** 
- **request:**  `id` (CircleCI  ID)`ip_address` ( IP  127.0.0.1  IPV4 ) `client_trace_id` ( HTTP X-Client-Trace-Id ID )  JSON BLOB 

## CircleCI 

CircleCI CircleCI ** 

-  ( )  
  -  ( )  
  - 
  - ** AWS  IAM  GitHub  [Machine User](https://developer.github.com/v3/guides/managing-deploy-keys/#machine-users) CircleCI  
-  stdout   
  -  stdout  `env`  `printenv` 
  - `echo`  
  -  
- VCS [](https://ja.wikipedia.org/wiki/) () 
-   []({{ site.baseurl }}/ja/2.0/contexts/#)
- SSH 
- VCS  2  (2FA)  ([Github 2FA](https://help.github.com/en/articles/securing-your-account-with-two-factor-authentication-2fa)[Bitbucket](https://confluence.atlassian.com/bitbucket/two-step-verification-777023203.html))  GitHub  Bitbucket 
-   CircleCI ** **** [ ]({{site.baseurl}}/ja/2.0/oss/#)

## 
{:.no_toc}

[GitHub  Bitbucket ]({{ site.baseurl }}/ja/2.0/gh-bb-integration/)
