---
layout: "docs"
page_title: "config.winrm - Vagrantfile"
sidebar_current: "vagrantfile-winrm"
description: |-
  The settings within "config.winrm" relate to configuring how Vagrant
  will access your Windows guest over WinRM. As with most Vagrant settings, the
  defaults are typically fine, but you can fine tune whatever you would like.
---

# WinRM Settings

**Config namespace: `config.winrm`**

The settings within `config.winrm` relate to configuring how Vagrant
will access your Windows guest over WinRM. As with most Vagrant settings, the
defaults are typically fine, but you can fine tune whatever you would like.

These settings are only used if you've set your communicator type to `:winrm`.

## Available Settings

* `config.winrm.username` (string) - This sets the username that Vagrant will use
to login to the WinRM web service by default. Providers are free to override
this if they detect a more appropriate user. By default this is "vagrant,"
since that is what most public boxes are made as.

* `config.winrm.password` (string) - This sets a password that Vagrant will use to
authenticate the WinRM user. By default this is "vagrant," since that is
what most public boxes are made as.

* `config.winrm.host` (string) - The hostname or IP to connect to the WinRM service.
By default this is empty, because the provider usually figures this out for
you.

* `config.winrm.port` (integer) - The WinRM port to connect to, by default 5985.

* `config.winrm.guest_port` (integer) - The port on the guest that WinRM is running on.
This is used by some providers to detect forwarded ports for WinRM. For
example, if this is set to 5985 (the default), and Vagrant detects a forwarded
port to port 5985 on the guest from port 4567 on the host, Vagrant will attempt
to use port 4567 to talk to the guest if there is no other option.

* `config.winrm.transport` (symbol)- The transport used for WinRM communication.
Valid settings include: `:negotiate`, `:ssl`, and `:plaintext`. The default is `:negotiate`.

* `config.winrm.basic_auth_only` (boolean) - Whether to use Basic Authentication. Defaults
to `false`. If set to `true` you should also use the `:plaintext` transport setting and
the Windows machine must be configured appropriately.

    **Note:** It is strongly recommended that you only use basic authentication for
    debugging purposes. Credentials will be transferred in plain text.

* `config.winrm.ssl_peer_verification` (boolean) - When set to `false` ssl certificate
validation is not performed.

* `config.winrm.timeout` (integer) - The maximum amount of time to wait for a response
from the endpoint. This defaults to 60 seconds. Note that this will not "timeout"
commands that exceed this amount of time to process, it just requires the endpoint to
report the status of the command before the given amount of time passes.

* `config.winrm.retry_limit` (integer) - The maximum number of times to retry opening
a shell after failure. This defaults to 3.

* `config.winrm.retry_delay` (integer) - The amount of time to wait between retries and
defaults to 10 seconds.

* `config.winrm.codepage` (string) - The WINRS_CODEPAGE which is the client's console
output code page. The default is 65001 (UTF-8).

    **Note:** Versions of Windows older than Windows 7/Server 2008 R2 may exhibit
    undesirable behavior using the default UTF-8 codepage. When using these older
    versions of Windows, its best to use the native code page of the server's locale.
    For example, en-US servers will have a codepage of 437. The Windows `chcp` command
    can be used to determine the value of the native codepage.
