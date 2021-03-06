# 基本知识和配置

正如前面所提到的，紧邻 **<font color='green'>main</font>** *sourceSet* 的就是 **<font color='green'>androidTest</font>** *sourceSet*，默认路径在 `src/androidTest/` 下。在测试 *sourceSet* 中会构建使用 Android 测试框架，并且可以部署到设备上的测试 apk 来测试应用程序。这里面可包含 unit tests，instrumentation tests 及 uiautomater tests。`<instrumentation>` 节点会包含在测试构建过程中自动生成的 AndroidManifest.xml，但是你也可以自己创建一个 `src/androidTest/AndroidManifest.xml` 文件并添加其他组件。

下面的值可以用来配置测试应用，相当于配置 `<instrumentation>` 节点（查看 [DSL reference][1] 了解详情）：

* `testApplicationId`
* `testInstrumentationRunner`
* `testHandleProfiling`
* `testFunctionalTest`

正如前面所看到的，这些配置在 **<font color='green'>defaultConfig</font>** 对象中配置：

``` Groovy
android {
    defaultConfig {
        testApplicationId "com.test.foo"
        testInstrumentationRunner "android.test.InstrumentationTestRunner"
        testHandleProfiling true
        testFunctionalTest true
    }
}
```

在测试应用程序的 manifest 文件中，`instrumentation` 节点的 `targetPackage` 属性值会自动使用测试应用的包名设置，即使这个名称是通过 **<font color='green'>defaultConfig</font>** 或者 *Build Type* 对象自定义的。这也是 manifest 中这一部分需要自动生成的原因之一。

另外，*androidTest* 也可以拥有自己的依赖。默认情况下，应用程序的依赖均会自动添加到测试应用中，但是也可以通过以下来扩展：

``` Groovy
dependencies {
    androidTestCompile 'com.google.guava:guava:11.0.2'
}
```

测试应用由 **<font color='green'>assembleAndroidTest</font>** task 构建。**<font color='green'>assemble</font>** task 不依赖于它，当测试运行时它会替代 **<font color='green'>assemble</font>** 并自动调用。

目前只有一个 *Build Type* 会被测试。默认情况下是 **<font color='green'>debug</font>** *Build Type*，可以通过以下代码进行自定义配置：

``` Groovy
android {
    ...
    testBuildType "staging"
}
```

[1]: http://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.ProductFlavor.html