## 发布到 Maven Central 仓库
参考 [https://proandroiddev.com/publishing-android-libraries-to-mavencentral-in-2021-8ac9975c3e52](https://proandroiddev.com/publishing-android-libraries-to-mavencentral-in-2021-8ac9975c3e52)

## 注意事项
1. 配置环境变量
      
|   环境变量           |  含义         | 
|--------------------|------------------|
|  OSSRH_USERNAME | mavenCentral 用户名 |
|  OSSRH_PASSWORD| mavenCentral 密码 |
|  SIGNING_KEY\_ID| 生成的 GPG id |
|  SIGNING_PASSWORD| GPG 密码 |
|  SIGNING_SECRET\_KEY\_RING\_FILE| 密钥导出生成的 xxx.gpg 文件路径 |
|  SONATYPE_STAGING\_PROFILE\_ID| https://s01.oss.sonatype.org/ 上的 profiles id |

2. 修改项目的根目录的 build.gradle 

  ```
   buildscript {
        repositories {
         .................
           // 增加 gradle 插件 的 maven 地址，防止无法获取插件
           maven {
               url "https://plugins.gradle.org/m2/"
           }
        }
        dependencies {
            .................
             // 增加 gradle 插件
            classpath 'io.github.gradle-nexus:publish-plugin:1.1.0'
        }
    }

   allprojects {
        repositories {
         .................
          // 增加 gradle 插件 的 maven 地址，防止无法获取插件
           maven {
                url "https://plugins.gradle.org/m2/"
           }
       }
     } 
    // 增加 gradle 发布脚本
   apply from: "https://raw.githubusercontent.com/lwjfork/scriptlib/master/gradle/publish/maven/publish-root.gradle"
```

3.  在发布的module的目录增加 gradle.properties 文件，并添加文件内容
   
   ``` 
   ## 发布库的 group id
    PUBLISH_GROUP_ID=
    ## 发布库的 artifactId
    PUBLISH_ARTIFACT_ID=
    ## 发布库的 版本
    PUBLISH_VERSION=
    # pom 配置
    ### pom 名称
    POM_NAME=
    ### 库的描述
    POM_DESCRIPTION=
    ### 库的地址
    POM_URL=
    ## pom.scm 配置
    POM_SCM_CONNECTION=
    POM_SCM_DEV_CONNECTION=
   POM_SCM_URL=

    ## pom.licenses
    POM_LICENCE_NAME=The Apache Software License, Version 2.0
    POM_LICENCE_URL=http://www.apache.org/licenses/LICENSE-2.0.txt

   ## pom.developers 信息
   POM_DEVELOPER_ID=
   POM_DEVELOPER_NAME=
   POM_DEVELOPER_EMAIL=
   ## module 名称
   PROJECT_NAME=GesturePwdView
   ```
4. 发布时，执行 task **publishReleasePublicationToSonatypeRepository**


## 1. 发布 Jar  （gradle version > 6.5 ）
#### 1.1 发布 只 包含 java 代码的 jar

1. 在 发布的 module 目录下的 build.gradle 文件末尾增加

   ```
   apply from: "https://raw.githubusercontent.com/lwjfork/scriptlib/master/gradle/publish/maven/jar/publish-no-kotlin.gradle"
   ``` 
   

#### 1.2 发布 包含 kotlin 代码的 jar
1. 在 根目录 build.gradle 文件的 dependencies 节点再次增加以下代码
   
   ```
     classpath "org.jetbrains.dokka:dokka-gradle-plugin:1.4.30"
   ```
2.  在 发布的 module 目录下的 build.gradle 文件末尾增加
 
   ```
   apply from: "https://raw.githubusercontent.com/lwjfork/scriptlib/master/gradle/publish/maven/jar/publish-contain-kotlin.gradle"
   ``` 
   
## 2. 发布  aar  （gradle version > 6.5 ）
#### 2.1 发布 只 包含 java 代码的 aar

1. 在 发布的 module 目录下的 build.gradle 文件末尾增加

   ```
   apply from: "https://raw.githubusercontent.com/lwjfork/scriptlib/master/gradle/publish/maven/aar/publish-no-kotlin.gradle"
   ``` 
   

#### 2.2 发布 包含 kotlin 代码的 aar
1. 在 根目录 build.gradle 文件的 dependencies 节点再次增加以下代码
   
   ```
     classpath "org.jetbrains.dokka:dokka-gradle-plugin:1.4.30"
   ```
2.  在 发布的 module 目录下的 build.gradle 文件末尾增加
 
   ```
   apply from: "https://raw.githubusercontent.com/lwjfork/scriptlib/master/gradle/publish/maven/aar/publish-contain-kotlin.gradle"
   ``` 
      
   

