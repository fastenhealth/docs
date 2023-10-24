---
title: Selfhosted Runners
parent: CI/CD
grand_parent: Technical
---

# Mac

{: .warning }
> This content is sourced from https://www.scaleway.com/en/docs/tutorials/install-github-actions-runner-mac/

## Introduction

GitHub Actions is a CI/CD platform that allows users to automate their software development workflows, connected to a 
Github organization or repository. While GitHub offers online runners with a pay-as-you-go model, self-hosted runners 
grant increased control over your CI/CD setup and enhanced customization. This is because you manage the runners yourself, 
rather than relying on GitHub's infrastructure. This tutorial shows you how to set up, configure, and connect a self-hosted 
runner on a Mac mini M1 to execute macOS pipelines.

{: .important }
> Github [recommends](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners#self-hosted-runner-security) to only use self-hosted runners with private repositories for security reasons.

## Installing the runner

1. Navigate to the main page of your [GitHub](https://github.com/) repository and click **Settings**.
2. Click **Actions**, located under **Code and automation** on the left sidebar. A menu displays.
3. Click **Runners**.
4. Click the **New self-hosted runner** button. You are redirected to the self-hosted runners configuration page.
5. Select **macOS** as a runner image and **ARM64** as an architecture.
   {: .warning }
   > After selecting the runner image and architecture, GitHub prompts you to execute a sequence of shell commands. Those commands serve to authenticate your machine with your Github repository, download the necessary runtime and set-up the runner within your environment. Take note of these commands, as you will need to execute them on your Mac mini M1.
6. [Connect](/bare-metal/apple-silicon/how-to/connect-to-mac-mini-m1/) to your Mac mini M1 using VNC.
   {: .warning }
   > In this instance, SSH cannot be used as the runner service needs a graphical session to be started.
   
7. Open a terminal and execute the commands previously prompted by Github. Don't launch the runner yet.
   {: .warning } 
   > This tutorial assumes that you picked the default settings when prompted during step 6.
    
## Configuring the runner

Once the runner is installed, you must configure it to use the dependencies needed for your workflows.

1. Install the dependencies needed for your workflows. For example, [Homebrew](https://brew.sh/) is a popular package manager for macOS that can be installed with the following command:
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
   Unlike online runners where dependencies have to be installed each time a workflow is run, self-hosted runners allow you to prepare all the dependencies that you need.

2. Create a file named `.path` in the root of the runner directory and define the content of the runner's `$PATH` variable within it. As the runner uses an empty user profile, its path must be configured accordingly. This file is located in the root of the runner directory. To be able to use during a workflow the homebrew command previously installed, append this content at the end of the .path file:
    ```
    :/opt/homebrew/bin
    ```
3. Specify your environment variables in the `.env` file, following the same rationale as the path configuration. This file is also located in the root of the runner directory. To tell homebrew to avoid doing cleanups during workflow in order to not waste compute time, add the following variable to `.env`:
    ```
    HOMEBREW_NO_INSTALL_CLEANUP=TRUE
    ```
   {: .warning }
   > The `.env` file follows the bash syntax to set variables.
   

4. You can create your own scripts to [execute before or after a job](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/running-scripts-before-or-after-a-job).

## Configuring the service

After configuring the runner, you can configure it as a service in order to run it in the background and follow the lifecycle of your Mac mini from boot time to shut down, as well as restarts in case of failures.

1. Your Mac must be configured to log-in automatically. Go to **System Preferences** > **Users and Groups** > **Login Options** and select the **m1** user in the **Automatic Login** picklist.

2. Install and run the service:
```sh
./svc.sh install
./svc.sh start
```

## Using the runner in a workflow

The runner is already authenticated to your repository and referenced with the labels `self-hosted`, `macOS` and `ARM64`.
You can use it in your workflows, by [populating `jobs.<job_id>.runs-on`](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on) with those labels.

For example, the following workflow will use the self-hosted runner to install Node.js using Homebrew:

```yaml
name: Sample workflow

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: [self-hosted, macOS, ARM64]

    steps:
      - name: Install NodeJS
        run: brew install node
```

## Conclusion

This tutorial showed you how to set up, configure, and connect a self-hosted runner on a Mac mini M1 for executing macOS pipelines. The runner is now ready to be used in your workflows. For more information, visit [Managing self-hosted runners on Github Docs](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners).

# Windows

- https://github.com/actions/runner-images/blob/main/docs/create-image-and-azure-resources.md
- https://github.com/philips-labs/terraform-aws-github-runner

To build these images you first need to install packer. You will also need an amazon account and to have provisioned your credentials for packer to consume.

Assuming you are building the `windows-core-2022` image. Then run the following from within the windows-core-2022 folder

```
subl github_agent.windows.pkr.hcl
# update region to us-east-1
# update root_volume_size_gb to 50


packer init .
packer validate .
packer build github_agent.windows.pkr.hcl
```

Your image will then begin to build inside AWS and when finished you will be provided with complete AMI.
