## GitLab CI/CD `workflow` keyword
the top-level `workflow` keyword is used to define a set of rules that apply to
pipelines in general as opposed to specific jobs. 

### `Workflow` Syntax in **.gitlab-ci.yml**
```yaml
workflow:
  rules:
    - if: <condition>
      when: <on_condition>
```
 ### Explanation of Keywords

| Key         | Description                                                                      |
| ----------- | -------------------------------------------------------------------------------- |
| `workflow:` | Top-level keyword in `.gitlab-ci.yml` file                                       |
| `rules:`    | List of conditions that determine if the pipeline should run                     |
| `if:`       | Condition written as a string (using GitLab CI/CD predefined variables)          |
| `when:`     | Outcome if the `if` condition is true: `always` (run pipeline) or `never` (skip) | 

### Some example `if` clauses for `workflow: rules:` 
| Key                                                | Description                                            |
| -------------------------------------------------- | ------------------------------------------------------ |
| `if: '$CI_PIPELINE_SOURCE == "merge_request_event"'` | Control when merge request pipelinescrun.            |
| `if: '$CI_PIPELINE_SOURCE == "push"'`         | Control when both branch pipelines and tag pipelines run.  |
| `if: $CI_COMMIT_TAG`                                 | Control when tag pipelines run.                      |
| `if: $CI_COMMIT_BRANCH`                              | 	Control when branch pipelines run.      |

### Interactions between `workflows` and `rules`

A workflow can have an optional name along with a required rules section. Rules in
a workflow are similar to those used in a specific job with some exceptions. The “when”
option can only have the values always or never. Also, you **cannot use** the “allow_failure”
option in a workflow rule. The main use case for a workflow is to restrict a pipeline to
be either a branch pipeline or a merge request pipeline.
So how, then, do workflow rules work with job-specific rules? The workflow rules are applied first. When a workflow rule matches, the jobspecific rules are then applied; if no workflow rule matches, the job for that pipeline type is removed. To think of it another way, both a workflow rule and a job-specific rule must
match for a job to be executed.

### Example
```yaml
workflow:
  rules:
    # Run only if the pipeline is triggered by a merge request
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
      when: always

    # Run only if the commit is a tag (e.g., v1.0.0)
    - if: '$CI_COMMIT_TAG'
      when: always

    # Run on default branch (usually 'main' or 'master')
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
      when: always

    # Fallback: skip pipeline for everything else, If none of the above rules match, this one will apply
    - when: never
```    

GitLab applies these `rules:` from top to bottom. The first matching rule wins, and the rest are ignored.
