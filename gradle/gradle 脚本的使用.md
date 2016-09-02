# gradle 脚本的使用

使用每个gradle 脚本需要 

 ```
  apply from:   你所使用脚本
  
 ```
 
 
## android module 上传到 jcenter（假设你有jcenter帐号了）
### 加入上传jcenter 必须的组件
  在 根目录的 build.gradle 文件里加入上传jcenter必须的组件
   
            
          `classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2`
          
          `classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3`
          
   重点是 以上两行
          
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
在一个配置文件里 配置你所想要配置的 库的信息。建议你在local.properties 里配置你的信息 防止被泄漏（local.properties 默认是不加入版本控制的）

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

### 引入[utils.gradle](./utils.gradle)和   [bintray.gradle](./bintray.gradle) 文件   
> 建议 你将utils.gradle 和 bintray.gradle 放置在 根路径下 这样获取路径只需要使用
> rootProject.getRootDir().getAbsolutePath()+"/utils.gradle" 和 rootProject.getRootDir().getAbsolutePath()+"/bintray.gradle"
 
 在需要上传module的build.gradle  文件里加入
 
 ```
apply from: utils.gradle 的路径
loadProperties(配置的properties的路径)
apply from: bintray.gradle的路径"
 ``` 
其中的配置的properties 就是你前面配置的库信息的文件
  