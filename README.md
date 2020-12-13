# maven-oss-parent NOT MAINTAINED ANYMORE
*Know how to upload to maven central* 

[![Build][build_shield]][build_link]
[![Maintainable][maintainable_shield]][maintainable_link]
[![Coverage][coverage_shield]][coverage_link]
[![Issues][issues_shield]][issues_link]
[![Commit][commit_shield]][commit_link]
[![Dependencies][dependency_shield]][dependency_link]
[![License][license_shield]][license_link]
[![Central][central_shield]][central_link]
[![Tag][tag_shield]][tag_link]
[![Javadoc][javadoc_shield]][javadoc_link]
[![Size][size_shield]][size_shield]
![Label][label_shield]

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


[build_shield]: https://github.com/YunaBraska/maven-oss-parent/workflows/JAVA_CI/badge.svg
[build_link]: https://github.com/YunaBraska/maven-oss-parent/actions?query=workflow%3AJAVA_CI
[maintainable_shield]: https://img.shields.io/codeclimate/maintainability/YunaBraska/maven-oss-parent?style=flat-square
[maintainable_link]: https://codeclimate.com/github/YunaBraska/maven-oss-parent/maintainability
[coverage_shield]: https://img.shields.io/codeclimate/coverage/YunaBraska/maven-oss-parent?style=flat-square
[coverage_link]: https://codeclimate.com/github/YunaBraska/maven-oss-parent/test_coverage
[issues_shield]: https://img.shields.io/github/issues/YunaBraska/maven-oss-parent?style=flat-square
[issues_link]: https://github.com/YunaBraska/maven-oss-parent/commits/master
[commit_shield]: https://img.shields.io/github/last-commit/YunaBraska/maven-oss-parent?style=flat-square
[commit_link]: https://github.com/YunaBraska/maven-oss-parent/issues
[license_shield]: https://img.shields.io/github/license/YunaBraska/maven-oss-parent?style=flat-square
[license_link]: https://github.com/YunaBraska/maven-oss-parent/blob/master/LICENSE
[dependency_shield]: https://img.shields.io/librariesio/github/YunaBraska/maven-oss-parent?style=flat-square
[dependency_link]: https://libraries.io/github/YunaBraska/maven-oss-parent
[central_shield]: https://img.shields.io/maven-central/v/berlin.yuna/maven-oss-parent?style=flat-square
[central_link]:https://search.maven.org/artifact/berlin.yuna/maven-oss-parent
[tag_shield]: https://img.shields.io/github/v/tag/YunaBraska/maven-oss-parent?style=flat-square
[tag_link]: https://github.com/YunaBraska/maven-oss-parent/releases
[javadoc_shield]: https://javadoc.io/badge2/berlin.yuna/maven-oss-parent/javadoc.svg?style=flat-square
[javadoc_link]: https://javadoc.io/doc/berlin.yuna/maven-oss-parent
[size_shield]: https://img.shields.io/github/repo-size/YunaBraska/maven-oss-parent?style=flat-square
[label_shield]: https://img.shields.io/badge/Yuna-QueenInside-blueviolet?style=flat-square
[gitter_shield]: https://img.shields.io/gitter/room/YunaBraska/nats-streaming-server-embedded?style=flat-square
[gitter_link]: https://gitter.im/nats-streaming-server-embedded/Lobby*__*