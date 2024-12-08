---
title: Red vs. Blue - Red Team Bottlenecking
layout: post
date: 2023-10-31 19:00
image: /assets/images/markdown.jpg
headerImage: false
tag:
- competitions
category: blog
author: taylornguyen
description: asdfasdfasdf
---

<p align="center">
  <img src="https://media.discordapp.net/attachments/754129859554443286/1307788955181256805/image.png?ex=6755f2e0&is=6754a160&hm=360095328a2c0f7e3bef9c3aa44d070ed91dad0ac69281cc49eb601e8d442619&=&format=webp&quality=lossless" width="50%"/>
  <em>We had just under 2000 beacons</em>
</p>


It's been a while since I've posted about Red vs. Blue, but for a pretty good reason - I'm not actively developing RvB since I graduated. But I like to help out as a red teamer and also like to spend time developing new tooling to make life easier as a RTer in RvB. I've taken some sort of lead role and am the main guy to set up infra before competition and represent the red team to the rest of the organizers.

One of the issues that RvB deals with is lack of RTers, or should I say, _experienced_ red teamers. We took a bit hit during Fall 2024 RvB, where most of the designated red teamers were out competing in CPTC that very same day. We only have 5-6 people attacking 4 boxes x 12ish teams, so we were massively understaffed. Some folks from the dev team and SWIFT eboard volunteered to be red teamers, and they were pretty green with the workflow for red teaming.

How did the event pan out? Not bad, but I had some good lessons learned.

## Red Teaming - RvB vs HTB

Red teaming for RvB is really different than doing HackTheBox or TryHackMe - it's more of a post-exploitation/automation/defense evasion challenge, rather than initial access/privesc exploration.

Yes, you kinda need to know the basics of red teaming, so doing some HTB or THM is required. For example:
- Using psexec/smbexec/evil-winrm to gain CLI access into Windows box
- Obtaining reverse shells for both OS's
- Familiarity with CLI for both Windows and Linux (since you most likely won't use RDP to gain RCE)
- NMAP against teams to check for firewall status
- Some enumeration on web apps or other stuff, mainly checking low hanging fruits

<p align="center">
  <img src="https://i.postimg.cc/X7nKvPr1/SCR-20241207-suql.png" width="50%"/>
</p>

However we're not really trying to uncover the tiniest of misconfigurations, like you'd do on HTB/THM. The RvB environment is ripe with misconfigurations and vulnerabilities that are designed for easy initial access. We're _expecting_ low-hanging fruit vulns. Even more, we also get the default admin creds at the same time as the blue teams, so we can prepare commands and scripts to use.

## Michael, the guinea pig

I was catching up with my buddy Michael a couple of weeks prior to the event, and I invited him to be a red teamer for this event. Althought he leaned more into IT/sysadmin stuff for work, he accepted the invite, and I had an entire study plan to get him up to speed. We focused on Windows exploitation for him.

It was basically split into the following activities:

- C2 Team Server basics and operations
  - Connecting to the Team Server
  - Setting Up Listeners
  - Generating Beacons
  - Obtaining Callbacks
- Red Team Tooling for RvB
  - Evil-WinRM/psexec to interact with Windows machines via CLI
  - Netexec to run one-liners against one machine, and then many machines at once
  - The above, but with PTH
- Low-hanging fruit stuff
  - DCSync
  - ZeroLogon
- RvB 1v1 Scrimmage
  - Michael would be the red teamer, going against an actual RvB competitior as some sort of practice round

He got pretty comfortable with the techniques - to the level where he can do things on his own in an actual RvB setting without much assistance. (the goal with this study plan)

## Other Preparation

We had other RTers that were also more comfortable with Windows, but no Linux people. So I decided to focus on Linux for this comp. Linux pentesting was more of my weak spot, and when it comes to persistence/defense evasion I knew some basic stuff but the commands can get pretty granular.

I ended up using Mythic as the C2 server for Linux environments, now that it came with a "run a command on all beacons" feature, and spent a good amount of time setting up infra and Kali instances for the red teamers.

Two of the eboard folks volunteered to help out with red teaming, albeit a bit too late. We didn't really have time to go thru an entire study plan like I did with Michael, so I had to figure out what they knew already and how to utilize their existing knowledge as best as possible, such as having them focus in port scanning and interacting with Mythic to turn off services, while I worked on more complex tasks such a website defacement and persistence across all teams.

## Competition

While I was able to get Linux beacons easily, I think I spent way too much time troubleshooting Windows stuff. Some of our automation stuff for Mythic didn't work so I was like "oh well". I mean the most we did was turn off services. It was difficult to do team-specific hax because, well, my focus was thinnly spread across all teams.

As the primary operator for Linux stuff, my attention was 100% focused on RvB red teaming. I wish I could have been more helpful with guiding the newer folks, but it was near impossible to do.

Part of being lead is helping the newer folks to be more comfortable with the red teaming process, since maybe they can develop a genuine interest and contribute more next comp, and honestly it feels really good to overpower the blue teamers in these settings. Also it's just a really good skill to have, and immensely helps with overall security knowledge.

## Lessons Learned

As a lead, you can either:
- Do active operations
- Guide newer people learn more about red teaming

Not both.

## If you want to red team...

then decide early on, because there are people that are willing to help! It just takes a lot of time to get you up to speed and comfortable with the techniques, and it is not as difficult as you think!

