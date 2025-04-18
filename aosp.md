# 什么是 AOSP ？ 
Android系统作为一个庞大的开源项目，除了一些谷歌自带服务之外，其他所有代码均以AOSP（Android Open Source Project）的形式开源。对于框架开发者来说，熟悉AOSP是必不可少的知识。即使是普通开发者，为了优化代码或者是调用一些系统底层API，有时也需要参考底层源码。那么就需要搭配一个合适的源码阅读环境了。

使用 AOSP 代码编译固件时，一共可以编译三种固件：

* user：限制所有权限，用于发布给用户使用的最终版本。
* userdebug： 开放部分权限，允许root。
* eng：工程师模式，开放所有权限并且有额外的调试工具。

# AOSP 如何在线阅读源码？

1. 查看方式
   
    * google官方：https://cs.android.com/    除可以查看 Android的源码，AndroidX的也可以查看  

    * 国内镜像：http://aospxref.com/        只能查看 Android的源码

2. Android 和 AndroidX 区别

   简而言之，AndroidX是Google针对Android平台推出的下一代支持库，旨在解决原支持库中的一些限制，并提供更强的灵活性、更好的维护性和更高的性能。对于开发者来说，迁移到AndroidX可以获得最新的功能和改进，同时也能确保应用在未来得到更好的支持。如果你正在开始一个新的Android项目，强烈推荐直接采用AndroidX；而对于现有的项目，则可以根据实际情况考虑是否进行迁移。

    * ```Android``` 在早期，Android 提供了一系列的支持库（Support Libraries），旨在为开发者提供向后兼容性以及一些额外的UI组件和工具类。这些库允许开发者使用较新的API，即使是在旧版本的Android设备上也能正常工作。支持库包括了多个版本，如v4, v7, v8, v13等，每个版本都有其特定的目标API级别和功能集。
    
    * ```AndroidX``` 鉴于支持库变得越来越复杂，并且为了更好地管理依赖关系，Google推出了AndroidX作为支持库的新一代替代品。AndroidX是对原有支持库的一个重大改进，提供了更好的模块化、更清晰的命名空间以及长期的支持承诺。AndroidX不仅包含了所有之前支持库的功能，还引入了许多新特性，并且更加注重向后兼容性和跨版本的一致性。


4. Android库中有很多子项目

    * ```art```  Android Runtime，目录包含了 Android 运行时的实现，它是 Android 应用程序执行的核心部分之一。ART 是 Dalvik 虚拟机的继承者，从 Android 5.0（Lollipop）开始被引入，旨在提高应用程序性能和效率。提供了一个高性能的运行环境，支持预编译代码以加快应用启动速度。
包括垃圾回收、解释器、即时编译器（JIT）、Ahead-of-Time (AOT) 编译等功能。

    * ```bionic``` 是 Android 的 C 标准库实现，它提供了对 C 语言标准库的支持，并针对移动设备进行了优化。实现了大部分 POSIX 标准接口。包含了自己的 libc（C library）、libm（math library）、libdl（dynamic linking library）等库。设计上注重减少内存占用和提高性能，适合移动设备使用。

    * ```bootable``` 目录包含与引导加载过程相关的所有组件，如 bootloader 和 recovery image。bootloader: 引导加载程序是系统启动时首先运行的软件，负责初始化硬件并加载操作系统内核。recovery: 恢复模式允许用户进行系统更新、擦除数据等操作，而不依赖于正常的Android系统环境。

    * ```build``` 包含构建Android系统所需的各种脚本和配置文件。提供了用于编译整个Android源码树的工具和规则。

    * ```cts``` (Compatibility Test Suite)，CTS 是确保设备与Android兼容性的重要测试套件。提供了一系列自动化测试，帮助开发者验证他们的设备或应用是否符合Android兼容性定义文档(CDD)的要求。

    * ```dalvik```  Dalvik 是Android早期使用的虚拟机，但在Android 5.0之后被ART（Android Runtime）取代。在较新的Android版本中，dalvik目录可能不再活跃使用。

    * ```developers``` 这个目录通常包含面向开发者的示例代码、指南和其他资源。帮助开发者更好地理解和使用Android平台。

    * ```development``` 包含了一些开发工具和示例代码，有助于开发者了解如何扩展Android的功能。提供了开发环境设置脚本、IDE配置等。

    * ```device```   包含针对不同硬件设备的具体实现细节。针对特定设备的定制化配置、内核调整以及设备特有的库和应用程序。

    * ```frameworks```  核心框架代码，包括Android的服务和Java API层。提供了Android应用运行的基础架构，如Activity管理、包管理、电话服务等。

    * ```hardware``` 包含与硬件抽象层（HAL）相关的库和实现。定义了Android与底层硬件交互的标准接口。

    * ```kernel``` Android基于Linux内核，此目录包含了不同设备的内核源码。 提供了Android操作系统的核心组件之一，负责管理系统资源、进程调度等。

    * ```libcore``` 实现了核心的Java库，如java.*和javax.*命名空间下的类。 支持Android应用程序运行所必需的基本Java库。

    * ```libnativehelper``` 提供了JNI（Java Native Interface）支持，使得Java代码可以调用C/C++代码。为Android提供了一种机制，让高级语言能够与本地代码交互。

    * ```packages``` 包含了预装的应用程序和服务，如计算器、日历、浏览器等。提供了标准的Android应用和服务，它们作为系统的一部分被安装到设备上。

    * ```pdk``` （Platform Development Kit）提供给OEM厂商用来开发和测试新设备的工具和资源集合。支持快速集成和测试新硬件。

    * ```platform_testing``` 包含了平台级别的测试工具和测试用例。 用于验证Android平台自身及其组件的功能正确性。

    * ```sdk``` 软件开发工具包，提供了开发Android应用所需的工具和API。包括SDK管理器、模拟器、调试桥（ADB）、命令行工具等。

    * ```system``` 系统级的库和服务，不直接属于框架或应用层。提供了低级别的系统服务和库，支持系统的高效运行。

    * ```test``` 包含了各种类型的测试，如单元测试、集成测试等。用于验证Android系统及其组件的正确性和稳定性。

    * ```toolchain``` 编译工具链，包括编译器、链接器和其他必要的工具。支持将源代码编译成可在目标设备上运行的二进制文件。

    * ```tools``` 包含了多种开发和调试工具。如external中的第三方库和工具，prebuilts中的预编译工具链等。

    * ```trusty```   Trusty是一个安全的操作系统，设计用于保护敏感数据和操作。提供了一个隔离环境来执行高安全性要求的任务，比如支付处理。



参考资料：https://zhuanlan.zhihu.com/p/574856795
