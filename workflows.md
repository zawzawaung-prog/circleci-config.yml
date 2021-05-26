---
layout: classic-docs
title: ""
short-title: ""
description: ""
order: 30
---

![]({{ site.baseurl }}/assets/img/docs/wf-header.png)

 

- 
{:toc}

## 

****  



-  
- 
-  
- 

 1   **

### 
{:.no_toc}



- RUNNING: 
- NOT RUN: 
- CANCELLED: 
- FAILING:  1  ( 1  Failing)
- FAILED:  1  (  1  )
- SUCCESS: 
- ON HOLD: 
- NEEDS SETUP:  [config.yml]({{ site.baseurl }}/ja/2.0/configuration-reference/)  

### 
{:.no_toc}

CircleCI API  API  **:** `build` 

[]({{ site.baseurl }}/ja/2.0/faq) 

## 

`workflows` ***CircleCI [workflows]({{ site.baseurl }}/ja/2.0/configuration-reference/#workflows)*

**:** Docker `run`  `.circleci/config.yml` [YAML  ](http://yaml.org/spec/1.2/spec.html#id2765878) [Reuse YAML in the CircleCI Config (CircleCI  YAML )](https://circleci.com/blog/circleci-hacks-reuse-yaml-in-your-circleci-config-with-yaml/)

 `.circleci/config.yml`  `workflows:`   `.circleci/config.yml` 2   `build_and_test`  `workflows:`  `jobs:`  

```yaml
jobs:
  build:
    docker:
      - image: circleci/<language>:<version TAG>
    steps:
      - checkout
      - run: <command>
  test:
    docker:
      - image: circleci/<language>:<version TAG>
    steps:
      - checkout
      - run: <command>
workflows:
  version: 2
  build_and_test:
    jobs:
      - build
      - test
```

[](https://github.com/CircleCI-Public/circleci-demo-workflows/blob/parallel-jobs/.circleci/config.yml)

## 

   

-  lint 
- ** setup 

[]({{ site.baseurl }}/ja/2.0/optimizations)[]({{ site.baseurl }}/ja/2.0/adv-config)

### 
{:.no_toc}

4  

![]({{ site.baseurl }}/assets/img/docs/sequential_workflow.png)

 `config.yml` 

```yaml
workflows:
  version: 2
  build-test-and-deploy:
    jobs:
      - build
      - test1:
          requires:
            - build
      - test2:
          requires:
            - test1
      - deploy:
          requires:
            - test2
```

 `requires:`  `deploy:` `build``test1``test2`    `deploy`  `test2` `test2`  `test1` `test1`  `build` 

[](https://github.com/CircleCI-Public/circleci-demo-workflows/blob/sequential-branch-filter/.circleci/config.yml)

### 
{:.no_toc}

   

![]({{ site.baseurl }}/assets/img/docs/fan-out-in.png)

 `config.yml` 

```yaml
workflows:
  version: 2
  build_accept_deploy:
    jobs:
      - build
      - acceptance_test_1:
          requires:
            - build
      - acceptance_test_2:
          requires:
            - build
      - acceptance_test_3:
          requires:
            - build
      - acceptance_test_4:
          requires:
            - build
      - deploy:
          requires:
            - acceptance_test_1
            - acceptance_test_2
            - acceptance_test_3
            - acceptance_test_4
```

`build` 4   `deploy` 4  

[](https://github.com/CircleCI-Public/circleci-demo-workflows/tree/fan-in-fan-out)

## 

 [Approval ()]  `type: approval`  `jobs`  

```yaml
# ...
# << buildtest1test2deploy  >>
# ...

workflows:
  version: 2
  build-test-and-approval-deploy:
    jobs:

      - build  #  
      - test1: #    1 
          requires: # `build` test1 
            - build
      - test2: #    2 
          requires: # test2  `test1` 
            - test1
      - hold: # <<< CircleCI Web 
          type: approval # <<<  "On Hold" 
          requires: # test2  "hold" 
           - test2
      # `hold` `hold` 
      #  
      - deploy:
          requires:
            - hold
```

CircleCI  [Workflows ()]  `hold` [Approve ()] `deploy:`   `hold` 



- `approval` `workflow` ****
- `hold` 
-  `build`  `test1`  `type: approval` 
- `type: approval` `wait``pause` 
-  `require:` **  `deploy:` 
-  `type: approval` 

`request-testing` 

![]({{ site.baseurl }}/assets/img/docs/approval_job.png)

`request-testing`  

![]({{ site.baseurl }}/assets/img/docs/approval_job_cloud.png)

## 

  

 `triggers`  `triggers` `workflows` **** UTC  `cron` 

**:** CircleCI v2.1    

### 
{:.no_toc}

`git push`   `triggers` `schedule` 

`nightly`  0  (UTC)  `cron` POSIX `crontab` `cron` [crontab  man ](https://www.unix.com/man-page/POSIX/1posix/crontab/) `master`  `beta` 

**:**  15   0  (UTC)  

```yaml
workflows:
  version: 2
  commit:
    jobs:
      - test
      - deploy
  nightly:
    triggers:
      - schedule:
          cron: "0 0 * * *"
          filters:
            branches:
              only:
                - master
                - beta
    jobs:
      - coverage
```

 `commit`  `triggers` `git push`  `nightly`  `triggers` `schedule` 

### 
{:.no_toc}

 `schedule` `cron`  `filters` 

`cron` [ crontab ](https://crontab.guru/)

**:** cron  (`*/1``*/20`) **** ****

`filters` 

CircleCI [branches ]({{ site.baseurl }}/ja/2.0/configuration-reference/#branches-1)

[](https://github.com/CircleCI-Public/circleci-demo-workflows/blob/try-schedule-workflow/.circleci/config.yml)

## 



###  
{:.no_toc}

 4  []({{ site.baseurl }}/ja/2.0/contexts)

 `config.yml` `org-global`  

```yaml
workflows:
  version: 2
  build-test-and-deploy:
    jobs:
      - build
      - test1:
          requires:
            - build
          context: org-global
      - test2:
          requires:
            - test1
          context: org-global
      - deploy:
          requires:
            - test2
```

`context`  `org-global`   `test1`  `test2`  

### 
{:.no_toc}

3  (DevStagePre-Prod)   `jobs`  `branches`  `config.yml`  

![]({{ site.baseurl }}/assets/img/docs/branch_level.png)

 `config.yml` 

```yaml
workflows:
  version: 2
  dev_stage_pre-prod:
    jobs:
      - test_dev:
          filters:  # 
            branches:
              only:  # 
                - dev
                - /user-.*/
      - test_stage:
          filters:
            branches:
              only: stage
      - test_pre-prod:
          filters:
            branches:
              only: /pre-prod(?:-.+)?$/
```

[](#)

  [](https://github.com/CircleCI-Public/circleci-demo-workflows/blob/sequential-branch-filter/.circleci/config.yml)

### Git 
{:.no_toc}

 CircleCI   () [](#)  

2 

- `untagged-build`:  `build` 
- `tagged-build`: **** `v`  `build` 

```yaml
workflows:
  version: 2
  untagged-build:
    jobs:
      - build
  tagged-build:
    jobs:
      - build:
          filters:
            tags:
              only: /^v.*/
```

`build-n-deploy`  2 

- `build`: 
- `deploy`: 'v' 

```yaml
workflows:
  version: 2
  build-n-deploy:
    jobs:
      - build:
          filters:  # `deploy`   `build` 
            tags:
              only: /.*/
      - deploy:
          requires:
            - build
          filters:
            tags:
              only: /^v.*/
            branches:
              ignore: /.*/
```

`build-test-deploy`  3 

- `build`:  'config-test' 
- `test`:  'config-test' 
- `deploy`: 'config-test' 

```yaml
workflows:
  version: 2
  build-test-deploy:
    jobs:
      - build:
          filters:  # `test`   `build` 
            tags:
              only: /^config-test.*/
      - test:
          requires:
            - build
          filters:  # `deploy`   `test` 
            tags:
              only: /^config-test.*/
      - deploy:
          requires:
            - test
          filters:
            tags:
              only: /^config-test.*/
            branches:
              ignore: /.*/
```

**:** GitHub  Web  [ 5 MB](https://developer.github.com/webhooks/#payloads) [](https://developer.github.com/v3/activity/events/types/#createevent) 3  CircleCI 

### 
{:.no_toc}

CircleCI  Java   CircleCI 

`only: /^config-test/`  `config-test`  `config-test`  `only: /^config-test.*/` 

  2.1   3-7 `/^version-2\.1\.[3-7]/` 

  [java.util.regex ](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html)

## 

 1             

![ ]({{ site.baseurl }}/assets/img/docs/workspaces.png)

    

Scala   CPU  Scala   CPU      Scala 

2 jar  `build`   `build` `integration-test``unit-test``code-coverage` jar 

`persist_to_workspace`  `persist_to_workspace`  `paths:` `root`   () 

`attach_workspace`   `config.yml`  2 `downstream`  `flow`  `downstream`  `flow` 

```yaml
# CircleCI 2.1  Executor 
#  Docker 
# https://circleci.com/ja/docs/2.0/reusing-config/#-executors- 

version: 2.1

executors:
  my-executor:
    docker:

      - image: buildpack-deps:jessie
    working_directory: /tmp

jobs:
  flow:
    executor: my-executor
    steps:

      - run: mkdir -p workspace
      - run: echo "Hello, world!" > workspace/echo-output

      #   (workspace/echo-output) 

      - persist_to_workspace:
          #  working_directory  
      #  
          root: workspace
          # 
          paths:
            - echo-output

  downstream:
    executor: my-executor
    steps:

      - attach_workspace:
          # working_directory 
          at: /tmp/workspace

      - run: |
          if [[ `cat /tmp/workspace/echo-output` == "Hello, world!" ]]; then
            echo "It worked!";
          else
            echo "Nope!"; exit 1
          fi

workflows:
  version: 2

  btd:
    jobs:

      - flow
      - downstream:
          requires:
            - flow
```

  CircleCI  [`config.yml`](https://github.com/circleci/circleci-docs/blob/master/.circleci/config.yml) 

[Persisting Data in Workflows: When to Use Caching, Artifacts, and Workspaces (: )](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/)

## 

 **** **[Workflows ()]** **[Rerun ()]** [**Rerun from failed ()**] 

![CircleCI  ]({{ site.baseurl }}/assets/img/docs/rerun-from-failed.png)

## 



### 
{:.no_toc}

()    

### 
{:.no_toc}

`config.yml` 

 

CircleCI  (* *)  

  URL 

`https://circleci.com/:VCS/:ORG/:PROJECT`

  URL 

`https://circleci.com/:VCS/:ORG/workflows/:PROJECT`

NEEDS SETUP ()

![]({{ site.baseurl }}/assets/img/docs/workflow-config-error.png)

### GitHub 
{:.no_toc}

GitHub  GitHub   `ci/circleci`   CircleCI 1.0 

![GitHub  ]({{ site.baseurl }}/assets/img/docs/github_branches_status.png)

`ci/circleci` GitHub CircleCI  GitHub 

GitHub  [Settings ()] > [Branches ()]  [Edit ()]  (: https://github.com/your-org/project/settings/branches)

## 
{:.no_toc}

- 1.0 `circle.yml`  2.0 `.circleci/config.yml` [1.0  2.0 ]({{ site.baseurl }}/ja/2.0/migrating-from-1-2/)

- []({{ site.baseurl }}/ja/2.0/faq) 

-  GitHub  [CircleCI  ](https://github.com/CircleCI-Public/circleci-demo-workflows)

## : 
{:.no_toc}

<iframe width="560" height="315" src="https://www.youtube.com/embed/3V84yEz6HwA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen mark="crwd-mark"></iframe>

### : 
{:.no_toc}

<iframe width="560" height="315" src="https://www.youtube.com/embed/FCiMD6Gq34M" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen mark="crwd-mark"></iframe>
