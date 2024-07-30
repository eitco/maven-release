# maven release github action

[![License](https://img.shields.io/github/license/eitco/bom-maven-plugin.svg?style=for-the-badge)](https://opensource.org/license/mit)

This github action starts a maven release build. It is a [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action)
that:

1. optionally sets an ssh private key
    * using the [ssh agent action](https://github.com/webfactory/ssh-agent)
    * if the parameter `git-ssh-private-key` is not set, this step is omitted
2. checks out the repository source code
    * using the [default checkout action](https://github.com/actions/checkout)
3. sets up a jdk and maven
    * using the [default setup-java action](https://github.com/actions/setup-java)
4. executes the maven release process
   * it executes the [maven release plugins](https://maven.apache.org/maven-release/maven-release-plugin/) goals [`prepare`](https://maven.apache.org/maven-release/maven-release-plugin/prepare-mojo.html) and [`perform`](https://maven.apache.org/maven-release/maven-release-plugin/perform-mojo.html) 

The action can be customized using the following parameters:

## java-version
The (major) version of the jdk.

default: **17**

## java-distribution
The jdk distribution

default: **temurin**

## gpg-private-key
The gpg private key to use for artifact signing. Make sure to use a github secret here.

## gpg-key-name
The name of the gpg private key. Consider using a github secret here.

## gpg-passphrase
The passphrase of the gpg private key. Make sure to use a github secret here.

## deploy-user
The user to authenticate at the artifact repository. Consider using a github secret here.

## deploy-password
The password to authenticate at the artifact repository. Make sure to use a github secret here.

## global-settings-location

The path inside the repository to the global maven settings used to deploy release artifacts. The default value works
for projects generated using [eitcos default maven github template](https://github.com/eitco/maven-template)

default: **deployment/global-settings.xml**

## git-ssh-private-key

An ssh private key to use in later steps e.g. to commit documentation to a github pages repository. 