# 源代码概览


##  目录构概览

```
.ci          持续继承工具目录
.github      github一些说明文档
benchmarks   基于JMH的基准压测
buildSrc     构建elasticsearch的相关插件代码
client       elasticsearch客户端代码
dev-tools	 几个开发工具脚本
distribution elasticsearch的打包发行相关，将elasticsearch打成各种发行包（zip，deb，rpm，tar）的模块。具体用法如是，在相应的发行版本模块下执行publishToMavenLocal这个Task，如果执行成功的话就会在路径build/distributions下生成对应的发行包，这种打好的包就能在生产服务器上运行。
docs	     文档目录
gradle       gradlew用到的，jar包
libs         一些依赖包
licenses	
modules	     作为elasticsearch除核心外的必备模块相关代码
plugins      作为elasticsearch必备的插件的相关代码，
server       elasticsearch服务端代码
x-pack	     x-pack的源代码
```