#总结：
##1.use_frameworks!则表明依赖的库编译生成.frameworkds的包，而不是.a的包。
##2.inhibit_warnings参数能够有效的抑制CocoaPods引入的第三方代码库产生的warning，但是有时候会产生意想不到的错误，例如我今天引入ReactiveCocoa的时候就产生了下面的错误 pod 'ReactiveCocoa', '~> 2.1', :inhibit_warnings => true,同理，inhibit_all_warnings也会产生类似的问题
##3. （没太懂是什么意思）  project 'TestProject', 'Mac App Store' => :release, 'Test' => :debug

##4.问题:在cocoapods1.4 之前 对于pods库集成swift库 都是需要我们设置 !use_framework ，这样设置之后所有的pods库都必须使用动态库，但这就带来一个问题，如果我需要集成一个静态库怎么办？
#解决办法:
#1 升级pods
#gem install cocoapods
#2 自己组件库的podsepc 添加s.static_framework = true
#这里有个问题说下，显然 很多第三方你发不了podspec，所以需要对主工程的podfile 做些改造。
#
#pre_install do |installer|
#
#    Pod::PodTarget.send(:define_method, :static_framework?) { return true }
#end
#添加这个代码 我们可以把所有的pods库都设为静态库。
#
#3 podfile 里添加  use_modular_headers!
#或者你可以增对单独的库使用 :modular_headers => true
#pod 'SSZipArchive', :modular_headers => true##
##5.xcodeproj 'OCBase2018'
#xcodeproj,现在被project代替，这个变量就别使用了

#4. use_frameworks!
#使用frameworks动态库替换静态库链接
#(1)swift项目cocoapods 默认 use_frameworks!
#(2)OC项目cocoapods 默认 #use_frameworks!
#5. project
#
#默认情况下是没有指定的，当没有指定时，会使用Podfile目录下与target同名的工程：(我们只有一个工程JYCocoaPodsTest)
## JYCocoaPodsTest这个Target只有在JYCocoaPodsTest工程中才会链接
#target ‘JYCocoaPodsTest’ do
#    project ‘JYCocoaPodsTest’
#    …
#end
# 6    debug测试的时候有这个库,release有这个库
#pod 'PonyDebugger', :configurations => ['Release', 'App Store']
#pod 'AFNetworking', :configurations => ['Debug']
#7. inherit! :search_paths
#明确指定继承于父层的所有pod，默认就是继承的




platform :ios, '8.0'

inhibit_all_warnings!

target 'OCBase2018' do
#nsarry等的扩展
  pod 'ObjectiveSugar', '~> 1.1.0'
#  压缩和解压缩
  pod 'SSZipArchive', '~> 2.1.4'

  target "OCBase2018Tests" do
    inherit! :search_paths
    pod 'OCMock', '~> 2.0.1'  #单元测试
  end
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    puts "#{target.name}"
  end
end
##给所有target自定义编译配置
#post_install do |installer|
#    installer.pods_project.targets.each do |target|
#        target.build_configurations.each do |config|
#            config.build_settings['GCC_ENABLE_OBJC_GC'] = 'supported'
#        end
#    end
#end

