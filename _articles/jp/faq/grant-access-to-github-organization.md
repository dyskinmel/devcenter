---
changelog: 
last_modified_at: 
title: How to grant Bitrise access to a GitHub Organization?
menu:
  faq:
    weight: 9

---
{% include not_translated_yet.html %}

This guide explains how to grant access for [bitrise.io](https://www.bitrise.io/) to your GitHub Workspace.

{% include message_box.html type="note" title="Have you authorized Bitrise on Github?" content=" This guide presumes you have already [authorized](https://help.github.com/articles/authorizing-oauth-apps/) Bitrise on GitHub.
"%}

1. Open [https://github.com](https://github.com).
2. In the top right corner, click your avatar and select `Settings`.
3. On the left side, select `Applications`.
4. Click `Authorized OAuth Apps`. You will see the list of apps which can access your account.
5. Click on `Bitrise`.
6. Scroll down to `Workspace access` and click `Grant` so that Bitrise can access your Workspace's repository.

![{{ page.title }}](/img/faq/grant-org-access.jpg)

{% include message_box.html type="important" title="Can't see `Grant` button next to app under `Workspace access`" content="If there's no `Grant` button but only a **red cross** icon next to the Workspace in the `Workspace access` that means that **the access was previously granted but then it was revoked**. You can fix this by first selecting the Workspace under `Workspace settings` on the left side, then clicking `Third-party access`. You can see `Bitrise` with `Denied` access. Click the pencil icon and `Grant access` to Bitrise. Now you can go back to your `Authorized OAuth Apps` and click on Bitrise. You should see a green tick instead of the red cross icon next to your Workspace. "%} 

![{{ page.title }}](/img/faq/third-party-access.jpg)

You can see the Workspace and its repositories if you go back to [bitrise.io](https://www.bitrise.io), click on your avatar, select `Add new App` and hit `Next`.

{% include message_box.html type="note" title="Repository is a fork of another private repository" content="
If the repository is a fork of another private repository which belongs to **(another) Workspace**, you have to repeat these steps and grant access for Bitrise for the Workspace **which owns the original repository**. This is a GitHub limitation: to be able to access a private repository fork you have to grant access for the service (Bitrise) in both repositories; in the fork and in the original repository/Workspace too. "%}