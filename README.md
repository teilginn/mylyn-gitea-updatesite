# Mylyn/Gitea Tasks Connector Update Site

This is the release and update site for the *Mylyn/Gitea Tasks Connector* (https://forge.chapril.org/gitea/mylyn-gitea/ ).

## Copyrights and License

(c) 2021 F.Terrot

The *Mylyn/Gitea Tasks Connector* is provided under the MIT License you may find a copy here [https://teilginn.github.io/mylyn-gitea-updatesite/LICENSE](https://teilginn.github.io/mylyn-gitea-updatesite/LICENSE)

### Thanks and Credits

I want to thanks and credit:

* `pweingardt` for the [Mylyn Gilab Connector](https://github.com/pweingardt/mylyn-gitlab) which helps me in my initial plug-ins setup.
* `zeripath` for the [Java Gitea API](https://github.com/zeripath/java-gitea-api) I used first to communicate with Gitea's instance before facing ssl and JDK 11 compliance issues. 
* Contributors to the [GitHub Mylyn Connector](https://github.com/eclipse/egit-github) which helps me to understand how I can make GUI of the plugin different.

## Authentication

Starting with version 0.3.0, the *Mylyn/Gitea Tasks Connector* plugin will be signed with a self-signed certificate. 
In addition to this _internal_ signature, a detached GPG signature is provided for all files associated with the release (including this README) in the `gpg/` directory,
more over all commits in *Mylyn/Gitea Tasks Connector* related repositories are also now signed.

Self-signed certificate finger print: `E4:DE:51:E9:22:C9:2E:41:26:50:E8:C4:C8:5C:DF:E5:B1:04:36:D8:B8:46:E5:C9:C2:EF:06:9E:29:3C:55:01`

GPG key finger print: `F9B4 EC90 120D 8584 397F D876 2A76 6910 298F 3874`

If you want to verify the release in front of GPG, the public key file is available from *Mylyn/Gitea Tasks Connector Update Site [2A766910298F3874.asc](https://teilginn.github.io/mylyn-gitea-updatesite/2A766910298F3874.asc)
or from the different Git repositories used to develop the plugin :

* Update Site sources [main repository](https://forge.chapril.org/gitea/mylyn-gitea-updatesite/src/commit/457a618b438b6a712221cfabae80aa799df83135/2A766910298F3874.asc) and [Github mirror](https://raw.githubusercontent.com/teilginn/mylyn-gitea-updatesite/master/2A766910298F3874.asc)
* Plugin sources [main branch](https://forge.chapril.org/gitea/mylyn-gitea/src/commit/9322d65b8baae36f173163ac8a04852cf1fe07c4/2A766910298F3874.asc)

You can also check the GPG key validity/fingerprint from [keys.openpgp.org](https://keys.openpgp.org/) : [https://keys.openpgp.org/search?q=2A766910298F3874](https://keys.openpgp.org/search?q=2A766910298F3874)

## Usage

1. Install the plug-in either using the Eclipse market place 
[https://marketplace.eclipse.org/content/mylyngitea-tasks-connector](https://marketplace.eclipse.org/content/mylyngitea-tasks-connector)
 either using obviously this site [https://teilginn.github.io/mylyn-gitea-updatesite/](https://teilginn.github.io/mylyn-gitea-updatesite/)
 as a manually configured update site.
2. Add a new Tasks Repository, using the new *Gitea Issues* repository type.
  1. Enter the project URL (something like `http(s)://my-gitea-instance.org/myname_or_organisation/my_repository(.git)`) (the connector will disguard the `.git` if present)
  2. Enter the API key token you have created via your Gitea’s web interface: `Settings | Applications | Generate New Token`.
  It's also possible to use usename/password couple.
  3. **Do not forget to check the "Save Password" checkbox**. I don't know how to create a password prompt...
  4. Use the `Validate Settings...` button to verify your settings and then `Close` the dialog
3. You can now create queries
4. Read, Modify and create issues.

If you use *https* instead of http (*and you absolutely should use https*), be sure you have a _valid_ certificate. That means it is signed by a trusted CA.
 If you don't have a _valid_ certificate like a self signed certificate, the plugin may refuse to connect. If you want to add your CA certificate to the
 java keystore, you have to:

1. Find the keystore which is used by your JVM (on my machine it is /etc/ssl/certs/java/cacerts)
2. Find out the password for the keystore (the default is "changeit")
3. Add the CA certificate to this keystore
  1. On Linux, Mac OS X, or Unix systems, use `keytool -import -alias A-UNIQUE-ALIAS -file YOUR-CA.crt -keystore $PATH_TO_YOUR_KEYSTORE` (root permissions may be necessary)
  2. On Windows, in an Administrator Command Prompt use `"%PROGRAMFILES%\java\jre<JAVE-VERSION>\bin\keytool" -import -alias A-UNIQUE-ALIAS -file YOUR-CA.cer -keystore "%PROGRAMFILES%\Java\jre7\lib\security\cacerts"`

Note: Starting with Java8, Let'Encrypt Certificates are accepted default.

## What versions are supported

The Mylyn/Gitea Tasks connector is developed and so tested under Linux (XUbuntu 20.04) using:

* Eclipse 2019-12 (4.14.0 Build 20191212-1212) 
* Mylyn 3.24
* Java JDK 11
* Java Gitea API 1.13

It is tested in front of *Gitea 1.14* Instance. It's highly recommended to keep your Gitea's instance up to date. You can use the [Gitea Auto Update](https://github.com/CMiksche/gitea-auto-update) script to do it for You.

The plug-ins is configured to be compliant with Java 1.8 and Mylyn 3.8.0 as minimal versions and should be compliant with newest Eclipse versions.

The plug-ins should also run with Windows and certainly MAc-OS Eclipse clients. 

## What time zone is used in the task editor? 

The times that appear in the Gitea issue editor (ie. created, modified) are in your local machine’s time zone. 

## Known issues/Limitations

* *Mylyn/Gitea Tasks Connector* is using the Gitea's instance Swagger API. It's obvious but it can only communicate with the Gitea's instance only if the Swagger API is activate. This feature is active by default, so contact your Gitea's instance administrator if it has been disabled.
* List of Eclipse versions plugins is compliant with, is to be defined. It will be test with the version of Eclipse I'm using (Linux/Windows) in front of an *always* up to date gitea instance. 
* If you create a new milestone or add a new member via the web interface, you have to update the repository configuration or query properties, so that the connector reloads the project members and milestones. Right click on the Gitea repository in the Task repositories view and click on "Update Repository Configuration".
* Offline mode is not supported.
* Out of the box support for valid certificates only. 
* Supports only token and user/password as authentication scheme.
* The _Project_ feature is not supported as there is no Gitea Swagger API for that (at least in version 1.13)  

Check Issues repository for more up to date development status information

* [Known issues](https://github.com/teilginn/mylyn-gitea/issues?q=is%3Aopen+is%3Aissue)
* [known limitations](https://github.com/teilginn/mylyn-gitea/labels/known_limitation)

## Report an issue/Request a new feature

To avoid any account management activity, issues tracker is handled at [Github](https://github.com/teilginn/mylyn-gitea/issues).

Feel free to open issues to report bugs or request new features but please only write in English or in French (Google translate is not so good with technical tanslations)

### Won't be implemented

The goal of this connector is *not* to replaced the [Gitea](https://gitea.io/) web interface.
So everything which is not Issue related or not link with what may help a developer in his day-to-day issue management
 like Team/Repository management and milestone management will not be implemented.
