# AAR 格式文件

'aar' 是由 Android Library Project 析出的可发布的二进制数据包。

该文件后缀名为 .aar，对应的 maven artifact type 应为 aar，但该文件实际是包含下列内容的一个 zip 包：

* /AndroidManifest.xml (必需)
* /classes.jar (必需)
* /res/ (必需)
* /R.txt (必需)
* /assets/ (可选)
* /libs/*.jar (可选)
* /jni/<abi>/*.so (可选)
* /proguard.txt (可选)
* /lint.jar (可选)

这些内容均直接放置于 zip 包的根路径中。

其中 R.txt 通过指定 aapt 的 --output-text-symbols 选项而生成。