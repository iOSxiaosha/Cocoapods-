# Cocoapods-安装教程
Cocoapods安装教程，参考网上多数文档，结合自身安装过程中遇到的问题，以及提交到svn后遇到的坑，整理而成，如有不足，欢迎指正

一、准备工作

1、检查ruby版本号

sudo gem -v

注：一般都不是最新，需要升级到最新

2、升级到最新版本号

gem update --system

3、检查ruby源

gem sources -l

注：默认是https://rubygems.org/

4、移除ruby源

gem sources --remove https://rubygems.org/

5、替换国内镜像源

gem sources --add https://gems.ruby-china.org

再次检查此时的 ruby 源：（ 已经变成了 ruby-china 源 ）
*** CURRENT SOURCES ***
https://gems.ruby-china.org

注：目前最新的ruby源是ruby-china(2016/12/21)

二、安装Cocoapods

由于 OS X 系统的不同，此处的指令也是有些变化:
OS X 10.11之前系统的安装 CocoaPods 指令： $ sudo gem install cocoapods
OS X 10.11以后系统的安装 CocoaPods 指令： $ sudo gem install -n /usr/local/bin cocoa pods

三、配置

1、检查是否安装成功

pod search 'AFNetworking'
如果能搜索出结果，则说明安装成功

2、安装成功后，执行pod setup命令

这个过程比较慢，需要等一段时间
注： pod setup 是Cocoapods将它的信息下载到 ~/.cocoapods/repos 目录下。即使在安装时不执行此命令，在初次执行 pod install 命令时，系统也会自动执行 pod setup

3、查看setup是否执行成功

cd ~/.cocoapods

接下来输入：

du -sh *

如果显示0B repos，则说明没有安装成功。

重新执行pod setup，稍后会提示setup completed，终端中输入 pod list，展示出安装列表, 如果安装成功则会出现很多；

再一次输入：

pod search 'AFNetworking'

输入过后它可能会报：

[!] Unable to find a pod with name, author, summary, or descriptionmatching `AFNetworking`

解决方案，终端输入：

rm ~/Library/Caches/CocoaPods/search_index.json

再次输入：pod search 'AFNetworking'，就行了！

四、测试

1、创建test工程

2、在工程根目录下，创建Podfile文件

touch Podfile

3、编辑Podfile文件

platform :ios, '7.0'

target '自己的项目名称' do

pod 'AFNetworking', '~>3.1.0'

end

注：platform :ios , 冒号和ios之间不应有空格, ios为小写

4、编辑完，保存退出，执行pod install命令

注：正常等一会就好了，一般都比较快

五、提交svn注意事项

1、Pods文件夹千万不要提交，Pods文件夹千万不要提交， Pods文件夹千万不要提交

注：…/Pods/Pods.xcodeproj …Pods/Target Support Files/这些每次编译都会改动从而引起合并代码的时候冲突

2、只提交Podfile、Podfile.lock和XXX.xcworkspace文件即可(XXX为工程名)

3、同事更新svn，然后执行pod install 安装即可

4、以后打开工程的方式改为打开XXX.xcworkspace文件

六、参考文档

1、http://www.jianshu.com/p/6d8604f0b94c

2、http://www.jianshu.com/p/0cea9006c0cb

3、http://www.jianshu.com/p/fe0bb6b12f9d

4、https://biezhi.me/2016/03/26/cocoaPods-installation-encountered-pit/
