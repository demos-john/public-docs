---
description: Sync your Bitbucket repo with GitBook
---

# Enabling Bitbucket Sync

This guide will take you through setting up your GitBook site with a repo on Bitbucket Cloud.

### How Bitbucket Sync works

Bitbucket Sync works the same way as GitHub Sync and GitLab Sync. It keeps your GitBook site and a Bitbucket repository in sync in both directions:

* When you merge a change request in GitBook, GitBook commits the change to the synced branch in Bitbucket.
* When someone pushes a commit to the synced branch in Bitbucket, GitBook updates the matching space.

Your content is stored in the repository as Markdown files. GitBook reads the `gitbook-docs.yaml` file in your project directory to map each space on your site to a directory in the repository. See [Content configuration](content-configuration.md) for details.

{% stepper %}
{% step %}
### Open Git Sync for your site

From your site, open Git Sync in the sidebar.
{% endstep %}

{% step %}
### Connect Bitbucket

Create an API token in your Atlassian account settings. Give it read and write access to repositories, then enter your Atlassian email address and the token in GitBook.

{% hint style="info" %}
The account that owns the token must have **Write** or **Admin** access to the repository in its Bitbucket workspace.
{% endhint %}
{% endstep %}

{% step %}
### Select a repository and branch

Under **Source repository**, select the workspace and the repository that contains your documentation. Select the branch that GitBook syncs with. If the branch doesn’t exist, GitBook creates it during the initial sync.

{% hint style="info" %}
**Can’t find your repository?** Make sure your API token has repository access and that its account belongs to the repository’s workspace.
{% endhint %}

{% hint style="warning" %}
If your `main` branch has branch restrictions, select a separate branch for Git Sync. You can merge that branch into `main` while keeping its restrictions.
{% endhint %}
{% endstep %}

{% step %}
### Choose an initial sync direction

Choose the source of truth for the initial sync. Select **Swap direction** if the repository content should replace the GitBook content.

{% hint style="warning" %}
**Bitbucket → GitBook can replace your site’s content.** GitBook replaces each synced section with the content of the selected branch. If the repository is empty, or is behind GitBook because recent change requests haven’t been exported yet, that content is lost from the section and your published site.

You choose a direction every time you set up Git Sync, including when you reconnect it or re-create an existing connection. Before you start the sync, confirm the repository, branch, and direction. If you choose Bitbucket → GitBook, check that the branch’s latest commit includes your most recent merged change requests.

If content was replaced, see [Troubleshooting](troubleshooting.md) to restore it.
{% endhint %}
{% endstep %}

{% step %}
### Set the project directory

If your documentation lives in a subdirectory, enter it under **Project directory**. GitBook stores your site’s `gitbook-docs.yaml` file in this directory. Use this configuration if your docs live within a [monorepo](monorepos.md).
{% endstep %}

{% step %}
### Map your spaces

Under **Content mapping**, assign each space to a directory in the repository. Use `./` for paths relative to the project directory. Use `/` for paths from the repository root. Newly linked spaces sync automatically.
{% endstep %}

{% step %}
### Review advanced options

If needed, configure agent instruction files or a commit message template.
{% endstep %}

{% step %}
### Sync your site

Click **Sync** to start the initial sync.
{% endstep %}

{% step %}
### Write and commit

Merge a change request in GitBook to commit its changes to Bitbucket. Commits to Bitbucket sync back to GitBook.
{% endstep %}
{% endstepper %}

#### Exclude a space from site-wide Git Sync

In the site’s Git Sync content mapping, click the remove icon next to the space you want to exclude. You can then configure Git Sync from that space.

If the site already has Git Sync, GitBook asks you to choose a scope:

* Select the site’s repository and branch to add the space to site-wide Git Sync.
* Select an independent repository and branch to configure Space Git Sync.

If the site doesn’t use Git Sync, GitBook configures Git Sync independently for the space.

To configure Git Sync for a single space, in the space you want to sync, click **Set up** next to **Git Sync** in the [space header](../../reference/gitbook-ui.md#space-header). From the provider list, click **Bitbucket Sync**, and click **Configure**.
