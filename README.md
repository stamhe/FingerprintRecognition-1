# FingerprintRecognition
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;指纹识别，除了api>=23的支持指纹识别的设备，还支持api&lt;23的具有指纹识别硬件支持的设备（前提是这些设备兼容了Google官方的标准接口）
## 指纹识别用途
大概列举几个指纹识别的用途

1. 系统解锁
2. 应用锁
3. 支付认证
4. 普通的登录认证


## 指纹识别适配
指纹识别适配会有很多问题，这些问题可以从下面三种情况中看出。

1. Google官方支持指纹识别的标准接口是在Android6.0开始的，如果各个厂商都升级到6.0并且硬件上都给予支持，那么我们按照标准的指纹识别接口使用就可以了。
2. 如果在android6.0发布以后，手机厂商来不及升级，但是工程师们参考了官方指纹识别的代码，把代码移植到他们的6.0版本以下的系统，或者参照Google提供的接口自己实现了一套指纹识别机制，只是对开发者暴露的接口一样，这样就可以像使用标准接口一样使用，但是这种情况就难说了，实现不好的可能本身就有很多bug，适配起也比较麻烦，不过起码还是能用的。
3. 如果厂商在Google之前就已经做了指纹识别，那这种情况肯定不能使用官方标准接口，如果要适配这种设备，只能使用厂商提供的第三方指纹识别SDK。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一般情况下只需要跟着Google官方走就行，6.0以下系统直接不支持，这样也省去很多适配问题。但是如果一个app拥有大量第三方厂商6.0以下的设备，非要支持指纹识别功能，那么只能去做支持了。对于上面提到的三种情况，前面两种情况代码写法是一致的，只需要按照Google官方文档写就行了，只是不再需要api>=23的逻辑判断，代码会有警告，还必须使用try catch进程异常捕获，因为鬼都不知道厂商系统内部会发生什么崩溃出来（红米note3,系统5.0或者5.1的，调用mFingerprintManager.hasEnrolledFingerprints()方法时，内部抛出空指针异常）。第三种情况如果要做支持，只能通过公司合作的方式去找厂商提供SDK了。

## 指纹识别操作截图
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目中只对上文提到的前面两种情况做支持，下面是在Vivo V3（系统5.1.1，api 22）设备上操作截图。

主界面：

![未开始使用](/docpic/fingerprint1.png "指纹识别默认界面，点击开始指纹识别按钮启动指纹识别功能")

开始指纹识别

![开始](/docpic/fingerprint2.png "可以长按指纹解锁键进行指纹识别")

指纹识别结果

![识别成功](/docpic/fingerprint3.png "指纹识别成功提示")

## 操作动画演示

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;动画有8M左右，所有导致项目有点大，不过为了读者更加形象了解并理解指纹解锁。动画中无法看到手指长按指纹识别按键的部分，只能看到识别成功失败的结果。

![动画演示](/docpic/vivo_v3_fingerprint.gif "演示操作流程")

## 经验总结
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;指纹识别虽然适配上有很多问题，安全性方面也还不完善，但是指纹识别的快捷体验确实不错，用在一些不需要关注安全性能的产品上是完全可以的。如果您想了解指纹识别，您想知道指纹识别怎么视频不同的api版本，那么本项目值得参考。知识这东西，说不听什么时候它就起作用了，技多不压身，多学习多了解是好事。