---
title: Managing an app's bitrise.yml configuration
redirect_from:
- "/bitrise-cli/bitrise-yml-online/"
- "/bitrise-cli/bitrise-yml-online"
tag:
- bitrise.yml
- builds
description: Every bitrise.yml file is stored for your builds on bitrise.io. They
  come in handy when you'd like to check the configuration with which a specific build
  has run. To do that, you can either use our GUI or your build's online bitrise.yml
  file.
summary: ''
menu:
  builds-main:
    weight: 23

---
The `bitrise.yml` file is the heart of your Bitrise setup: [it stores your build configuration, right down to Step input values, the trigger map, and stack information](/bitrise-cli/basics-of-bitrise-yml/#bitriseyml-configuration). When you edit your Workflows on the graphical UI of our Workflow Editor, you actually modify the `bitrise.yml` file.

{% include message_box.html type="warning" title="Changing the stack type in the bitrise.yml file" content="Currently, you can't set the default stack type for an app's builds directly in the `bitrise.yml` file of the app. You can only set it on the **Stacks** tab of the Workflow Editor."%}

{% include message_box.html type="warning" title=".yml size limitations" content="Please note that the total, combined size of the `bitrise.yml` and the  `bitrise.secrets.yml` file cannot exceed 200KB."%}

There are two ways to manage the `bitrise.yml` file of your app:

* Keep the file in your Git repository: with this solution, you have full control over maintaining and versioning the `bitrise.yml` file.
* Keep it on [bitrise.io](http://bitrise.io/ "http://bitrise.io"): Bitrise will store your configuration, and you can access it any time on the website. With this solution, the configuration file is fully independent from your repository.

You can switch between the two solutions at any time.

{% include message_box.html type="info" title="Multiple apps with the same repository" content="You can only store a single `bitrise.yml` file in a given repository. Bitrise will look for the file in the root directory, and as such, currently there's no way to include two in separate folders.

If you have two or more Bitrise apps connected to the same repository, you can store all their Workflows in the same `bitrise.yml` file. Of course each Workflow must have a different name: you can't have two `primary` Workflows in the same file, for example."%}

## Storing the bitrise.yml file in your repository

{% include message_box.html type="warning" title="GitHub Enterprise" content="Unfortunately, this feature is not yet supported for GitHub Enterprise users. If you wish to store the `bitrise.yml` in your repository as a GitHub Enterprise user, we recommend this workaround: [Using the bitrise.yml from repository](/tips-and-tricks/use-bitrise-yml-from-repository/)."%}

When you store the `bitrise.yml` configuration file in your repository, the build process on Bitrise will use that file to run your builds. This means that:

* You have full control over versioning your configuration file.
* Every time you make a change to your Workflows or your trigger map, you must commit the changes to the file in the repository.

{% include message_box.html type="important" title="Service credential user" content="In order to be able to use the feature, you must set the Service credential user correctly: it must be a user who has at least `read` access to the repository at your app's hosting service.

To check the Service credential user, go to the **Team** tab of your app, and find the **Service credential User** option. If you need to change it, keep in mind that for security reasons, you can only select your own account as service credential user. If you don't have `read` access to your app's repository at your hosting service, you can't set the appropriate Service credential user. "%}

{% include message_box.html type="warning" title="Repository access" content="Be aware that if your app uses a repository where the Service credential user integration is not supported - for example, the repository is only accessible under a private IP subnet -, the feature won't work as the website can't grab the `bitrise.yml` due to IP addressing limitations.

The feature is definitely supported for the following hosting services:

* GitHub (only GitHub.com accounts; GitHub Enterprise is not supported)
* BitBucket
* GitLab
* Self-hosted GitLab (as long as the repository is not on a private network)."%}

{% include message_box.html type="warning" title="Changing the stack type in the bitrise.yml file" content="Currently, you can't set the default stack type for an app's builds directly in the `bitrise.yml` file of the app. You can only set it on the **Stacks** tab of the Workflow Editor."%}

To store the file in your repository, you must commit it to the root of your Bitrise app’s default branch. You can check the app’s default branch on [bitrise.io](http://bitrise.io/ "http://bitrise.io"): open the app, and go to the **Settings** tab. Scroll down to the **DEFAULT BRANCH** option to check which branch should contain the `bitrise.yml` file.

You don’t need to create your own `bitrise.yml` file in advance to use this solution though: during the process of updating your settings, you will have the chance to download the current file from the website, or copy its full content. Once you commit that file to the appropriate branch, you can change the setting. Let’s see how to do that:

{% include message_box.html type="important" title="The `bitrise.yml` file must be valid!" content="Always make sure that the `bitrise.yml` file in the repository is valid: a `bitrise.yml` with incorrect syntax will break your builds!"%}

1. Open the app on Bitrise.
2. Go to the **Workflows** tab.
3. In the Workflow Editor, go to the **bitrise.yml** tab.
4. Click **Store in app repository**.
5. If you don’t have a `bitrise.yml` file the repository, you will be prompted to add one.

   ![{{ page.title }}](/img/bitrise_workflow_editor-2.png)  
   You can download the current `bitrise.yml` file from the website, or copy its entire content to the clipboard. Either way, you have to commit the file to the root directory of the repository to proceed. Remember: you must commit the file to the branch that is set as the default branch on [bitrise.io](https://www.bitrise.io)! You can check the default branch under the **Settings** tab on our website.
6. Click **Update setting**.
7. When prompted to make sure your `bitrise.yml` file is valid, click **Continue**.

If all goes well, you should receive confirmation of successfully changing your `bitrise.yml` storage settings.

### Storing the bitrise.yml on multiple branches

When you first add the `bitrise.yml` to your repository, it must be committed to the default branch. You can check out the app's default branch on [bitrise.io](https://www.bitrise.io) under the **Settings** tab.

{% include message_box.html type="warning" title="The bitrise.yml file on the default branch" content="If you choose to store the `bitrise.yml` file in the repository, the default branch must have a `bitrise.yml`!"%}

However, once you did the initial configuration to set up using the `bitrise.yml` from your repository, you can store `bitrise.yml` files on other branches and use any of them to run builds. If you want to build a branch of your repository on Bitrise, you need to have a `bitrise.yml` file on that branch. And don't forget that you always need to keep a `bitrise.yml` file on the default branch.

{% include message_box.html type="example" title="Example setup with bitrise.yml on multiple branches" content="Let's say you have an app called FantasticApp. In FantasticApp's Git repository, the default branch is called `main`. There is also a `deploy` branch.

Any code push or pull request to `main` triggers a Workflow called `main`. Any code push or pull request to `deploy` triggers a Workflow called `deploy`.

In the repository, there is a `bitrise.yml` file on both the `main` and the `deploy` branch, containing both Workflows. When making changes to the Workflows, the FantasticApp team commits the modified `bitrise.yml` file to both branches to ensure that their Workflows are up to date on both. "%}

## Storing the bitrise.yml file on bitrise.io

The default setting is to store the `bitrise.yml` file on [bitrise.io](http://bitrise.io/ "http://bitrise.io"): when you add a new app, we automatically create a `bitrise.yml` file for you and it’s stored on our website. If this works for you, then you don’t need to change anything!

If, however, you changed your storage settings to keep the configuration file in your repository, you can easily change it back any time to store the file on [bitrise.io](http://bitrise.io/ "http://bitrise.io").

1. Open the app on Bitrise.
2. Go to the **Workflows** tab.
3. In the Workflow Editor, go to the **bitrise.yml** tab.
4. Click **Store on bitrise.io**.
5. Choose which `bitrise.yml` file should be used on [bitrise.io](http://bitrise.io/ "http://bitrise.io") from now.  
   \- You can copy the content of the `bitrise.yml` file stored in the app’s repository.  
   \- You can copy the last version of the `bitrise.yml` file that you used on [bitrise.io](http://bitrise.io/ "http://bitrise.io").
6. Click **Update setting**.

If all goes well, you should receive confirmation of successfully changing your `bitrise.yml` storage settings.

## Accessing a build's bitrise.yml

Every `bitrise.yml` file is stored for your builds on [bitrise.io](https://www.bitrise.io). They come in handy when you'd like to check the configuration with which a specific build has run. To do that, you can either use the online **Workflow Editor** or your build's online `bitrise.yml` file. If you choose the latter, you can compare changes, restore the current build to the original version, edit the config, and download the file to your computer.

{% include message_box.html type="note" title="Using filters on your Builds Board" content="
If an app has multiple builds on [bitrise.io](https://www.bitrise.io) and you want to pick a specific build out of those, then these filters will help you a lot. Click on your app in your **Dashboard** and use the following fields:

* You can search for a build number or commit message in the **Try build number or commit message** grey field.
* You can pick which of these triggers was used for your build: **Pushes**, **Pull Requests**, **Tags** or all of these.
* You can pick which **branch** the build was started on.
* You can select either the **primary** or the **deploy workflow** of the build."%}

  ![{{ page.title }}](/img/builds.png)

1. Select an application on your **Dashboard** and select one of its builds.
2. Click the **Show bitrise.yml** button at the top OR at the bottom of your inline log.

   You should see your build's `bitrise.yml` content displayed in ace editor but it's not editable here. See where you can [edit the `bitrise.yml` online](#editing-and-downloading-bitriseyml-online).

## Checking changes in bitrise.yml online

Once you've clicked **Show bitrise.yml**, you will see the **BUILD'S BITRISE YML** pop-up window displaying your builds' configuration details. If the build's `bitrise.yml` content differs from the current build's `bitrise.yml`, you will see two editors displayed side-by-side in the **BITRISE.YML CHANGES** pop-up window. The differences between the builds are highlighted in the following colors:

* Green means added content.
* Blue means modified content.
* Red means deleted content.

![{{ page.title }}](/img/bitrise-yml-changes.png)

## Restoring and undoing changes in bitrise.yml online

If you don't like the changes made to your current `bitrise.yml`, you can easily restore it to the build's original `bitrise.yml`.

1. Click the **Show bitrise.yml** button at the top OR at the bottom of your inline log on [bitrise.io](https://www.bitrise.io/).
2. In the **BITRISE.YML CHANGES** pop-up window, click the orange **Restore** button.
3. Hit **OK** in the **Are you sure?** pop-up window to confirm and override the current `bitrise.yml`.

![{{ page.title }}](/img/bitrise-yml-changes-are-you-sure.png)

## Editing and downloading bitrise.yml online

You can edit your build config in yml format in the **bitrise.yml editor** if you go to your app's Workflow Editor and click the **bitrise.yml** tab.

![{{ page.title }}](/img/bitrise-yml-tab.png)

* Press **F1** for the full command list.
* Fold and unfold with the **-** and **+** signs.
* Press **Ctrl**/**Cmd** + **F** for search and replace where you can search with `RegExp`, `Match Whole Word`, case-sensitive, case-insensitive, or to search only in the selected section.
* Use the **preview sidebar** on the right for easier navigation.

You can save or discard any changes you have made with the config. If you click **Download currently saved config**, you can download this YML version to your own computer and run it with bitrise CLI on your computer.

You might want to copy this whole YML configuration or just part of it to another app, so that you can use the copied version as a base and extend it with a few extra steps. All you have to do is copy this `bitrise.yml` content and paste it into the new app's **bitrise.yml editor** and develop it further.

## Editing a bitrise.yml locally

Our yml scheme is shared on [schemastore](http://schemastore.org/json/). This means that syntax highlight and auto-completion is available for the following files if you edit them locally:

* `bitrise.yml`
* `step.yml`
* `bitrise.json`

The following editors support the auto-complete feature:

* IntelliJ IDEA
* PhpStorm
* PyCharm
* Rider
* RubyMine
* Visual Studio 2013+
* Visual Studio Code
* Visual Studio for Mac
* WebStorm
* JSONBuddy![](/img/autocomplete.png)

If you store your project’s bitrise.yml on Bitrise, you can download it by clicking the **Download currently saved config** button on the **bitrise.yml** page of the **Workflow Edito**r and enjoy auto-completion in your editor locally.![](/img/bitriseymlonline.jpg)

## Deleting a build's bitrise.yml

If you wish, you can simply delete a build's `bitrise.yml` file. But please note that this action cannot be undone: nobody will be able to view that particular build's `bitrise.yml` file once you delete it.

1. Select an application on your **Dashboard** and select one of its builds.
2. Click the **Delete bitrise.yml** button.

   ![{{ page.title }}](/img/delete-bitrise-yml.png)
3. In the confirmation window, click **Yes**.

{% include banner.html banner_text="Check out a `bitrise.yml` file online" url="https://app.bitrise.io/dashboard/builds" button_text="Go to your app" %}