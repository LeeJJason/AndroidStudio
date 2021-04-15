# APK 下载并安装
目录：
* lib ：FileProvider 需要使用库
* res : FileProvider 使用的目录资源，拷贝 xml 目录到 Android 工程 res 目录中
* code: 使用到的代码


1. 需要在 AndroidManifest 中添加权限
```xml
 <!-- 添加安装权限 -->
<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
```
2. 适配更新APK路径
```xml
<!-- 适配android 7.0以及以上更新APK路径 -->
<provider android:name="android.support.v4.content.FileProvider" 
    android:authorities="${applicationId}.fileprovider" 
    android:exported="false" 
    android:grantUriPermissions="true">
    <meta-data android:name="android.support.FILE_PROVIDER_PATHS" android:resource="@xml/provider_paths" />
</provider>
```

3. 在资源中添加 `provider_paths` 的内容，拷贝目录 res 里面的资源到Android工程。
4. Java代码调用