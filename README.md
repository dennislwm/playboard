# playboard

<h1 align="center" style="border-bottom: none;">playboard</h1>
<h3 align="center">An automated process to save URLs of web sites and consume them using an RSS reader.</h3>
<br />
<p align="center">
  <p align="center">
    <a href="https://github.com/dennislwm/playboard/issues/new?template=bug_report.yml">Bug report</a>
    ·
    <a href="https://github.com/dennislwm/playboard/issues/new?template=feature_request.yml">Feature request</a>
    ·
    <a href="https://github.com/dennislwm/playboard/wiki">Read Docs</a>
  </p>
</p>
<br />

---

![GitHub repo size](https://img.shields.io/github/repo-size/dennislwm/playboard?style=plastic)
![GitHub language count](https://img.shields.io/github/languages/count/dennislwm/playboard?style=plastic)
![GitHub top language](https://img.shields.io/github/languages/top/dennislwm/playboard?style=plastic)
![GitHub last commit](https://img.shields.io/github/last-commit/dennislwm/playboard?color=red&style=plastic)
![Visitors count](https://hits.sh/github.com/dennislwm/playboard/hits.svg)
![GitHub stars](https://img.shields.io/github/stars/dennislwm/playboard?style=social)
![GitHub forks](https://img.shields.io/github/forks/dennislwm/playboard?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/dennislwm/playboard?style=social)
![GitHub followers](https://img.shields.io/github/followers/dennislwm?style=social)

## Purpose

This document describes the `playboard` automated process to save URLs of web sites and consume them using an RSS reader.

## Audience

The audience for this document includes:

* Mobile User who will send messages, via Bookmarklet or Email, and consume RSS feeds on their iPhone device.

* Mac User who will send messages, via Bookmarklet or Email, consume RSS feeds, and query text from an archive on their workstation.

* DevSecOps Engineer who will design system workflows, configure any SaaS or selfhosted services, and plan for disaster recovery.

## Why `playboard`?

1. Previously, there wasn't a systematic workflow to send a URL of an article (message), consume and save the message, which can then be queried using a search tool. The methods of sending a message via an Email, WhatsApp or Telegram led to a message sprawl.

2. As an analogy, you have a system of sending messages to one or more queues based on the Tags. A Tag represents a queue, such that a message can be tagged to one or more Tags, hence it is fanned out to multiple queues. Messages in queues can be consumed as separate RSS feeds using Tags. For example, if a message is tagged with `Github`, then it will be appended to the RSS feed with `t:Github`.

3. You have two methods of sending messages, either by Email or Bookmarklet, and on different devices, such as iPhone device or Mac workstation. This flexibility allows you to be more productive as you do not need to be in front of a workstation in order to send messages.

4. The messages are sent to a SaaS application (**Pinboard.in**), hence you don't have to manage the server or application. However, you are still responsible for disaster recovery. The SaaS application is a paid service that has two tiers: Standard (USD $22) and Pro (USD $39). The Pro tier includes a backup of your data on their cloud server for disaster recovery.

5. Currently, there isn't an automated process to save pages of individual Bookmarks as a PDF file. However, as the Bookmarks are consumed from RSS feeds, it is possible to automate this process.

6. In order to search the content of your PDF archive, you have to index and query the text using a MacOS application (**Recoll**). The search function is not available online as the application runs on your workstation.

7. For disaster recovery, you have the option Backup & Restore only, as the service relies on a third-party SaaS application. Using the 3-2-1 backup strategy, you should always have 3 copies of your data, i.e. (1) your production data on the SaaS application (**Pinboard.in**), (2) a primary backup copy on your repository (this **GitHub.com** repo), and (3) a secondary backup copy on another site (TO DO).

## Limitations

This project has several limitations that may hinder your workflow.

* There isn't an automated process to save pages of individual Bookmarks as a PDF file from your RSS feeds. However, we can use a CLI (**wkhtmltopdf**) to facilitate this automation.
* The search function is not available online as the application (**Recoll**) runs on your workstation.
* There is no secondary backup data site for disaster recovery.
* The Recovery Point Objective (RPO) for the Backup & Restore disaster recovery plan is ONE (1) day, however you can configure the CI pipeline to run more frequently.

## Getting Started 🚀

We have a thorough guide on how to set up and get started with `playboard` in our [documentation](https://github.com/dennislwm/playboard/wiki).

## Bugs or Requests 🐛

If you encounter any problems feel free to open an [issue](https://github.com/dennislwm/playboard/issues/new?template=bug_report.yml). If you feel the project is missing a feature, please raise a [ticket](https://github.com/dennislwm/playboard/issues/new?template=feature_request.yml) on GitHub and I'll look into it. Pull requests are also welcome.

## 📫 How to reach me
<p>
<a href="https://www.linkedin.com/in/dennislwm"><img src="https://img.shields.io/badge/LinkedIn-blue?style=for-the-badge&logo=linkedin&labelColor=blue" height=25></a>
<a href="https://twitter.com/hypowork"><img src="https://img.shields.io/badge/twitter-%231DA1F2.svg?&style=for-the-badge&logo=twitter&logoColor=white" height=25></a>
<a href="https://leetradetitan.medium.com"><img src="https://img.shields.io/badge/medium-%2312100E.svg?&style=for-the-badge&logo=medium&logoColor=white" height=25></a>
<a href="https://dev.to/dennislwm"><img src="https://img.shields.io/badge/DEV.TO-%230A0A0A.svg?&style=for-the-badge&logo=dev-dot-to&logoColor=white" height=25></a>
<a href="https://www.youtube.com/user/dennisleewm"><img src="https://img.shields.io/badge/-YouTube-red?&style=for-the-badge&logo=youtube&logoColor=white" height=25></a>
</p>
<p>
<span class="badge-buymeacoffee"><a href="https://ko-fi.com/dennislwm" title="Donate to this project using Buy Me A Coffee"><img src="https://img.shields.io/badge/buy%20me%20a%20coffee-donate-yellow.svg" alt="Buy Me A Coffee donate button" /></a></span>
<span class="badge-patreon"><a href="https://patreon.com/dennislwm" title="Donate to this project using Patreon"><img src="https://img.shields.io/badge/patreon-donate-yellow.svg" alt="Patreon donate button" /></a></span>
<span class="badge-newsletter"><a href="https://buttondown.email/dennislwm" title="Subscribe to Newsletter"><img src="https://img.shields.io/badge/newsletter-subscribe-blue.svg" alt="Subscribe Dennis Lee's Newsletter" /></a></span>
