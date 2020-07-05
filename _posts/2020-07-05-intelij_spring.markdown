---
layout: post
title:  "Using Spring Boot in Intelij Community version"
date:   2020-07-05 11:23:20 +0800
categories: spring
---
Intelij is a great software but the ultimate version is paid. The community version doesn't have great support for spring framework. In the ultimate version, we can easily start a Spring boot project with the Spring Initiallizr plugin but the Community version doesn't have it.

Fortunately, there is a plugin called Spring Assistant which is almost a free substitute of Spring Initiallizr in the Community version. Unfortunately, since it is free, it is not as well maintained as the Spring Initiallizr. When I start the Spring boot project from it, I cannot run it. All the Spring boot library cannot be found.

I carefully checked the the source code it generates, but it seems the code is totally fine -- in fact they all use the code directly pulled from the spring.io website. Also I checked to run it with command line and it is totally fine, so I found that it is the IDE that doesn't work.

The reason of this is the Intelij Gradle setting changed some a bit (maybe in recent versions). We can fix this by adding a file in the .idea directory of the project like:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project version="4">
  <component name="GradleMigrationSettings" migrationVersion="1" />
  <component name="GradleSettings">
    <option name="linkedExternalProjectsSettings">
      <GradleProjectSettings>
        <option name="distributionType" value="DEFAULT_WRAPPED" />
        <option name="externalProjectPath" value="$PROJECT_DIR$" />
        <option name="gradleHome" value="/usr/local/Cellar/gradle/6.5.1/libexec" />
        <option name="modules">
          <set>
            <option value="$PROJECT_DIR$" />
          </set>
        </option>
      </GradleProjectSettings>
    </option>
  </component>
</project>
```

Then all will be fine! The gradle will help us to add these dependencies!

I spent several hours for this issue, and hope this will not trouble others again!



