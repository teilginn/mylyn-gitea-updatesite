# mylyn-gitea-updatesite

This is the update site for the Mylyn/Gitea Tasks Connector (https://forge.chapril.org/gitea/mylyn-gitea).

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
 
## Known limitations 

A lot of limitation are present in these first development versions. They may disppear during the walk to Version 1.0.0

* Password/Acces token requires to be saved during repository configuration - this is why we recommend to use only access token (configured by default) as they can easily be revoked.
* It's not possible to submit changes 
* It's not possible to filter per Project
* It's required to known the exact list of labels
* ...

