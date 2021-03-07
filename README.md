# mylyn-gitea-updatesite

This is the update site for the Mylyn/Gitea Tasks Connector (https://forge.chapril.org/gitea/mylyn-gitea).

## Usage

1. Install the plugin obviously (you can use the https://teilginn.github.io/mylyn-gitea-updatesite/ update site)
2. Add a new Tasks Repository, using the new *Mylyn/Gitea Tasks Connector*
  1. Enter the project URL (something like `http(s)://my-gitea-instance.org/myname_or_organisation/my_repository(.git)`) (the connector will disguard the `.git` if present)
  2. Enter the API key token you have created via your Gitea’s web interface: `Settings | Applications | Generate New Token`. It's also possible to use usename/password.
  3. **Do not forget to check the "Save Password" checkbox**. I don't know how to create a password prompt...
3. You can now create queries and issues

If you use https instead of http (*and you absolutely should use https*), be sure you have a valid certificate. That means it is signed by a trusted CA. If you don't have a valid certificate (like a self signed certificate), the plugin will refuse to connect. If you want to add your CA certificate to the java keystore, you have to:

1. Find the keystore which is used by your JVM (on my machine it is /etc/ssl/certs/java/cacerts)
2. find out the password for the keystore (the default is "changeit")
3. add the CA certificate to this keystore
  1. On Linux, Mac OS X, or Unix systems, use `keytool -import -alias A-UNIQUE-ALIAS -file YOUR-CA.crt -keystore $PATH_TO_YOUR_KEYSTORE` (root permissions may be necessary)
  2. On Windows, in an Administrator Command Prompt use `"%PROGRAMFILES%\java\jre7\bin\keytool" -import -alias A-UNIQUE-ALIAS -file YOUR-CA.cer -keystore "%PROGRAMFILES%\Java\jre7\lib\security\cacerts"`

I don't kown if I will introduce the option to ignore certificate errors. It is not a good way to do those kind of things, especially as it's now not so difficult to get a valid certificate for self hosted services thanks to Let's Encrypt.

Note that Let's Encrypt certificates are accepted from Java 1.8 and are fully supported by the connector.


## What versions are supported

The Mylyn/Gitea Tasks connector is developped under Linux (XUbuntu 20.04) using:
* Eclipse 2019-12 (4.14.0 Build 20191212-1212)
* Mylyn 3.24
* Java JDK 11
* Java Gitea API 1.13

It is tested in front of *Gitea 1.13* servers. 

It is configured to be compliant in theory with Java 1.8 and Mylyn 3.8.0 as minimal versions.

## What time zone is used in the task editor? 

The times that appear in the Gitea issue editor (ie. created, modified) are in your local machine’s time zone. 

## Known issues/Limitations

* The Mylyn/Gitea Tasks connector can only communicate with Gitea instances when the Swagger API is not been desactivated. (Note: that this feature is activated by default)
* List of Eclipse versions plugins is compliant with, is to be defined. It will be test with the version of Eclipse I'm using (Linux/Windows) in front of an *always* up to date gitea instance. 
* Version 1.x will only support read access and queries, we have may to wait the Version 2.x to create and modify issues.
* If you created a new milestone or added a new member via the web interface, you have to update the repository configuration, so that the connector reloads the project members and milestones. Right click on the Gitea repository in the Task repositories view and click on "Update Repository Configuration".
* Offline mode does not work.
* Out of the box support for valid certificates only. 
* Only support token and user/password as authentication scheme.


### Won't be implemented

The goal of this connector is not to replaced the [Gitea](https://gitea.io/) web interface, so everything which is not Issue related or not link with what may help a developper in his day-to-day issue management like Team/Repository management and milestone management will not be implemented.

