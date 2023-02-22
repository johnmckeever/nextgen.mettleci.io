---
layout: page
title: "Configuring MettleCI Workbench to communicate with Git over HTTPS"
permalink: /
---

# Configuring MettleCI Workbench to communicate with Git over HTTPS

**Note**

This page describes the functionality of MettleCI Workbench **version
1.0-1280 and later**.  
For older versions of Workbench, see this page: <a
href="Configuring_MettleCI_Workbench_to_communicate_with_Git_over_HTTPS_legacy_"
data-linked-resource-id="1112375301" data-linked-resource-version="7"
data-linked-resource-type="page">Configuring MettleCI Workbench to
communicate with Git over HTTPS (legacy)</a>

Data Migrators recommend using the SSH protocol for authentication
between MettleCI Workbench and your remote Git repositories as it is
easier to manage access in a uniform manner across multiple remote Git
repository hosts (Github, Bitbucket, Gitlab, etc). SSH keys also tend to
be more secure than username/password credentials.

# Config.yml Changes

**Warning**

Upgrading MettleCI Workbench from a version prior to 1.0-1280 will
result in a breaking change for customers using Git over HTTPS.  
The global HTTPS credentials stored under the `gitAuthentication`
section of the `config.yml` file are no longer used in MettleCI
Workbench version 1.0-1280 onwards**.** The continued presence of those
values in that file will not cause any adverse behaviour, but those
values will be ignored, and would be better removed from the file to
avoid confusion.

In the event that you need to use Git over HTTPS rather than SSH you can
configure MettleCI Workbench to store a set of username/password
credentials for each user which will be used for all Git HTTPS requests.

These are configured in the `config.yml` file as shown below:

``` java
...
gitAuthentication:
  sshKey: "/opt/dm/mci/workbench.key"       # Location of our private SSH key
  httpsEnabled: true                        # Set true to use HTTPS
  httpsProvider: "SunJSSE"                  #
  httpsCredentialsStore:                    # Details of the SSL certificate file
    type: "PKCS12"
    path: "/opt/dm/mci/.secrets/git-credentials.p12"
    password: ${file:UTF-8:/opt/dm/mci/.secrets/git-credentials-keystore-password}
...
```

The comments in the example above are just for clarity. You should not
have any comments or trailing whitespace after the entries in your
`config.yml`.

This password will be stored in a file
(`.secrets/git-credentials-keystore-password`) referenced in the
`config.yml` file, as shown above.

The git credentials will be stored in a keystore
(`.secrets/git-credentials.p12`) that requires the keystore password and
will be created when the config option `httpsEnabled: true` has been
added to the `config.yml`

# Generating the Git Credentials KeyStore

The Workbench Setup Wizard will automatically generate the
`.secrets/git-credentials-keystore-password` file for you with MettleCI
Workbench **version 1.0-1327 and later**

If you are running MettleCI Workbench on Microsoft Windows, you can skip
this Section

If you are upgrading from an older version of Workbench, you will need
to create this file yourself using the following instructions:-

1.  Make sure the MettleCI Workbench Service is stopped

    ``` java
    $> service dm-mettleci-workbench stop
    ```

2.  Edit the `config.yml` file and add or set the `httpsEnabled` entry
    under the `sshKey` entry. Make sure it is set to `false` for the
    time being.

    ``` java
    gitAuthentication:
      sshKey: "/opt/dm/mci/workbench.key"
      httpsEnabled: false
    ```

3.  In order to create the password file make sure to login as the
    `mciworkb` user.

    ``` java
    $> sudo su - mciworkb
    $> cd /opt/dm/mci
    $> umask 006
    $> touch .secrets/git-credentials-keystore-password
    ```

4.  Edit the file with your preferred editor and enter a new password

    ``` java
    $> vim .secrets/git-credentials-keystore-password

    any_random_generated_password_with_letters_numbers_and_symbols
    ```

5.  Edit the `config.yml` file and add or set the `httpsEnabled` entry
    to `true` under the `sshKey` entry.

    ``` java
    gitAuthentication:
      sshKey: "/opt/dm/mci/workbench.key"
      httpsEnabled: true
    ```

6.  MettleCI Workbench will need to be restarted after saving changes to
    `config.yml`.

    ``` java
    $> service dm-mettleci-workbench start
    ```

