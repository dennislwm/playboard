# playboard

---
# 1. Introduction
## 1.1. Purpose

This document describes the Playboard automation and manual services that is provided for DevSecOps Engineer, Mac and Mobile Users.

## 1.2. Audience

The audience for this document includes:

* Mobile User who will send messages, via Bookmarklet or Email, and consume RSS feeds on their iPhone device.

* Mac User who will send messages, via Bookmarklet or Email, consume RSS feeds, and query text from an archive on their workstation.

* DevSecOps Engineer who will design system workflows, configure any SaaS or selfhosted services, and plan for disaster recovery.

---
# 2. System Overview
## 2.1. Benefits and Values

1. Previously, there wasn't a systematic workflow to send a URL of an article (message), consume and save the message, which can then be queried using a search tool. The methods of sending a message via an Email, WhatsApp or Telegram led to a message sprawl.

2. As an analogy, you have a system of sending messages to one or more queues based on the Tags. A Tag represents a queue, such that a message can be tagged to one or more Tags, hence it is fanned out to multiple queues. Messages in queues can be consumed as separate RSS feeds using Tags. For example, if a message is tagged with `Github`, then it will be appended to the RSS feed with `t:Github`.

3. You have two methods of sending messages, either by Email or Bookmarklet, and on different devices, such as iPhone device or Mac workstation. This flexibility allows you to be more productive as you do not need to be in front of a workstation in order to send messages.

4. The messages are sent to a SaaS application (**Pinboard.in**), hence you don't have to manage the server or application. However, you are still responsible for disaster recovery. The SaaS application is a paid service that has two tiers: Standard (USD $22) and Pro (USD $39). The Pro tier includes a backup of your data on their cloud server for disaster recovery.

5. Currently, there isn't an automated process to save pages of individual Bookmarks as a PDF file. However, as the Bookmarks are consumed from RSS feeds, it is possible to automate this process.

6. In order to search the content of your PDF archive, you have to index and query the text using a MacOS application (**Recoll**). The search function is not available online as the application runs on your workstation.

7. For disaster recovery, you have the option Backup & Restore only, as the service relies on a third-party SaaS application. Using the 3-2-1 backup strategy, you should always have 3 copies of your data, i.e. (1) your production data on the SaaS application (**Pinboard.in**), (2) a primary backup copy on your repository (this **GitHub.com** repo), and (3) a secondary backup copy on another site (TO DO).

## 2.2. Workflow

This project uses several methods and products to optimize your workflow.
- Uses a SaaS application (**Pinboard.in**) to add Bookmarks by either a Bookmarklet or by sending an Email.
- Uses a SaaS application (**Pinboard.in**) to manage Bookmarks and share them as separate RSS feeds using Tags.
- Uses a MacOS/iOS application (**NetNewsWire**) to consume individual RSS feeds and save them to a cloud storage.
- Uses a Cloud Storage (**OneDrive.com**) to read, write and synchronise the RSS feeds.
- Uses a CI pipeline (**GitHub Actions**) to store a primary backup of all Bookmarks for disaster recovery.
- Uses a Chrome extension (**PrinterFriendly**) to save pages of individual Bookmarks as a PDF file.
- Uses a MacOS application (**Recoll**) to index and query text from your PDF archive.

## 2.3. Limitations

This project has several limitations that may hinder your workflow.
- There isn't an automated process to save pages of individual Bookmarks as a PDF file from your RSS feeds.
- The search function is not available online as the application (**Recoll**) runs on your workstation.
- There is no secondary backup data site for disaster recovery.
- The Recovery Point Objective (RPO) for the Backup & Restore disaster recovery plan is ONE (1) day, however you can configure the CI pipeline to run more frequently.

---
# 3. User Personas
## 3.1 RACI Matrix

|            Category            |                         Activity                          | Mobile User | Mac User | DevSecOps |
|:------------------------------:|:---------------------------------------------------------:|:-----------:|:--------:|:---------:|
| Installation and Configuration |  Add a Save to Pinboard Bookmarklet on the iPhone device  |     R,A     |          |           |
| Installation and Configuration | Add a Save to Pinboard Bookmarklet on the Mac workstation |             |   R,A    |           |
|           Execution            |                 Adding a URL via Bookmark                 |     R,A     |          |           |
|           Execution            |           Consume an RSS feed in an RSS Reader            |     R,A     |          |           |
|       Disaster Recovery        | Configure a CI pipeline to store a primary backup of data |             |          |    R,A    |

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
https://feeds.pinboard.in/rss/secret:SECRET_TOKEN/u:USERNAME/t:TAG1
https://feeds.pinboard.in/rss/secret:SECRET_TOKEN/u:USERNAME/t:TAG1/t:TAG2
```

---
# 6. Disaster Recovery
## 6.1. Configure a CI pipeline to store a primary backup of data

This runbook should be performed by the DevSecOps Engineer.

The CI pipeline runs on a scheduled job and will backup all your Bookmarks to this repository using the API method.

1. Open your web browser and navigate to your remote repository > Settings > Secrets and variables > Actions.

2. Click on New repository secret for each of these keys:
  - `API_BASE_URL`: `https://api.pinboard.in`
  - `API_ENDPOINT`: `v1/posts/all`
  - `API_TOKEN`: API_TOKEN

