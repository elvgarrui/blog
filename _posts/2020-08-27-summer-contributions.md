---
layout: post
title: "My journey at Linux System Roles"
tags: gsoc linux-system-roles floss
author:
- Elvira G.
meta: "GSOC"
---


Linux System Roles are a collection of roles and modules that assist Linux administrators in the configuration of GNU/Linux subsystems through Ansible. There are roles for managing different parts of the systems: selinux, storage, network...

### Improving the Network Linux System Role

My main objective was to improve the Network Linux System Role. Although the
proposal covered the many different tasks that were proposed for the project, my
mentors and I decided to better focus on improving the integration testing of
the project. Therefore, most of my contributions were related to this matter,
being the addition of Pytest as integration testing tool the most remarkable
addition to the project. Below you can see the detailed list of contributions:

#### Merged PRs

Started before 1st May, 2020:

- [**PR207 - Separate debug and info logs from
  warnings**](https://github.com/linux-system-roles/network/pull/207): Fixes
[Issue 29](https://github.com/linux-system-roles/network/issues/29).

After 1st May, 2020:
- [**PR226 -  Update contributing.md with steps to
  contributing**](https://github.com/linux-system-roles/network/pull/226).

- [**PR223 - Change ethtool features to use
  underscores**](https://github.com/linux-system-roles/network/pull/223).
Refers to [Issue
206](https://github.com/linux-system-roles/network/issues/206). The role now
accepts properties written with underscores or dashes, and fail if both options
are mixed.

- [**PR237 - Fail if state and persistent_state are
  incompatible**](https://github.com/linux-system-roles/network/pull/237):
Fixes [Issue 205](https://github.com/linux-system-roles/network/issues/205).

- [**PR251 - Fix error message format**](https://github.com/linux-system-roles/network/pull/251).
 
- [**PR260 - Add Pytest integration
  tests**](https://github.com/linux-system-roles/network/pull/260): This PR
contains two different commits. The first one creates the script for testing
and the [mocking of the Ansible
runtime](http://elviragruiz.net/2020/07/20/mocking-ansible-python.html). The
second one consist of playbooks that allow the Pytest run in the project
internal test-harness. The test harness allows the execution of these tests in
Linux distributions, with different versions CentOS, Fedora and RHEL.

### Todo

There are some tasks that still need to be finished. The most important is to
add Python 2 support to the Pytest integration testing. After that, I also want to finish [Issue
206](https://github.com/linux-system-roles/network/issues/206).

### 🌤️  Summer is ending... 🌤️ 

It has been an intense but rewarding summer, and I feel like I've learnt a lot. I've been able to work directly with awesome professionals. I'm willing to continue contributing to Linux System Roles and to improve my skills as a software engineer!!

*Thanks to Fedora and all the mentors. Thanks to Till for being so understanding and patient with me. I really appreciate all the time you have dedicated to my mentoring.*
