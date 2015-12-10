# mbari-maven-repository #

---


Due to the upcoming Google Code shutdown this repository is now read-only. A copy of this repository has been cloned to [GitHub](https://github.com/hohonuuli/mbari-maven-repository).

---


This is a central maven repository for MBARI open source software projects. Jars in this repository are either produced by MBARI or used by MBARI projects.

## Using Artifacts in this Repository ##

To use artifacts from this repository in your projects add the following to your pom.xml file

```
<repository>
  <id>mbari-maven-repository</id>
  <name>MBARI Maven Repository</name>
  <url>https://mbari-maven-repository.googlecode.com/svn/repository/</url>
</repository>
```

If you're brave, you can also use the SNAPSHOT repository by adding the following to your pom.xml file
```
<repository>
  <id>mbari-maven-snapshot-repository</id>
  <name>MBARI Maven Snapshot Repository</name>
  <url>https://mbari-maven-repository.googlecode.com/svn/snapshot-repository/</url>
</repository>
```

## Browsing for Artifacts ##

You can browse for artifacts under the [Source](http://code.google.com/p/mbari-maven-repository/source/browse/#svn%2Frepository) tab above.


## Deploying Artifacts ##

To deploy to this repository, add the following to your pom.xml:

```
</build>
  <extensions>  
    <extension>  
      <groupId>org.apache.maven.wagon</groupId>  
      <artifactId>wagon-webdav</artifactId>  
    </extension>  
  </extensions>
</build>

<distributionManagement>
  <repository>
    <uniqueVersion>true</uniqueVersion>
    <id>mbari-maven-repository</id>
     <url>dav:https://mbari-maven-repository.googlecode.com/svn/repository</url>
  </repository>
  <snapshotRepository>
    <uniqueVersion>true</uniqueVersion>
    <id>mbari-maven-snapshot-repository</id>
     <url>dav:https://mbari-maven-repository.googlecode.com/svn/snapshot-repository</url>
  </snapshotRepository>
</distributionManagement>
```

Also add the following to your servers to your settings.xml file (most likely located at $HOME/.m2/settings.xml)

```
<settings 
    xmlns="http://maven.apache.org/SETTINGS/1.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>mbari-maven-repository</id>
            <username>your-google-id</username>
            <password>your-google-password</password>
            <filePermissions>775</filePermissions>
            <directoryPermissions>775</directoryPermissions>
        </server>
        <server>
            <id>mbari-maven-snapshot-repository</id>
            <username>your-google-id</username>
            <password>your-google-password</password>
            <filePermissions>775</filePermissions>
            <directoryPermissions>775</directoryPermissions>
        </server>
    </servers>
</settings>
```

## Deploying Artifacts from the Command Line ##

It's relatively simple to deploy single-jar artifacts via the command line to the repo. Refer to the documentation of the [Maven Deploy Plugin](http://maven.apache.org/plugins/maven-deploy-plugin/howto.html) for the nitty-gritty details. For reference, here's an example of the command used to deploy [Sanselan](http://commons.apache.org/sanselan) to our repository:
```
mvn deploy:deploy-file \
  -Durl=dav:https://mbari-maven-repository.googlecode.com/svn/repository \
  -DrepositoryId=mbari-maven-repository \ 
  -DgroupId=org.apache.commons \
  -DartifactId=sanselan \
  -Dpackaging=jar \
  -Dfile=sanselan-0.97-incubator.jar \
  -Dversion=0.97 \
  -DgeneratePom=true
```