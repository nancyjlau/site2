---
title: Improving Open Ended Model Exploration in Security Contexts
description: This is a working log with periodic updates.
slug: model-exploration
date: 2025-10-30 00:00:00+0000
categories:
    - model exploration
#weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Hi, this is a working log with periodic updates.

I've been working with a 300 hour dataset collected from real time red/blue team defense logs in a real life setup from a cybersecurity competition. 

We have:
\- 10 teams x 6 snapshots x 2 systems (Windows DC and Linux Wordpress)
\- ~70 GB of Windows Plaso forensic timelines
\- ~200k+ events per team 

| Data         |                  |                                |
|------------------------|------------------|--------------------------------|
| **System**             | **Collection Tool** | **Data Type**               |
| Windows (Bluecheese)   | Velociraptor     | Plaso forensic timelines       |
| Linux (Oaxaca)         | CyLR             | Syslog, Apache access/error logs |

From the logs, we can see red team activity, such as behaviors like XSS injection attempts on the WordPress login, path traversal attacks, SQL injection probes, web shell hunting (/sysShell, /webshell4), and CVE scanning.

All of this data is pretty good data that I haven't been able to find anywhere else. I have no idea how to create clear tasks out of this, but I'm going to try to go with doing RLER from the [DR Tulu](https://arxiv.org/abs/2511.19399) paper.

Possible ideas:
