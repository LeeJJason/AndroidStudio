```gradle
buildscript {
    repositories {
        mavenCentral()
        google()
        jcenter()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.4.0'
    }
}

allprojects {
    repositories {
        mavenCentral()
        google()
        jcenter()
        flatDir {
            dirs 'libs'
        }
    }
}

//应用使用 com.android.application
//apply plugin: 'com.android.application'
//JAR使用 com.android.library
apply plugin: 'com.android.library'


dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation project(':unity-android-resources')
}

android {
    compileSdkVersion 26
    buildToolsVersion '29.0.2'

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    //应用相关设置
    defaultConfig {
        minSdkVersion 16
        targetSdkVersion 26
        //应用时用于包名
        //applicationId 'com.dreamforest.reborn'
        ndk {
            abiFilters 'armeabi-v7a', 'x86'
        }
        versionCode 1
        versionName '1.11.181450'
        //默认生成版本
        defaultPublishConfig 'release'
    }

    lintOptions {
        abortOnError false
    }

    aaptOptions {
        [
            //相关的资源
        
        ]
    }

    buildTypes {
        debug {
            minifyEnabled false
            useProguard false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-unity.txt'
            jniDebuggable true
        }
        release {
            minifyEnabled false
            useProguard false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-unity.txt'
            signingConfig signingConfigs.debug
        }
    }

    packagingOptions {
        doNotStrip '*/armeabi-v7a/*.so'
        doNotStrip '*/x86/*.so'
    }

/*
    //应用时用于标记是否分包
    bundle {
        language {
            enableSplit = false
        }
        density {
            enableSplit = false
        }
        abi {
            enableSplit = true
        }
    }*/
}

//到处JAR包，用于标记是否生成 BuildConfig
afterEvaluate {
    generateReleaseBuildConfig.enabled = false
    generateDebugBuildConfig.enabled = false
}
```