---
layout: page
title: "A Summary of MettleCI Components"
permalink: /install
---

# A Summary of MettleCI Components

A summary of all of the components referenced in MettleCI Topology
diagrams.

# DataStage Environments

MettleCI works with all versions of DataStage from v9.2 onwards. This
covers both…

-   Traditional non-Cloud Pak versions of DataStage up to version
    11.7.x. (often referrred to as ‘standalone’ DataStage), and

-   DataStage running within an IBM Cloud Pak for Data environment

Note that MettleCI can also work with some versions of DataStage prior
to v9.2, but with some reductions in capability, dependent upon how old
you particular version is.

# MettleCI Workbench Service

This service provides an HTTP/S endpoint through which users access the
MettleC Workbench browser-based application. This service exchanges a
unit test files with the MettleCI Unit Test Harness which can only be
installed on the Engine tier. For this reason the MettleCI Workbench
Service requires a shared filesystem with the MettleCI Unit Test
Harness. For non-Cloud Pak instances of DataStage the easiest way of
achieving this is to install the MettleCI Workbench Service on the
DataStage Engine tier, co-resident with the MettleCI Unit Test Harness.

# MettleCI Workbench Host

For Cloud Pak DataStage instances it is not possible to install the
MettleCI Workbench Service on the DataStage Engine tier so the MettleCI
Workbench Service needs to be installed on a separate, dedicated host
which is configured to communicate with the Cloud Pak DataStage
Conductor node, both over HTTPS and via a shared network file system.

# MettleCI Command Line Interface

The MettleCI Command Line Interface (CLI) provides a suite of automation
capabilities which are used by your build tool’s Agent/Runner to
implement an automated Continue Integration and Deployment pipeline. It
comprises a lightweight ‘Command Shell’ which provides a command line
interface with no functionality, and a suite of ‘plugins’ which provide
the actual commands used to build your pipeline. The example pipelines
shipped with MettleCI

# MettleCI Agent Host

The MettleCI Agent Host is a dedicated Microsoft Windows host running
three components: A DataStage Client tier, a MettleCI CLI, and your
chosen CI/CD agent/runner.

For more information on this host see
<a href="The_Mettle_Agent_Host" data-linked-resource-id="2327019539"
data-linked-resource-version="4" data-linked-resource-type="page">The
Mettle Agent Host</a>.

# Application Lifecycle Management Tools

The Application Lifecycle Management (ALM) tools are a classification of
user-selected tools providing the following capabilities:

-   Work Item Management (WIM), such as Atlassian Jira,

-   Git repository, such as GitHib or Atlassian Bitbucket,

-   CI/CD build and deployment tool, such as Jenkins or Atlassian
    Bamboo.

Different tools provide different combinations of these capabilities
within the same platform. For example,

|                  |                    |                          |                    |
|------------------|--------------------|--------------------------|--------------------|
|                  | **Git Repository** | **Work Item Management** | **CI/CD Pipeline** |
| **Atlassian**    | ✅ (via Bitbucket) | ✅ (via Jira)            | ✅ (via Bamboo)    |
| **Azure DevOps** | ✅                 | ✅                       | ✅                 |
| **GitHub**       | ✅                 | ✅                       | ✅                 |
| **GitLab**       | ✅                 | ✅                       | ✅                 |
| **Jenkins**      | ⛔️                 | ⛔️                       | ✅                 |
