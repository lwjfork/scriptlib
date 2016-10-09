# gradle 脚本的使用

使用每个gradle 脚本需要 

 ```
  apply from:   你所使用脚本
  
 ```
 
 
## android module 上传到 jcenter（假设你有jcenter帐号了）
### 加入上传jcenter 必须的组件
>此处会因为gradel插件版本的差异导致上传失败。如果出现错误，在确定你配置无错的情况下，请更改你的gradle版本或者 com.github.dcendents:android-maven-gradle-plugin 的版本,
  >>更改版本请参考 [android-maven-gradle-plugin](https://github.com/dcendents/android-maven-gradle-plugin)
  
在 根目录的 build.gradle 文件里加入上传jcenter必须的组件
   
            
          `classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2`
          
          `classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3`
          
  
  加入后 根目录下的build.gradle的完整内容：
          
  ```
  buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.5.0'
        //  下面两行是上传 jcenter 上的可以删除了
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
  }

   allprojects {
    repositories {
        jcenter()
    }
   }     
  ```  

### 配置你的库信息
在一个配置文件里 配置你所想要配置开源库的信息。在根目录下的local.properties 里配置你的信息 防止被泄漏（local.properties 默认是不加入版本控制的）

   ```
    # 这里改成groupId ， 比如com.android.support
    PROJ_GROUP=com.android.support
     # 这里改成库版本 ， 比如22.2.0
    PROJ_VERSION =22.2.0
     # 这里改成库名字 ， 比如appcompat
     PROJ_NAME=appcompat
     # 这里改成github地址 ， 比如https:github.com/android/appcompat
     PROJ_WEBSITEURL=https:github.com/android/appcompat
     # 这里改成issue地址 ，
    #比如https:github.com/android/appcompat/issues
     PROJ_ISSUEURL=https:github.com/android/appcompat/issues
     # 这里改成版本控制地主 ，
     # 比如https:github.com/android/appcompat.git
    PROJ_VCSURL=https:github.com/android/appcompat.git
    # 这里改成库的描述信息
    PROJ_DESCRIPTION=common utils for Android
    # 这里改成库的标示 ， 比如appcompat - v7
    PROJ_ARTIFACTID=appcompat - v7
     # 这里改成开发者id ， 比如
     DEVELOPER_ID=google
    # 这里改成开发者名字 ， 比如android
    DEVELOPER_NAME=android
    #这里改成开发者邮箱，比如[email]someone@android.com[/email]
    DEVELOPER_EMAIL=someone@android.com
    # 用户名
    BINTRAY_USER=你的jcenter的名字
     # key
    BINTRAY_APIKEY=你在jcenter上生成的key 
   ```

### 引入[bintray.gradle](./bintray.gradle) 文件   
> 建议 使用网络上的 bintray.gradle 
 
 在需要上传module的build.gradle 文件的末尾加入
 
 ```
apply from: "https://raw.githubusercontent.com/lwjRes/scriptlib/master/gradle/bintray.gradle"
 ``` 

  
