# 鸿蒙 Fastlane 流水线搭建

做为客户端开发者，相信 Fastlane 大家都很熟悉，都多少接触并使用过。我们一般都用在 android 和 ios 等平台的项目构建上，包括自动化测试，自动化部署等。但是鸿蒙应用使用 Fastlane 构建，相信这里是头一份儿。

## 开始

### 安装 fastlane

这里 Fastlane 的安装等就不做什么过多介绍了，按照[开发文档](https://docs.fastlane.tools/)一路下一步就可以完成。

### 初始化 fastlane

直接步入正题吧，这里方便演示使用的是一个idea新建的空项目。

首先到项目目录下初始化 fastlane

```shell
> fastlane init

[✔] 🚀 
[✔] Looking for iOS and Android projects in current directory...
[14:04:57]: Created new folder './fastlane'.
[14:04:57]: No iOS or Android projects were found in directory '/Users/dede/Workspace/Fake/HarmonyFastlaneDemo'
[14:04:57]: Make sure to `cd` into the directory containing your iOS or Android app
[14:04:57]: Alternatively, would you like to manually setup a fastlane config in the current directory instead? (y/n)
```

由于默认 fastlane 只支持 android、ios/mac 和 跨平台项目的构建，对 鸿蒙 项目也是比较陌生，会无法识别，这里直接 `y` 选择手动配置，一路按回车，直到结束

```log
[14:07:31]: -----------------------------
[14:07:31]: --- Welcome to fastlane 🚀 ---
[14:07:31]: -----------------------------
[14:07:31]: fastlane can help you with all kinds of automation for your mobile app
[14:07:31]: We recommend automating one task first, and then gradually automating more over time
[14:07:31]: ------------------------------------------------------------
[14:07:31]: --- Setting up fastlane so you can manually configure it ---
[14:07:31]: ------------------------------------------------------------
[14:07:31]: It looks like your project isn't set up to do automatic version incrementing
[14:07:31]: To enable fastlane to handle automatic version incrementing for you, please follow this guide:
[14:07:31]:     https://developer.apple.com/library/content/qa/qa1827/_index.html
[14:07:31]: Afterwards check out the fastlane docs on how to set up automatic build increments
[14:07:31]:     https://docs.fastlane.tools/getting-started/ios/beta-deployment/#best-practices
[14:07:31]: Installing dependencies for you...
[14:07:31]: $ bundle update
[14:07:41]: --------------------------------------------------------
[14:07:41]: --- ✅  Successfully generated fastlane configuration ---
[14:07:41]: --------------------------------------------------------
[14:07:41]: Generated Fastfile at path `./fastlane/Fastfile`
[14:07:41]: Generated Appfile at path `./fastlane/Appfile`
[14:07:41]: Gemfile and Gemfile.lock at path `Gemfile`
[14:07:41]: Please check the newly generated configuration files into git along with your project
[14:07:41]: This way everyone in your team can benefit from your fastlane setup
[14:07:41]: Continue by pressing Enter ⏎

[14:07:45]: fastlane will collect the number of errors for each action to detect integration issues
[14:07:45]: No sensitive/private information will be uploaded, more information: https://docs.fastlane.tools/#metrics
[14:07:45]: ----------------------
[14:07:45]: --- fastlane lanes ---
[14:07:45]: ----------------------
[14:07:45]: fastlane uses a `Fastfile` to store the automation configuration
[14:07:45]: Within that, you'll see different lanes.
[14:07:45]: Each is there to automate a different task, like screenshots, code signing, or pushing new releases
[14:07:45]: Continue by pressing Enter ⏎

[14:07:47]: --------------------------------------
[14:07:47]: --- How to customize your Fastfile ---
[14:07:47]: --------------------------------------
[14:07:47]: Use a text editor of your choice to open the newly created Fastfile and take a look
[14:07:47]: You can now edit the available lanes and actions to customize the setup to fit your needs
[14:07:47]: To get a list of all the available actions, open https://docs.fastlane.tools/actions
[14:07:47]: Continue by pressing Enter ⏎

[14:07:48]: ------------------------------
[14:07:48]: --- Where to go from here? ---
[14:07:48]: ------------------------------
[14:07:48]: 📸  Learn more about how to automatically generate localized App Store screenshots:
[14:07:48]:             https://docs.fastlane.tools/getting-started/ios/screenshots/
[14:07:48]: 👩‍✈️  Learn more about distribution to beta testing services:
[14:07:48]:             https://docs.fastlane.tools/getting-started/ios/beta-deployment/
[14:07:48]: 🚀  Learn more about how to automate the App Store release process:
[14:07:48]:             https://docs.fastlane.tools/getting-started/ios/appstore-deployment/
[14:07:48]: 👩‍⚕️  Learn more about how to setup code signing with fastlane
[14:07:48]:             https://docs.fastlane.tools/codesigning/getting-started/
[14:07:48]: 
[14:07:48]: To try your new fastlane setup, just enter and run
[14:07:48]: $ fastlane custom_lane
```

这里 fastlane 就初始化完成了，查看项目文件就已经帮我们创建好了fastlane必须的文件

![fastlane dir](https://assets.che300.com/wiki/2024-09-27/17274175409166461.png)

### 自定义 lane

打开 `Fastfile` 文件，已经帮我们新建了一个默认的 `custom_lane`

```ruby
default_platform(:ios)

platform :ios do
  desc "Description of what the lane does"
  lane :custom_lane do
    # add actions here: https://docs.fastlane.tools/actions
  end
end
```

我们可以尝试运行一下。

```shell
> fastlane custom_lane

[✔] 🚀 
[14:16:31]: fastlane detected a Gemfile in the current directory
[14:16:31]: However, it seems like you didn't use `bundle exec`
[14:16:31]: To launch fastlane faster, please use
[14:16:31]: 
[14:16:31]: $ bundle exec fastlane custom_lane
[14:16:31]: 
[14:16:31]: Get started using a Gemfile for fastlane https://docs.fastlane.tools/getting-started/ios/setup/#use-a-gemfile
[14:16:31]: ------------------------------
[14:16:31]: --- Step: default_platform ---
[14:16:31]: ------------------------------
[14:16:31]: Driving the lane 'ios custom_lane' 🚀

+---------------------------------------+
|           fastlane summary            |
+------+------------------+-------------+
| Step | Action           | Time (in s) |
+------+------------------+-------------+
| 1    | default_platform | 0           |
+------+------------------+-------------+

[14:16:31]: fastlane.tools finished successfully 🎉
```

可以看到已经运行成功了，默认的模板是ios平台，我们让 fastlane 入乡随俗，改为 harmony 平台

```ruby
default_platform(:harmony)

platform :harmony do
  desc "Description of what the lane does"
  lane :custom_lane do
    puts "Hello World!"
    # add actions here: https://docs.fastlane.tools/actions
  end
end
```

再次运行 `fastlane custom_lane` 并成功输出 `Hello World!`

```shell
> fastlane custom_lane

[✔] 🚀 
[14:18:45]: fastlane detected a Gemfile in the current directory
[14:18:45]: However, it seems like you didn't use `bundle exec`
[14:18:45]: To launch fastlane faster, please use
[14:18:45]: 
[14:18:45]: $ bundle exec fastlane custom_lane
[14:18:45]: 
[14:18:45]: Get started using a Gemfile for fastlane https://docs.fastlane.tools/getting-started/ios/setup/#use-a-gemfile
[14:18:45]: ------------------------------
[14:18:45]: --- Step: default_platform ---
[14:18:45]: ------------------------------
[14:18:45]: Platform 'harmony' is not officially supported. Currently supported platforms are [:ios, :mac, :android].
[14:18:45]: Platform 'harmony' is not officially supported. Currently supported platforms are [:ios, :mac, :android].
[14:18:45]: Driving the lane 'harmony custom_lane' 🚀
[14:18:45]: Hello World!

+---------------------------------------+
|           fastlane summary            |
+------+------------------+-------------+
| Step | Action           | Time (in s) |
+------+------------------+-------------+
| 1    | default_platform | 0           |
+------+------------------+-------------+

[14:18:45]: fastlane.tools finished successfully 🎉
```

可以看到 fastlane 说 harmony 是不支持的平台，这里可以忽略它，因为不会影响构建

### Harmony 打包命令

鸿蒙打包脚本使用的时 **hvigor** 命令，它被集成在 **DevEco Studio** 和 **Command Line Tools** 中，可以在这里 [下载](https://developer.huawei.com/consumer/cn/download/)。由于我们要搭建流水线，可以直接下载对应平台的 **Command Line Tools** 工具解压即可。同时将 `comand-line-tools/bin` 目录设置到 **PATH** 环境变量中。

#### 构建 Hap 包

像我们开发和测试期间的鸿蒙安装包，都是 .hap 格式，我们可以通过如下命令来构建：

```shell
hvigorw assembleHap --mode module -p product=default -p buildMode=release --no-daemon
```

命令和 gradle 项目很类似。执行完成后就可以看到 Hap 产物已经出现在了输出路径下

![Hap output](https://assets.che300.com/wiki/2024-09-27/17274187486198193.png)

由于这里只是演示，我们没有配置 release 签名，所以生成的 Hap 是没有签名的。

#### 构建 App 商店包

鸿蒙应用商店需要上传 .app 文件，.hap 是不能进行发布的。就类似于 play 商店要求传 .aab 而不是 .apk 一样

```shell
hvigorw assembleApp --mode project -p product=default -p buildMode=release --no-daemon
```

![App output](https://assets.che300.com/wiki/2024-09-27/17274190620931102.png)

#### hvigorw 参数解析

* assembleApp、assembleHap: 任务名称，当然还有 clean 、init 等任务
* --mode: 构建的项目，类似于构建 module 还是构建 整个项目（hap 可以单独构建 module，app 需要构建整个项目）
* -p product=default: 产品类型，我们可以在 `build-profile.json5` 中定义不同的产品来区分不同的功能，例如：fortest、product等等，默认为default
* -p buildMode=release: 编译模式，默认有 debug 和 release，我们也可以在 `build-profile.json5` 定制
* --no-daemon: 不开启守护进程

#### 固定产物名称

通过两次打包我们发现，我们打包时的产物名称不是固定的，是通过项目和module的名称来生成的，我们如果要用流水线，最好固定一下产物的命名格式。

我们可以在 module 和 项目的 build-profile.json5 中添加如下声明固定产物名称：

项目级的 build-profile.json5 用于控制 App 的生成名称

```json
{
  "app": {
    "products": [
      {
        "name": "default",
        "output": {
          "artifactName": "hm_fastlane_demo"
        },
        // ...
      },
    ],
  }
}
```

module 级的 build-profile.json5 用于控制 Hap 的文件名

```json
{
  "apiType": "stageMode",
  // ...
  "targets": [
    {
      "name": "default",
      "output": {
        "artifactName": "hm_fastlane_demo"
      }
    },
  ]
}
```

### 将 hvigorw 命令封装成 lane

既然已经知道了鸿蒙的打包命令，我们就可以将这些命令封装成fastlane 自定义 lane 来调用。

我们将 task、product、build_mode和自定义参数 进行封装，组成了一个 `hvigor` 的 private lane（私有只能被其他lane调用），并定义了一个 `build_hap` lane 调用它

```ruby
default_platform(:harmony)

platform :harmony do
  desc "hvigor 命令行"
  private_lane :hvigor do |options|
    task = options[:task]
    product = options[:product]
    build_mode = options[:build_mode]
    args = options[:args]
    if args.nil?
      args = []
    end
    if !product.nil?
      args = args + ["-p", "product=#{product}"]
    end
    if !build_mode.nil?
      args = args + ["-p", "buildMode=#{build_mode}"]
    end
    if task.nil?
      cmds = ["hvigorw"] + args
    else
      cmds = ["hvigorw", task] + args
    end
    # 指定工作路径，fastlane 路径上一级，也就是项目的根路径
    Dir.chdir("../") do 
      sh cmds
    end
  end

  desc "Hap打包"
  lane :build_hap do
    # 安装依赖
    Dir.chdir("../") do
      sh("ohpm install --all")
    end

    hvigor(task: "clean")
    hvigor(
      task: "assembleHap",
      product: "default",
      build_mode: "release",
      args: ["--mode", "module", "--no-daemon"],
    )
  end
end
```

运行 `fastlane build_hap` 查看结果，发现成功运行了。

```log
+------+-------------------------------+-------------+
| Step | Action                        | Time (in s) |
+------+-------------------------------+-------------+
| 1    | default_platform              | 0           |
| 2    | Switch to harmony hvigor lane | 0           |
| 3    | hvigorw                       | 1           |
| 4    | Switch to harmony hvigor lane | 0           |
| 5    | hvigorw                       | 5           |
+------+-------------------------------+-------------+

[14:56:39]: fastlane.tools finished successfully 🎉
```

### 上传打包产物

上面的步骤已经成功通过 fastlane 构建了鸿蒙项目了，我们可以在构建成功后将hap 和 app上传的分发平台（目前还没有）或者文件服务上。由于项目的情况不同，这里简单演示怎么上传到minio

minio 提供了 `mc` 命令行工具，对文件服务的访问和管理，我们只需要简单封装成 lane 就可以供fastlane使用

```ruby
  desc "上传文件到MinIO file_path: 文件路径, remote_path: 上传文件夹路径"
  lane :upload_to_minio do |options|
    file_path = options[:file_path]
    remote_path = options[:remote_path]
    if !File::exist?(file_path)
      puts "⚠️ Upload to MinIO file not exist: #{file_path}"
      next
    end
    file_name = File::basename(file_path)
    sh("mc", "cp", file_path, "#{remote_path}/#{file_name}")
  end
```

再改造一下我们的 `build_hap` lane

```ruby
  desc "Hap打包"
  lane :build_hap do
    # 安装依赖
    Dir.chdir("../") do
      sh("ohpm install --all")
    end

    hvigor(task: "clean")
    hvigor(
      task: "assembleHap",
      product: "default",
      build_mode: "release",
      args: ["--mode", "module", "--no-daemon"],
    )

    # 在module级的build-profile.json5中指定产物名称
    # "output": { "artifactName": "hm_fastlane_demo" }
    hap_path = File::expand_path("../entry/build/default/outputs/default/hm_fastlane_demo-unsigned.hap")
    # 获取版本号
    version_name = JSON.parse(File.read("../AppScope/app.json5"))["app"]["versionName"]
    # 重命名
    hap_name = "#{File::basename(hap_path, ".hap")}_#{version_name}.hap"
    new_hap_path = File::join(File::dirname(hap_path), hap_name)
    File::rename(hap_path, new_hap_path)
    puts "Build output: #{new_hap_path}"

    # 上传minio
    upload_to_minio(
      file_path: new_hap_path,
      remote_path: "internal/harmony"
    )
  end
```

再次运行 `fastlane build_hap` lane，构建并上传成功

```shell
+------------------------------------------------------------------------------------+
|                                  fastlane summary                                  |
+------+---------------------------------------------------------------+-------------+
| Step | Action                                                        | Time (in s) |
+------+---------------------------------------------------------------+-------------+
| 1    | default_platform                                              | 0           |
| 2    | ohpm install --all                                            | 0           |
| 3    | Switch to harmony hvigor lane                                 | 0           |
| 4    | hvigorw                                                       | 0           |
| 5    | Switch to harmony hvigor lane                                 | 0           |
| 6    | hvigorw                                                       | 6           |
| 7    | Switch to harmony upload_to_minio lane                        | 0           |
| 8    | mc cp /Users/dede/Workspace/Fake/HarmonyFastlaneDemo/entry/bu | 0           |
+------+---------------------------------------------------------------+-------------+

[15:18:18]: fastlane.tools finished successfully 🎉
```

![minio file](https://assets.che300.com/wiki/2024-09-27/17274218237627369.png)

上传成功后面我们可以添加消息通知，例如钉钉机器人消息，通知到我们的其他小伙伴

## 更进一步

上面的演示都是基于本地系统的命令行工具进行构建的，我们可以在 Jenkins 、gitlab job 或者 github workflow 中调用 fastlane 流水线，进行自动化构建。

但是目前鸿蒙系统正在处于快速迭代的周期，很多功能和工具可能不太稳定。假如命令行工具出现了不兼容的问题，而 Jenkins 上正好又有多个需要不同版本命令行工具的项目，这种情况我们要如何处理呢。

我们可以在 fastlane 中进行构建环境的切换，将环境准备封装到一个单独的lane中

```ruby
  desc "构建环境准备"
  private_lane :prepare do
    # todo 命令行工具下载并切换

    sh "java --version"
    sh "ohpm -v"
    Dir.chdir("../") do
      sh("ohpm install --all")
    end
    hvigor(args: ["-v"])
  end
```

但是发现鸿蒙并没有提供可以直接下载的地址，下载地址也有签名校验，所以我们只能将需要的版本提前下载到打包Jenkins的宿主设备上，然后通过脚本来动态切换

```ruby
# 命令行工具
COMMAND_LINE_TOOLS_PLATFORM = "mac-arm64"# 打包机的平台架构
COMMAND_LINE_TOOLS_VERSION = "5.0.3.810"
# 依赖环境变量 HM_COMMAND_LINE_TOOLS_REPO 配置的命令行仓库路径
# 如果需要新版本，就将新下载的zip包放到此路径下

default_platform(:harmony)

platform :harmony do
  desc "构建环境准备"
  private_lane :prepare do
    command_line_tools_repo = ENV["HM_COMMAND_LINE_TOOLS_REPO"]
    puts "$HM_COMMAND_LINE_TOOLS_REPO: #{command_line_tools_repo}"
    if !command_line_tools_repo.nil?
      command_line_tools_zip = File::join(command_line_tools_repo, "commandline-tools-#{COMMAND_LINE_TOOLS_PLATFORM}-#{COMMAND_LINE_TOOLS_VERSION}.zip")
      command_line_tools_unzip = File::join(command_line_tools_repo, "unzip", COMMAND_LINE_TOOLS_VERSION)
      command_line_tools_home = File::join(command_line_tools_unzip, "command-line-tools")
      if !File::exist?(command_line_tools_home)
        if !File::exist?(command_line_tools_unzip)
          sh "mkdir -p #{command_line_tools_unzip}"
        end

        sh "unzip #{command_line_tools_zip} -d #{command_line_tools_unzip}"
      end
      # 更新环境变量
      ENV["NODE_HOME"] = "#{command_line_tools_home}/tool/node"
      ENV["PATH"] = "#{command_line_tools_home}/bin:$NODE_HOME/bin:#{ENV["PATH"]}"
      puts "$PATH: #{ENV["PATH"]}"
    end

    sh "java --version"
    sh "ohpm -v"
    Dir.chdir("../") do
      sh("ohpm install --all")
    end
    hvigor(args: ["-v"])
  end

  desc "Hap打包"
  lane :build_hap do
    prepare

    hvigor(task: "clean")
    hvigor(
      task: "assembleHap",
      product: "default",
      build_mode: "release",
      args: ["--mode", "module", "--no-daemon"],
    )
    # ...
  end
end
```

上面的 `prepare` lane 通过读取 `HM_COMMAND_LINE_TOOLS_REPO`环境变量 来找到命令行工具集的地址，内部会包含需要的命令行工具版本，按照需要会进行解压并更新 `PATH` 环境变量。

这里出于演示手动设置了 HM_COMMAND_LINE_TOOLS_REPO 环境变量

```shell
export HM_COMMAND_LINE_TOOLS_REPO="/Users/dede/Downloads/hm_cmdline_tools_repo"

// 此路径结构如下
├── commandline-tools-mac-arm64-5.0.3.810.zip
├── commandline-tools-mac-arm64-5.x.x.xxx.zip// 如果需要新版本就下载到这里
└── unzip
    └── 5.0.3.810
```

再次运行 `fastlane build_hap`

```shell

fastlane build_hap
```

```log
+------------------------------------------------------------------------------------+
|                                  fastlane summary                                  |
+------+---------------------------------------------------------------+-------------+
| Step | Action                                                        | Time (in s) |
+------+---------------------------------------------------------------+-------------+
| 1    | default_platform                                              | 0           |
| 2    | Switch to harmony prepare lane                                | 0           |
| 3    | mkdir -p /Users/dede/Downloads/hm_cmdline_tools_repo/unzip/5. | 0           |
| 4    | unzip /Users/dede/Downloads/hm_cmdline_tools_repo/commandline | 62          |
| 5    | java --version                                                | 0           |
| 6    | ohpm -v                                                       | 4           |
| 7    | ohpm install --all                                            | 0           |
| 8    | Switch to harmony hvigor lane                                 | 0           |
| 9    | hvigorw                                                       | 1           |
| 10   | Switch to harmony hvigor lane                                 | 0           |
| 11   | hvigorw                                                       | 2           |
| 12   | Switch to harmony hvigor lane                                 | 0           |
| 13   | hvigorw                                                       | 29          |
| 14   | Switch to harmony upload_to_minio lane                        | 0           |
| 15   | mc cp /Users/dede/Workspace/Fake/HarmonyFastlaneDemo/entry/bu | 0           |
| 16   | Switch to harmony push_msg lane                               | 0           |
+------+---------------------------------------------------------------+-------------+

[15:59:35]: fastlane.tools finished successfully 🎉
```

可以看到，命令行工具解压设置环境变量并成功构建了。可以看出unzip是比较耗时的，所以这里对已经解压过的版本进行了复用，加快构建速度。

### 完整的Fastfile

```ruby
# 命令行工具
COMMAND_LINE_TOOLS_PLATFORM = "mac-arm64"# 打包机的平台架构
COMMAND_LINE_TOOLS_VERSION = "5.0.3.810"
# 依赖环境变量 HM_COMMAND_LINE_TOOLS_REPO 配置的命令行仓库路径
# 如果需要新版本，就将新下载的zip包放到此路径下

default_platform(:harmony)

platform :harmony do
  desc "构建环境准备"
  private_lane :prepare do
    command_line_tools_repo = ENV["HM_COMMAND_LINE_TOOLS_REPO"]
    puts "$HM_COMMAND_LINE_TOOLS_REPO: #{command_line_tools_repo}"
    if !command_line_tools_repo.nil? # 没有HM_COMMAND_LINE_TOOLS_REPO环境变量就使用系统命令行工具
      command_line_tools_zip = File::join(command_line_tools_repo, "commandline-tools-#{COMMAND_LINE_TOOLS_PLATFORM}-#{COMMAND_LINE_TOOLS_VERSION}.zip")
      command_line_tools_unzip = File::join(command_line_tools_repo, "unzip", COMMAND_LINE_TOOLS_VERSION)
      command_line_tools_home = File::join(command_line_tools_unzip, "command-line-tools")
      if !File::exist?(command_line_tools_home)
        if !File::exist?(command_line_tools_unzip)
          sh "mkdir -p #{command_line_tools_unzip}"
        end

        sh "unzip #{command_line_tools_zip} -d #{command_line_tools_unzip}"
      end
      # 更新环境变量
      ENV["NODE_HOME"] = "#{command_line_tools_home}/tool/node"
      ENV["PATH"] = "#{command_line_tools_home}/bin:$NODE_HOME/bin:#{ENV["PATH"]}"
      puts "$PATH: #{ENV["PATH"]}"
    end

    sh "java --version"
    sh "ohpm -v"
    Dir.chdir("../") do
      sh("ohpm install --all")
    end
    hvigor(args: ["-v"])
  end

  desc "hvigor 命令行"
  private_lane :hvigor do |options|
    task = options[:task]
    product = options[:product]
    build_mode = options[:build_mode]
    args = options[:args]
    if args.nil?
      args = []
    end
    if !product.nil?
      args = args + ["-p", "product=#{product}"]
    end
    if !build_mode.nil?
      args = args + ["-p", "buildMode=#{build_mode}"]
    end
    if task.nil?
      cmds = ["hvigorw"] + args
    else
      cmds = ["hvigorw", task] + args
    end
    # 指定工作路径，fastlane 路径上一级，也就是项目的根路径
    Dir.chdir("../") do
      sh cmds
    end
  end

  desc "上传文件到MinIO file_path: 文件路径, remote_path: 上传文件夹路径"
  lane :upload_to_minio do |options|
    file_path = options[:file_path]
    remote_path = options[:remote_path]
    if !File::exist?(file_path)
      puts "⚠️ Upload to MinIO file not exist: #{file_path}"
      next
    end
    file_name = File::basename(file_path)
    sh("mc", "cp", file_path, "#{remote_path}/#{file_name}")
  end

  desc "Hap打包"
  lane :build_hap do
    prepare

    hvigor(task: "clean")
    hvigor(
      task: "assembleHap",
      product: "default",
      build_mode: "release",
      args: ["--mode", "module", "--no-daemon"],
    )

    # 在module级的build-profile.json5中指定产物名称
    # "output": { "artifactName": "hm_fastlane_demo" }
    hap_path = File::expand_path("../entry/build/default/outputs/default/hm_fastlane_demo-unsigned.hap")
    # 获取版本号
    version_name = JSON.parse(File.read("../AppScope/app.json5"))["app"]["versionName"]
    # 重命名
    hap_name = "#{File::basename(hap_path, ".hap")}_#{version_name}.hap"
    new_hap_path = File::join(File::dirname(hap_path), hap_name)
    File::rename(hap_path, new_hap_path)
    puts "Build output: #{new_hap_path}"

    # 上传minio
    upload_to_minio(
      file_path: new_hap_path,
      remote_path: "internal/harmony",
    )
    
    # 发送消息通知
    push_msg(
      message: "打包成功",
      url: "下载地址"
    )
  end

  lane :push_msg do |options|
    puts "发送消息"
    # todo
  end
end
```

## End

到这里 fastlane 在鸿蒙上的应用就结束了，对鸿蒙的命令行工具和打包工具进行了一次大胆结合，并成功应用。目前公司项目已经使用此方案在Jenkins上进行了部署，目前没有发现问题。

### 参考资料

* [fastlane docs](https://docs.fastlane.tools/)
* [配置多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-customized-multi-targets-and-products-guides-V5)
* [灵活定制编译选项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-hvigor-compilation-options-customizing-guide-V5)
* [搭建流水线](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-command-line-building-app-V5)