3. Create a new file `.github/workflows/main.yml` with the following code:

```yaml
# This workflow will install store a primary backup of all Bookmarks in this repo for disaster recovery.

name: main

# Controls when the action will run. Triggers the workflow on push or pull request
# events but only for the master branch
# * * * * *  UTC (Convert to Singapore: +0800)
# ┬ ┬ ┬ ┬ ┬
# │ │ │ │ └───── day of week (0 - 7) (0 to 6 are Sunday to Saturday, or use names; 7 is Sunday, the same as 0)
# │ │ │ └────────── month (1 - 12)
# │ │ └─────────────── day of month (1 - 31)
# │ └──────────────────── hour (0 - 23)
# └───────────────────────── min (0 - 59)
on:
  push:
  workflow_dispatch:
  schedule:
    - cron:  '1 0 * * *'

jobs:
  backup:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      # Get all bookmarks
      - name: Backup all Bookmarks
        run: |
          curl --version && jq --version
          response_api=$( curl -X GET "${{ secrets.API_BASE_URL }}/${{ secrets.API_ENDPOINT }}?auth_token=${{ secrets.API_TOKEN }}&format=json" || echo "" )
          if ! [[ -z "${response_api}" ]]; then
            mkdir -p api
            echo "${response_api}" | jq > api/bookmarks.json
          fi

      # Update git repository
      - name: Commit and push if changed
        run: |
          git --version
          git config --global user.email 'github-action-bot@example.com'
          git config --global user.name 'GitHub Action Bot'
          if ! [[ -z $(git status --porcelain) ]]; then
            git add .
            git commit -m "Updated bookmarks"
            git push
          else
            echo "No changes to commit"
          fi
```

4. Enable write permissions in your remote repository > Settings > Actions > General > Workflow permissions > Select **Read and write permissions**.

5. Click Save. The CI pipeline is configured to run on a daily schedule, or a push to the `main` branch.

<details>
<summary>
There are two methods to export all Bookmarks automatically: (1) RSS, and (2) API.
</summary>

### RSS method

The RSS feed URL requires a secret token, which you can obtain by Log in to your account > Click Private menu > Click RSS button. You can format the feed as JSON by replacing `rss` with `json`, for example:

`https://feeds.pinboard.in/json/secret:SECRET_TOKEN/u:USERNAME/`

```json
[{
    "u": "https:\/\/github.com\/dlt-hub\/dlt",
    "d": "GitHub - dlt-hub\/dlt: data load tool (dlt) is an open source Python library that makes data loading easy 🛠️",
    "n": "",
    "dt": "2023-10-27T15:38:40Z",
    "a": "dennislwm",
    "t": [
        "github",
        "python",
        "mlops"
    ]
},{
    "u": "https:\/\/vikunja.io\/",
    "d": "The open-source, self-hostable to-do app | Vikunja",
    "n": "",
    "dt": "2023-10-27T10:42:14Z",
    "a": "dennislwm",
    "t": [
        "github",
        "kanban",
        "selfhosted"
    ]
}]
```

### API method

The [API](https://pinboard.in/api) endpoint `v1/posts/all` requires an authentication token. You can format the response as JSON using the `format` parameter, for example:

`curl -X GET "https://api.pinboard.in/v1/posts/all?auth_token=API_TOKEN&format=json`

```json
[
  {
    "href": "https://github.com/dlt-hub/dlt",
    "description": "GitHub - dlt-hub/dlt: data load tool (dlt) is an open source Python library that makes data loading easy 🛠️",
    "extended": "",
    "meta": "1803a37c8234a7358d123fa07757de6d",
    "hash": "e65e8ed7ea527d65cb2664968fb68606",
    "time": "2023-10-27T15:38:40Z",
    "shared": "no",
    "toread": "no",
    "tags": "github python mlops"
  },
  {
    "href": "https://vikunja.io/",
    "description": "The open-source, self-hostable to-do app | Vikunja",
    "extended": "",
    "meta": "4bb1d6d4a8e7dbabbde237124389131d",
    "hash": "aa129cbf485568e9781eb72975a6028d",
    "time": "2023-10-27T10:42:14Z",
    "shared": "no",
    "toread": "no",
    "tags": "github kanban selfhosted"
  }
]
```
</summary>