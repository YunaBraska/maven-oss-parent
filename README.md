# Maven oss parent
### Know how to upload to maven central
[![License][License-Image]][License-Url]
[![Version][Version-image]][Version-Url]
[![Build][Build-Status-Image]][Build-Status-Url] 

[![License][License-Image]][License-Url]
[![Build][Build-Status-Image]][Build-Status-Url]  
[![Central][Central-image]][Central-Url] 
[![Javadoc][javadoc-image]][javadoc-Url]
[![Gitter][Gitter-image]][Gitter-Url] 

### Description
Maven oss parent pom helps open source projects to deploy and release Maven repositories to maven central (https://central.sonatype.org)
Since the official support is from [oss-parent](https://central.sonatype.org/pages/apache-maven.html#deprecated-oss-parent) is deprecated.
This pom creates a release profile which will:
* compile (optional - default=on)
* find duplicate imports (optional - default=on)
* generate test report (jacoco - optional - default=on)
* generate sources
* generate javadocs
* generate gpg signed files
* tag project version
* upload to sonatype nexus
* deploy to sonatype nexus
* release to sonatype nexus

### Attention
You should read [Maven Central Terms](http://repo1.maven.org/terms.html) before using this repository and deploy anything.
You wont be able to rename or delete any pushed repository.

### Usage
* Call `mvn clean deploy -P release` after setup the parent to deploy and release your project to maven central
* The repository will be uploaded, deployed,  released and central sync activated on [Sonatype Nexus](https://oss.sonatype.org/)
* The repository will be published to [Maven Central](https://search.maven.org), typically within 10 minutes, though updates to [Maven Central](https://search.maven.org) can take up to two hours.
* There is no formal relationship between [Maven Central](https://search.maven.org) and [MVN-Repository](https://mvnrepository.com), there is no know how for frequency or accuracy of their updates. (I will update this after [MVN-Repository](https://mvnrepository.com) respond in the next century)

### General setup
##### Project requirements
* _Detailed documentation can be found here: [Sonatype](https://central.sonatype.org)_
* Public git repository (_like on GiHub_)
* LICENSE file in root folder (_like [LICENSE](https://github.com/YunaBraska/maven-oss-parent/blob/master/LICENSE)_)
* README.md file in root folder (_like [README.md](https://github.com/YunaBraska/maven-oss-parent/blob/master/README.md)_)
* Account on [Sonatype Jira](https://issues.sonatype.org)
* Create Issue on [Sonatype Jira](https://issues.sonatype.org)
* gpg installed and setup - like: [gpg simple docu](https://wiki.ubuntuusers.de/GnuPG/)
```bash
	gpg --gen-key
	gpg --list-secret-keys
	gpg --keyserver hkp://pool.sks-keyservers.net --send-keys [your secret id]
```
* settings.xml file in maven home folder (_like [Settings documentation](https://central.sonatype.org/pages/apache-maven.html#distribution-management-and-authentication)_)
```xml
<settings>
    <servers>
        <server>
            <id>ossrh</id>
            <username>[Sonatype Jira username]</username>
            <password>[Sonatype Jira password]</password>
        </server>
    </servers>
    <profiles>
    <profile>
      <id>ossrh</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <gpg.executable>gpg</gpg.executable>
        <gpg.passphrase>[gpg passphrase]</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>
```

##### POM requirements [Example pom](https://github.com/YunaBraska/maven-oss-parent/blob/master/pom.xml)
* POM setup parent
```xml
 <parent>
     <groupId>berlin.yuna</groupId>
     <artifactId>maven-oss-parent</artifactId>
     <version>0.0.1</version>
 </parent>
```
* POM Project \<name\>, \<description\>, \<url\>, <developers> tag -like:
```xml
    <name>${project.artifactId}</name>
    <description>[some description...]</description>
    <url>https://github.com/YunaBraska/maven-oss-parent</url>

    <developers>
        <developer>
            <name>Yuna Morgenstern</name>
            <email>io@yuna.berlin</email>
        </developer>
    </developers>
```
* POM <developers tag> name and mail is needed - like:
```xml
    <developers>
        <developer>
            <name>Yuna Morgenstern</name>
            <email>io@yuna.berlin</email>
        </developer>
    </developers>
```
* POM <licenses> tag for public open source licenses - like: 
```xml
    <licenses>
        <license>
            <name>The Apache License, Version 2.0</name>
            <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
        </license>
    </licenses>
```
* POM <scm> tag for public sources - like:
```xml
    <scm>
        <connection>scm:git:https://github.com/YunaBraska/maven-oss-parent</connection>
        <developerConnection>scm:git:https://github.com/YunaBraska/maven-oss-parent</developerConnection>
        <url>https://github.com/YunaBraska/maven-oss-parent.git</url>
    </scm>
```

### TODOs:
* Create a maven plugin out of this knowledge

![maven-oss-parent](banner.png "maven-oss-parent")

[License-Url]: https://www.apache.org/licenses/LICENSE-2.0
[License-Image]: https://img.shields.io/badge/License-Apache2-blue.svg
[github-release]: https://github.com/YunaBraska/maven-oss-parent
[Build-Status-Url]: https://travis-ci.org/YunaBraska/maven-oss-parent
[Build-Status-Image]: https://travis-ci.org/YunaBraska/maven-oss-parent.svg?branch=master
[Coverage-Url]: https://codecov.io/gh/YunaBraska/maven-oss-parent?branch=master
[Coverage-image]: https://codecov.io/gh/YunaBraska/maven-oss-parent/branch/master/graphs/badge.svg
[Version-url]: https://github.com/YunaBraska/maven-oss-parent
[Version-image]: https://badge.fury.io/gh/YunaBraska%2Fmaven-oss-parent.svg
[Central-url]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22maven-oss-parent%22
[Central-image]: https://maven-badges.herokuapp.com/maven-central/berlin.yuna/maven-oss-parent/badge.svg
[Maintainable-Url]: https://codeclimate.com/github/YunaBraska/maven-oss-parent
[Maintainable-image]: https://codeclimate.com/github/YunaBraska/maven-oss-parent.svg
[Gitter-Url]: https://gitter.im/nats-streaming-server-embedded/Lobby
[Gitter-image]: https://img.shields.io/badge/gitter-join%20chat%20%E2%86%92-brightgreen.svg
[Javadoc-url]: http://javadoc.io/doc/berlin.yuna/maven-oss-parent
[Javadoc-image]: http://javadoc.io/badge/berlin.yuna/maven-oss-parent.svg