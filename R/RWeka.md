# 安装Weka
在R语言中使用RWeka需要事先安装好Weka软件  
并同时将Weka软件相关的jar包(如:weka.jar)添加到CLASSPATH  

weka介绍与安装: http://blog.csdn.net/lengwuqin/article/details/38665541  
Weka官网下载地址: http://www.cs.waikato.ac.nz/ml/weka/downloading.html  


# 安装R语言的RWeka包
RWeka包依赖rJava和Weka, 而rJava包需要Java运行环境, 所以一般操作步奏如下:
1. 安装好Java环境, 并设置好JAVA_HOME, ClASS_PATH等环境变量
2. 安装好Weka软件, 并把其包含的Weka.jar等jar包路径添加进CLASSPATH
3. 安装rJava包
4. 安装RWeka包

下面你就可以使用RWeka包愉快的进行玩耍了^_^