7.  Check that the keystore has been created by MettleCI Workbench

    ``` java
    $> ls -l /opt/dm/mci/.secrets/git-credentials*
    -rw-rw---- 1 mciworkb dstage  18 Jun  9 20:58 /opt/dm/mci/.secrets/git-credentials-keystore-password
    -rw-rw---- 1 mciworkb dstage 297 Jun  9 21:17 /opt/dm/mci/.secrets/git-credentials.p12
    ```

# User Profile Git Configuration

When HTTPS is enabled, each user can add their git credentials on the
Profile page which they can access from the menu in the top right corner
of Workbench:

**Note**

If your git repositories are in Azure DevOps you will need to provide an
Azure Personal Access Token (PAT) instead of your password.  
See the Azure documentation if you are unfamiliar with PATs:

<a
href="https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&amp;tabs=preview-page"
data-card-appearance="inline"
rel="nofollow">https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&amp;tabs=preview-page</a>

**Note**

If your git repositories are in Atlassian Bitbucket you will not be able
to use your Bitbucket account password as of March 1, 2022.  
From that date, you will need to provide an App password instead of your
account password.  
See the Atlassian documentation if you are unfamiliar with App
passwords:

<a
href="https://support.atlassian.com/bitbucket-cloud/docs/app-passwords"
rel="nofollow">https://support.atlassian.com/bitbucket-cloud/docs/app-passwords</a>

<img src="attachments/1745747969/1834319913.png?width=272"
class="image-left" loading="lazy"
data-image-src="attachments/1745747969/1834319913.png"
data-height="1342" data-width="1347" data-unresolved-comment-count="0"
data-linked-resource-id="1834319913" data-linked-resource-version="1"
data-linked-resource-type="attachment"
data-linked-resource-default-alias="image-20210618-044310.png"
data-base-url="https://datamigrators.atlassian.net/wiki"
data-linked-resource-content-type="image/png"
data-linked-resource-container-id="1745747969"
data-linked-resource-container-version="25"
data-media-id="c1cced5b-1528-4aed-985d-b6edf9f3d948"
data-media-type="file" width="272" />

You can then enter Git HTTPS or SSH repository URLS in the project
registration page. The ssh or https credentials will be used depending
on the configured Git protocol, any username shown in the URL will be
ignored and overridden by the settings included in `config.yml`:

<img src="attachments/1745747969/1745747985.png" class="image-left"
loading="lazy" data-image-src="attachments/1745747969/1745747985.png"
data-height="793" data-width="794" data-unresolved-comment-count="0"
data-linked-resource-id="1745747985" data-linked-resource-version="1"
data-linked-resource-type="attachment"
data-linked-resource-default-alias="image-20201015-011343.png"
data-base-url="https://datamigrators.atlassian.net/wiki"
data-linked-resource-content-type="image/png"
data-linked-resource-container-id="1745747969"
data-linked-resource-container-version="25"
data-media-id="0f1e867a-bf2b-48fc-aa3d-2c00667cb7b1"
data-media-type="file" />

Ensure that the Git Repository Server is reachable on Port 443 for HTTPS
or Port 80 for HTTP or Port 21 for FTP

**Tip**  
While most Git repository hosts only support HTTPS and SSH protocols,
MettleCI Workbench also supports HTTP and FTP. The same credentials are
used, with the only difference being that the registered Git URL will be
prefixed with the http:// or ftp:// protocol identifiers.

## Attachments:

<img src="images/icons/bullet_blue.gif" width="8" height="8" />
[image-20201015-011343.png](attachments/1745747969/1745747985.png)
(image/png)  
<img src="images/icons/bullet_blue.gif" width="8" height="8" />
[image-20201015-010421.png](attachments/1745747969/1745747988.png)
(image/png)  
<img src="images/icons/bullet_blue.gif" width="8" height="8" /> [Screen
Shot 2021-05-21 at 4.12.17
pm.png](attachments/1745747969/1744863253.png) (image/png)  
<img src="images/icons/bullet_blue.gif" width="8" height="8" />
[image-20210618-044305.png](attachments/1745747969/1834582071.png)
(image/png)  
<img src="images/icons/bullet_blue.gif" width="8" height="8" />
[image-20210618-044310.png](attachments/1745747969/1834319913.png)
(image/png)  
<img src="images/icons/bullet_blue.gif" width="8" height="8" />
[image-20210618-044349.png](attachments/1745747969/1834385445.png)
(image/png)  
