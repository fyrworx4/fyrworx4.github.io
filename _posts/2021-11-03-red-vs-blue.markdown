---
title: Red vs. Blue - The Beginnings
layout: post
date: 2021-11-03 22:01
image: /assets/images/markdown.jpg
headerImage: false
tag:
- rvb
category: blog
author: taylornguyen
description: A cool experience
---

Red vs. Blue is an adversarial simulation competition to provide students with a unique, hands-on experience of defending Linux and Windows machines from an active threat actor. It’s modeled after the CCDC competition to allow students to get the feel and rigor of a cyber competition, integrated with business objectives.

And it’s free for everyone. No experience required.

This has been one of the most ambitious projects that our student organization, SWIFT, has ever taken on.

This was a large-scale project that involved an immense amount of collaboration since summer. Red vs. Blue required lots of concentration, troubleshooting, and all-nighters to get to this level of quality of a workshop - for students, by students.

Here's how we did it.

---

### The setup
Red vs. Blue was originally a training exercise/scrimmage for high school CyberPatriot teams who made it to Nationals, but last year our organization decided to make it available for college students as well. Preparing for this version of Red vs. Blue began in the summer.

### The theme and setting
My good friend Alex pitched a Star Wars themed idea, which we all enjoyed, so we went with a Star Wars theme.

### Networking
The networking for Red vs. Blue had undergone tons of development in short, this is what the topology looked like:

![Topology](../assets/images/red-vs-blue/RvB-Topology.png)

Each blue-team environment is called a **pod**. Each pod was connected to a pfSense router called a **pod router**, and the pod routers were connected together by another pfSense router called the **core router**.

All environment boxes on all pods need to be accessible with individual IP addresses, so 1:1 NAT was configured on each of the pod routers.

A red team network was added to the core network and consisted of Kali machines and the scoring engine.

All of this was done on a vSphere cluster.

### Vulnerable machines
Another good friend of mine, Gabe, led the creation of vulnerable and misconfigured machines. We had four machines in total:

- Windows Server 2012 (Communications)
- Windows 7 (Docking Bay)
- Ubuntu 20.04 (???)
- CentOS 7 (Engines)

Each machine contains services that were scored for uptime. We did our best to fit the environment with our theme, but it is still funny to imagine a futuristic Star Wars ship run a mail server in the engines.

### Scoring engine
The scoring engine, built from Python, scores service uptime by simulting users accessing business-critical services, such as using SSH to remotely log into an SSH server or initiating a RDP authentication request to an RDP server. [Here’s the repo.](https://github.com/fyrworx4/PulseEngine-ScoringEngine)

There were two components to the scoring engine - the user web interface and the pollers. Credits to Nathan and Silas for building/developing the user web interface (which you can access by going here). I worked with Gabe and a CCDC team member, Jacob, to add more capabilities to the scoring engine, such as scoring a MySQL and IRC server.

### The competition
Setting up the environment was a project of its own, but the logitstics of how the event is run needs to be planned. We needed to answer questions such as:

- How are teams created? How will teams communicate?
- How difficult should the competition be?
- How do we send out announcements?

We settled on Discord to manage everything, both the internal operations of Red vs. Blue and the communication for teams. Alex set up an Apache Guacamole instance as a jump box where competitiors can access their team environment, so we needed to explain the process of how to connect to the environment using Apache Guacamole, especially to those who have never heard of a jump box before.

### Lessons learned
Red vs. Blue was a very large project that took many hours to accomplish. But many of those hours were from the last two weeks before the event. I wished that we started earlier, because towards the competition, I had to start pinging everyone on Discord to update the team on the statuses on the boxes.

Personally, it gave me some insight on how to manage and delegate tasks. Working on Red vs. Blue has taught me a lot about patience and how to make sure that everyone’s on the same page.

Also, we need to be more clear on what the objectives are. We tend to overestimate the skill level of our members, so we need to remind ourselves that tasks that seem simple to us (such as disabling SMBv1) are brand new to others.

But this is a unique opportunity for students to gain competition-level experience outside of CCDC/CPTC. A great start to Red vs. Blue, but we can do better.