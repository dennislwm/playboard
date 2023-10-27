# playboard

---
# 1. Introduction
## 1.1. Purpose

This document describes the Playboard automation and manual services that is provided for DevSecOps Engineer, Mac and Mobile Users.

## 1.2. Audience

The audience for this document includes:

* Mobile User who will add URLs, via Bookmark or Email, and consume RSS feeds on their iPhone device.

* Mac User who will add URLs, via Bookmark or Email, consume RSS feeds, and query text from an archive on their workstation.

* DevSecOps Engineer who will design system workflows, configure any SaaS or selfhosted services, and plan for disaster recovery.

---
# 2. System Overview
## 2.1. Benefits and Values

1. Previously, there wasn't a systematic workflow to send a URL of an article (message), consume and save the message, which can then be queried using a search tool. The methods of sending a message via an Email, WhatsApp or Telegram led to a message sprawl.

2. As an analogy, we have a system of sending messages to one or more queues based on the Tags. A Tag represents a queue, such that a message can be tagged to one or more Tags, hence it is fanned out to multiple queues. Messages in queues can be consumed as separate RSS feeds using Tags. For example, if a message is tagged with `Github`, then it will be appended to the RSS feed with `t:Github`.

3. We have two methods of sending messages, either by Email or Bookmarklet, and on different devices, such as iPhone device or Mac workstation. This flexibility allows you to be more productive as you do not need to be in front of a workstation in order to send messages.

4. The messages are sent to a SaaS application (**Pinboard.in**), hence we don't have to manage the server or application. However, we are still responsible for disaster recovery. The SaaS application is a paid service that has two tiers: Standard (USD $22) and Pro (USD $39). The Pro tier includes a backup of your data on their cloud server for disaster recovery.

5. Currently, there isn't an automated process to save pages of individual Bookmarks as a PDF file. However, as the Bookmarks are consumed from RSS feeds, it is possible to automate this process.

6. In order to search the content of your PDF archive, we have to index and query the text using a MacOS application (**Recoll**). The search function is not available online as the application runs on your workstation.

## 2.2. Workflow

This project uses several methods and products to optimize your workflow.
- Uses a SaaS application (**Pinboard.in**) to produce Bookmarks using a Bookmarklet or by sending an Email.
- Uses a SaaS application (**Pinboard.in**) to manage Bookmarks and share them as separate RSS feeds using Tags.
- Uses a MacOS/iOS application (**NetNewsWire**) to consume individual RSS feeds and save them to a cloud storage.
- Uses a Cloud Storage (**OneDrive.com**) to read, write and synchronise the RSS feeds.
- Uses a SaaS application (**Instapaper.com**) to backup all Bookmarks for disaster recovery.
- Uses a Chrome extension (**PrinterFriendly**) to save pages of individual Bookmarks as a PDF file.
- Uses a MacOS application (**Recoll**) to index and query text from your PDF archive.

---
# 3. User Personas
## 3.1 RACI Matrix

|            Category            |                         Activity                          | Mobile User | Mac User | DevSecOps |
|:------------------------------:|:---------------------------------------------------------:|:-----------:|:--------:|:---------:|
| Installation and Configuration |  Add a Save to Pinboard Bookmarklet on the iPhone device  |     R,A     |          |           |
| Installation and Configuration | Add a Save to Pinboard Bookmarklet on the Mac workstation |             |   R,A    |           |
|           Execution            |                 Adding a URL via Bookmark                 |     R,A     |          |           |
|           Execution            |           Consume an RSS feed in an RSS Reader            |     R,A     |          |           |

---
# 4. Installation and Configuration
## 4.1. Add a Save to Pinboard Bookmarklet on the iPhone device

This runbook should be performed by the Mobile User.

1. On your iPhone device, open the Safari browser and navigate to [Pinboard.in](https://pinboard.in/howto/#saving).

2. Click the Share menu > Add Bookmark.
  - For the Title, type `Save to Pinboard`.

3. Click Save > Click the Bookmark menu > Click Edit > Select the bookmark `Save to Pinboard`.
  - For the Address, copy and paste the Javascript code below.

```js
javascript:if(document.getSelection){s=document.getSelection();}else{s='';};document.location='https://pinboard.in/add?next=same&url='+encodeURIComponent(location.href)+'&description='+encodeURIComponent(s)+'&title='+encodeURIComponent(document.title)
```

4. Click Done > Click Done > Click Done.

## 4.2. Add a Save to Pinboard Bookmarklet on the Mac workstation

This runbook should be performed by the Mac User.

1. On your workstation, open the Chrome browser, download and install the [Pinboard Tools Chrome extension](https://chrome.google.com/webstore/detail/pinboard-tools/dpaohcncbmkojcpcjaojcehdlnjfbjkl).

---
# 5. Execution
## 5.1. Adding a URL via Bookmark

This runbook should be performed by the Mobile User.

1. On your iPhone device, open the Safari browser and navigate to the URL that you want to save.

2. Click the Bookmark menu > Select Save to Pinboard.

3. In the Pinboard dialog, edit the Bookmark.
  - For the URL, enter the URL that you want to save (auto filled).
  - For the Title, enter the Title of the Bookmark (auto filled).
  - For the Description, optionally enter a description for the Bookmark.
  - For the Tags, enter one or more categories (case insensitive) separated by space.

4. Click Add Bookmark.

## 5.2. Consume an RSS feed in an RSS Reader

This runbook should be performed by the Mobile User.

1. On your iPhone device, open your RSS Reader.

2. Click Add Feed.
  - For the URL, enter either a public or private RSS feed by TAG.
  - For the Title, enter `pin/TAG`.

3. To obtain the secret token, Log in to your account > Click Private menu > Click RSS button.

4. Refer to [Pinboard.in How To](https://pinboard.in/howto/#rss) for the URL pattern types.

```sh
https://feeds.pinboard.in/rss/secret:TOKEN/u:USERNAME/t:TAG1
https://feeds.pinboard.in/rss/secret:TOKEN/u:USERNAME/t:TAG1/t:TAG2
```
