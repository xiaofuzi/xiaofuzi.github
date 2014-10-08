#00.重构rails？
##为什么要重构rails？
对软件的底层细节有足够的理解，这样你才能够掌控它。这种特殊的能力是你无法伪造的。在搭建rails框架的过程中会让你对它有足够的了解。如果你确实这样做了，这不是很有价值吗？
在这里，将会教你重零开始使用ruby建立一个Rails-like web框架。通过本书的学习，可以让你对rails有更深入的理解，同时也可以帮助你建立自己的框架。
##什么样的人适合阅读本书？
首先你需要会使用Ruby。如果你已经编写过一些ruby app或者是rails app的话，那么本书会适合你阅读。

#0.5 环境搭建
你需要安装以下的软件：（本书编写时，rails还处于rails3）

* Ruby 1.9
* 一个编辑器
* 命令行工具
* git
* Bundler
* SQLite,在最后的章节才会用到。

#01从零开始
搭建好环境后，我们就可以开始创建我们的框架了，就像rails一样，我们会将我们的框架以gem包的形式搭建以便于可以被其它程序引用。在这本书中，我们将我们的框架称为“ Ruby on Rulers”.

####首先，创建一个空的gem:
> $bundle gem rulers
      create  rulers/Gemfile
      create  rulers/Rakefile
      create  rulers/LICENSE.txt
      create  rulers/README.md
      create  rulers/.gitignore
      create  rulers/rulers.gemspec
      create  rulers/lib/rulers.rb
      create  rulers/lib/rulers/version.rb

可以看到，bundle命令会给创建一个gem的骨架结构。

在rulers.gemspec中会声明Rulers的依赖包，同时还有其它的ruler属性信息，使用编辑器编辑添加你自己的信息进去就可以。

在这里我们需要给rulers添加一个依赖包rack。
通过命令： gem.add_runtime_dependency "rack"

Rack是一个与服务器交互的接口，通过rack，我们的框架就可以和Mongrel,Thin,Passenger,Webrick等交互。Rack负责处理http协议所做的工作，这使我们不用具体去关心如何发送一个Http request以及如何接收一个Http response。

####创建gem然后安装它：

    >gem build rulers.gemspec
    >gem install rulers-0.0.1.gem


##Hello World，一个简单的rails-like app
在这里，我们将手动的建立一个简单的rails-like app在我们的ruler之上如同（" rails new best_quotes"）做的功能一样。

创建一个名为best_quotes的目录（最好目录结构为 src/best_quotes,src与rulerlib同级）

     mkdir best_quotes
     cd best_quotes
     git init

然后创建两个文件夹，config,app:

     mkdir config
     mkdir app

将我们的rulergem添加到best_quotes 的 Gemfile中

     #best_quotes/Gemfile
     source :rubygems
     gem 'rulers'  #your gem name

然后运行" bundle install"命令以确保所有的依赖都以可以使用，该命令会创建一个名为Gemfile.lock的文件。

我们将会从一个简单的rack app开始编写我们的 ruler app。创建一个 config.ru文件，在文件中添加如下代码；

     #best_quotes/config.ru
     run proc {
     	[200, {'Content-Type' => 'text/html'},["Hello, world!"]]]
     }

rack "run" 表示响应每一个http request请求。在这里，proc返回一个http包，包括（200）和（“Hello， world！”），浏览器将根据这些内容来显示网页。
现在你可以通过运行 “ rackup -p 3001”,然后在浏览器中输入“http://localhost:3001”打开网页，你就会看到config.ru中的“ Hello world!”字符串了.

##在Ruler中使用Rack
在ruler的 lib/rulers.rb中，将内容更改为如下所示：

    # rulers/lib/rulers.rb
	require "rulers/version"
	module Rulers
                 class Application
                      def call(env)
     	             [200, {'Content-Type' => 'text/html'},
      	             ["Hello from Ruby on Rulers!"]]
                      end
                 end
	end

然后重新创建给gem并重新安装它。
做完以上工作后，回到best_quotes目录。现在你就可以使用Rulers::Application class了。在config目录下新建一个名为appliction.rb的文件，然后添加如下内容：

     #best_quotes/config/appliction.rb
     require "rulers"

     module BestQuotes
           class Appliction < Rulers::Appliction
           end
      end

通过以上的操作，"BestQuotes"application对象就可以使用Rulers 框架并输出“Hello from Ruby on rulers当我们使用它的时候。为了使用它，我们还需要在config.ru变更为如下：

     #best_quotes/config.ru
     require './config/appliction'
     run BestQuotes::Application.new

现在就可以上前面同样的方式查看了：

>"rackup -p 3001"
>"http://localhost:3001"