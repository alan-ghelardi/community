---
status: implementable
title: Pipeline Task Display Name
creation-date: '2021-01-28'
last-updated: '2022-01-04'
authors:
- '@itewk'
- '@abayer'
---

# TEP-0047: Pipeline Task Display Name
---


<!-- toc -->
- [Summary](#summary)
- [Motivation](#motivation)
  - [Goals](#goals)
  - [Non-Goals](#non-goals)
  - [Use Cases (optional)](#use-cases-optional)
- [Requirements](#requirements)
- [Proposal](#proposal)
  - [Notes/Caveats (optional)](#notescaveats-optional)
  - [Risks and Mitigations](#risks-and-mitigations)
  - [User Experience (optional)](#user-experience-optional)
  - [Performance (optional)](#performance-optional)
- [Design Details](#design-details)
- [Test Plan](#test-plan)
- [Design Evaluation](#design-evaluation)
- [Drawbacks](#drawbacks)
- [Alternatives](#alternatives)
- [Infrastructure Needed (optional)](#infrastructure-needed-optional)
- [Upgrade &amp; Migration Strategy (optional)](#upgrade--migration-strategy-optional)
- [References (optional)](#references-optional)
<!-- /toc -->

## Summary

A task in a Pipeline is currently represented in the UI (as observed in OpenShift 4.6)
using a field (`name`) that is meant to be machine readable, not human readable.
There should be the addition of a way to describe Pipeline tasks that are human readable
so that any tool that renders Tekton Pipeline can do so using a "human readable" field.

## Motivation

The end user of a Tekton pipeline can vary including but not limited to
application developer, to security professional, to compliance officer,
service reliability engineer, product manager, and beyond. The farther
you move away from the application developer the more important human
understanding of the CI/CD process is important.

Currently if a product manager or auditor was to look at a Tekton Pipeline run rendered in UI
that would be presented with a bunch of truncated machine readable task names, no spaces,
no special characters, no capitalization because the only option for tools to render these tasks
is the machine readable `Pipeline.spec.tasks.*.name` field.

Compare this to other tools in this space, Jenkins, GitLab CI, GitHub Actions, etc.
Their renderings of their workflows are meant to be human consumable. Their task names have
the option to be rendered in a human consumable format with use of any characters and fully
rendered for context.

### Goals

* Add a way to specify an optional display name for `Pipeline.spec.tasks.*.` items that allows
  any text and if provided will be useable by UIs rendering Tekton Piplines rather then the
  machine readable `Pipeline.spec.tasks.*.name` field.
* Add a way to specify a long form description for `Pipeline.spec.tasks.*.` items that allows for a
  long form description of a task in the context of a `Pipeline` to provide additional
  human context to the intent of a task in a Pipeline.
* Add a way to specify an optional display name for `Pipeline` objects that allows any text
  and if provided will be useable for UIs rendering Tekton `Pipeline` rather then the
  machine readable `Pipeline.name` field.
* Add a way to specify an optional display name for `Task` objects that allows any text
  and if provided will be useable for UIs rendering Tekton `Task` rather then the
  machine readable `Task.name` field.

### Non-Goals

* Display names or descriptions for `PipelineRun`s and `TaskRun`s.

### Use Cases (optional)

* Pipeline writers can optionally specify a display name for any/all tasks in a `Pipeline`.
* Pipeline writers can optionally specify a description for any/all tasks in a `Pipeline`.
* Pipeline writers can optionally specify a display name for a `Pipeline`.
* Pipeline writers can optionally specify a display name for a `Task`.

## Requirements

* New display name filed would be optional and accept any unicode character.
* New description field would be optional and accept any unicode character.

## Proposal

New fields are added to `Pipeline`, `Task`, and `PipelineTask` for display names, as well as
a new field on `PipelineTask` for description, matching the existing `Description` field on 
`Pipeline` and `Task`.

### Notes/Caveats (optional)

None.

### Risks and Mitigations

1. Tools that render Tekton pipelines will need to be updated to take advantage of the new
fields once they are available.

### User Experience (optional)

None.

### Performance (optional)

There will be a slight increase in CRD size when the new field(s) are used, but nothing significant.

## Design Details

No real design is needed here beyond adding the fields.

## Test Plan

N/A

## Design Evaluation

None.

## Drawbacks

None.

## Alternatives

TBD

## Infrastructure Needed (optional)

None.

## Upgrade & Migration Strategy (optional)

None.

## References (optional)

https://github.com/tektoncd/pipeline/issues/3466#issuecomment-767786717
