[var target]: # (/)

# !{project.name} NOT MAINTAINED ANYMORE
*Know how to upload to maven central* 

[include]: # (/README/shields.include.md)

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