---
layout: post
title: Ruby Trollop
date:   2014-05-10 
categories: Ruby Trollop
---

###### _This blog was copied from internet._

[Trollop](https://github.com/wjessop/trollop)
命令行参数的解析器(command line options parser)。其实Ruby自带的库里面就有像[OptionParser](http://ruby-doc.org/stdlib-2.1.2/libdoc/optparse/rdoc/OptionParser.html)这样具有类似功能的库，那我们为什么还要使用Trollop呢？我认为Trollop最大的好处就是简单好用。

介绍Trollop, _For Rubygems.org_

>Trollop is a commandline option parser for Ruby that just gets out of your way. One line of code per option is all you need to write. For that, you get a nice automatically-generated help page, robust option parsing, command subcompletion, and sensible defaults for everything you don't specify.

运行`gem install trollop`安装

然后现在假设一个场景。我们要写一个脚本，这个脚本需要能够在不同的环境下运行，假如是production/staging。所以我们在运行它的时候就希望可以带不同的环境选项(options)。如下一个程序就可以完成这个任务。

{% highlight ruby %}
opts = Trollop::options do
  opt :environment, "the environment to run the script against.", :type => :string
end
{% endhighlight %}

`require "trollop"`是为了包含这个库。下面最重要的一行是在代码块（block）中的:

	opt :environment, "the environment to run the script against.", :type => :string
	
这个代码块就会生成一个名叫opts的Hash，而`:environment`就是其中的key。在程序中要使用这个environment变量该怎么用呢？直接用`opts[:environment]`就可以了。以上这一行中间的String(废话)是对这个选项的描述，最后的`:type`是声明这个值的类型，也就是`opts[:environment]`的类型为String。所以下面这一行：

	puts "Running the script against environment: #{opts[:environment]}."
	
就打印出来了我们从命令行中传入的`environment`值。假如说我保存这个脚本为`test.rb`。那么我们只要就可以运行`ruby test.rb --environment production`。这样就会打印出`Running the script against environment: production.`如何知道都有哪些选项呢？运行一下`ruby test.rb --help`就可以看到如下内容：

	Options:
	  --environment, -e <s>:   the environment to run the script against.
	             --help, -h:   Show this message
             	
这些是Trollop为我们自动生成了，同时我们可以看到，对于我们的environment option, 不经可以用long option:`--environment`，还可以用short option:`-e`。对于help也同样可以用`--help`或者是`-h`。而且这个帮助也是Trollop自动生成的，完全不需要我们做额外的工作。

现在假设我们需要run一个benchmark,需要加一个运行次数的选项。那么我们只需要在程序块中加一行：

	opt :number, "running for this number of times", :type => :int
	
这样我们的帮助就变成了:

	Options:
	  --environment, -e <s>:   the environment to run the script against.
           --number, -n <i>:   running for this number of times
                 --help, -h:   Show this message
           	 
然后我们就可以运行`ruby test.rb -e staging -n 7`传入环境变量staging跟运行次数7了。

细心的读者可能发现，自动生成的short format往往就是long format的第一个字母。没错！那这样的话如果第一个字母相同怎么办呢？作者已经为我们设计好了算法来解决这种冲突。只要查看`--help`就可以看到每个选项的正确名称。而且如果我们不喜欢自动生成了选项名或者是帮助信息的话也可以自己来配置。总而言之，Trollop已经很贴心的帮我们做好了一切，但同时也给我们自己去customize的自由。