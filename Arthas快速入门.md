## Arthas快速入门

1. #### 简介

   Arthas是Alibaba开源的一款Java诊断工具，方便开发者在线排查问题，无需重启，同时可以跟踪Java代码，实时监控JVM状态，目前Arthas仅支持JDK6+，支持Linux/Mac/Windows，采用命令行交互模式，具有 `Tab` 自动补全功能，便于开发者进行快速定位和诊断问题。

2. #### 下载及启动arthas

   * 首先启动需要监测的项目。
   * 下载Arthas，下载地址：https://arthas.aliyun.com/arthas-boot.jar 。
   * 打开命令终端窗口运行Arthas，Arthas根目录下执行命令：`java -jar arthas-boot.jar`。
   * Arthas启动会列出所有的Java进程，并显示序号。
   * 输入需要监测项目的序号，回车。（监测成功的情况，会显示Arthas的LOGO）

3. 选择项目进程并通过dashboard查看项目状态

   在终端中输入命令：`dashboard`并回车。

   ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4a1fc5e63204880af10301e8210e2ac~tplv-k3u1fbpfcp-watermark.image)

   如图会展示线程信息，内存信息，运行系统。

   线程信息中包含线程id，我们可以根据线程id查看线程栈，如图main方法的线程id是1，我们执行命令：`thread 1`。

   ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9eefc5226b104c449d87aaa59352067b~tplv-k3u1fbpfcp-watermark.image)

   如图，可以清楚看到main方法中的栈信息。在栈内存中，我们看到main方法路径是：`demo.MathGame.main`，也就是说main方法在demo.MathGame下。

4. 通过jad反编译指定class

   现在我们找到MathGmae类并进行反编译，看看它的源码：

   - 终端执行命令：`sc -d *MathGame`。

     ![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4305641af44843fd84aba26dfa470332~tplv-k3u1fbpfcp-watermark.image)

     已经找到了这个类，并看到了这个类的相关信息。

   - 在终端控制台执行命令：`jad demo.MathGame`。

     ![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a9e8f11efedf4ad0a53d9a38e95e145c~tplv-k3u1fbpfcp-watermark.image)

     如图，即可看到整个类的源码了。

     同时，我们还可以输入命令：`watch demo.MathGame primeFactors returnObj`来查看函数的参数/返回值/异常信息。

     ![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6a7c84e37a3f44e48714de18003430cb~tplv-k3u1fbpfcp-watermark.image)

5. Profiler对项目采样生成火焰图

   `Profiler`命令支持生成应用热点的火焰图。本质上是通过不断的采样，然后把收集到的采样结果生成火焰图。

   `profiler`命令基本运行结构是 profiler action [actionArg]，我们可以通过执行命令：`profiler actions`来查看所有支持的action。

   `profiler`命令的版本，可以通过命令：`profiler version`查看。

   ###### Profiler参数说明

   | 参数名称    | 参数说明                                                     |
   | ----------- | ------------------------------------------------------------ |
   | *action*    | 要执行的操作                                                 |
   | *actionArg* | 属性名模式                                                   |
   | [i:]        | 采样间隔（单位：ns）（默认值：10'000'000，即10 ms）          |
   | [f:]        | 将输出转储到指定路径                                         |
   | [d:]        | 运行评测指定秒                                               |
   | [e:]        | 要跟踪哪个事件（cpu, alloc, lock, cache-misses等），默认是cpu |

   我们先看看如何查看cpu的火焰图。

   执行命令：`profiler start -e cpu`

   ![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fa536232f7a74f8abcfcccae4d83c842~tplv-k3u1fbpfcp-watermark.image)

   可以看到，cpu的火焰图正在绘制，执行命令`profiler status`可以看到profiler的状态，可以看到什么任务执行了多久。

	![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/adddb74d561f4d839e8a19d021fe1c0a~tplv-k3u1fbpfcp-watermark.image)

   当我们觉得检测的差不多了，可以看结果了，就执行命令`profiler stop`，会输出一张svg图片到output路径。
   
   output路径也可以手动指定，执行命令：`profiler stop --file 路径+文件名.svg`就能在指定路径输出svg火焰图了。	
   
   profiler不仅能生成出svg火焰图，还能生成html格式，执行命令`profile stop --format html`或`profile stop --file 路径+文件名.svg`就能生成出来了。

#### 总结

Arthas是一款十分优秀的Java应用诊断利器，内置了丰富的功能命令，是Java程序员排查jvm相关问题的利器。
