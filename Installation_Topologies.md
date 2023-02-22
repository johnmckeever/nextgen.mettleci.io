---
layout: page
title: "Installation Topologies"
permalink: /install
---

# Installation Topologies

These pages summarise some (but not all) possible MettleCI deployment
topologies.

## [A Summary of MettleCI Components](A_Summary_of_MettleCI_Components)

A summary of all of the components referenced in MettleCI Topology
diagrams.

## <a href="MettleCI_requirements_when_upgrading_DataStage_to_v11.7"
data-linked-resource-id="2193358849" data-linked-resource-version="4"
data-linked-resource-type="page">MettleCI requirements when upgrading
DataStage to v11.7</a>

When upgrading to the latest non-Cloud Pak version of DataStage you’ll
wonder which MettleCI tools and assets need to be upgraded, replaced, or
reconfigured, and which can be safely left in place. This page discusses
the technical aspects of re-configuration and will deliberately omit the
important project management aspects of handling a cutover between old
and new DataStage environments.

## <a
href="Standalone_DataStage_on_Different_Versions_-_Concurrent_use_for_upgrades"
data-linked-resource-id="1984397313" data-linked-resource-version="9"
data-linked-resource-type="page">Standalone DataStage on Different
Versions - Concurrent use for upgrades</a>

A hybrid environment featuring two DataStage platforms:

1.  A traditional standalone DataStage environment on v11.5.0 (for
    example), and

2.  A traditional standalone DataStage environment on v11.7.1 (for
    example)

Each environment has its own dedicated MettleCI Agent running on a
dedicated Windows host.

This topology is ideal for customers using MettleCI to upgrade between
different versions of Standalone DataStage.

## <a href="Standalone_DataStage_on_Unix_-_Dedicated_Agent_Host"
data-linked-resource-id="1633845302" data-linked-resource-version="5"
data-linked-resource-type="page">Standalone DataStage on Unix -
Dedicated Agent Host</a>

A Unix-based multi-tier DataStage environment where…

-   The MettleCI Workstation is installed on your DataStage Engine tier,
    and

-   The MettleCI Agent is installed on a dedicated Windows host

## <a href="Standalone_DataStage_on_Windows_-_Consolidated_Agent_Host"
data-linked-resource-id="1633812481" data-linked-resource-version="4"
data-linked-resource-type="page">Standalone DataStage on Windows -
Consolidated Agent Host</a>

A Windows-only single-tier DataStage environment where…

-   The MettleCI Workstation is installed on your DataStage Engine tier,
    and

-   The MettleCI Agent is installed on your DataStage Engine tier.

**This topology may find some applications in POC or Demo environment,
but is <u>not recommended</u> for real-world DataStage development.**

## <a href="Standalone_DataStage_on_Windows_-_Dedicated_Agent_Host"
data-linked-resource-id="1630928930" data-linked-resource-version="9"
data-linked-resource-type="page">Standalone DataStage on Windows -
Dedicated Agent Host</a>

A Windows-only multi-tier DataStage environment where…

-   The MettleCI Agent is installed

-   The MettleCI Workstation is installed on your Windows-based
    DataStage Engine tier, and

-   The MettleCI Agent is installed on a separate, dedicated Windows
    host

## <a href="The_Mettle_Agent_Host" data-linked-resource-id="2327019539"
data-linked-resource-version="4" data-linked-resource-type="page">The
Mettle Agent Host</a>

The MettleCI Agent Host is a dedicated Microsoft Windows host which is
used to run three major components:

-   A <a
    href="https://www.ibm.com/docs/en/iis/11.7?topic=components-client-tier"
    rel="nofollow">DataStage Client tier</a>,

## <a href="Using_Multiple_MettleCI_Agents"
data-linked-resource-id="1766817793" data-linked-resource-version="5"
data-linked-resource-type="page">Using Multiple MettleCI Agents</a>

Many customers cannot use a single MettleCI Agent Host to communicate
with multiple DataStage environments due to organizational security
policies.

This page describes how multiple MettleCI Agents Host can be configured
when you need to segregate agent access by DataStage environment or
network zone.

## <a href="Virtual_Desktop_Example_Topology"
data-linked-resource-id="2257911823" data-linked-resource-version="9"
data-linked-resource-type="page">Virtual Desktop Example Topology</a>

An example topology for an environment using the following technologies:

-   Citrix desktop virtualisation

-   Atlassian Bitbucket Git repository

-   Atlassian Jira work item management platform

-   Jenkins build tool
