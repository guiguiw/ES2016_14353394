# DOL实例分析&编程 #
## 实验任务 ##
- 修改dol文件中的example2,让3个square模块变为2个。
- 修改dol文件中的example1，使其输出3次方数。  

##实验注意事项##
- 修改代码后要重新编译，首先进入dol目录下：`cd dol`
- 进行编译：`ant -f build_zip.xml all`
- 编译成功后显示如图所示：  
 
     ![result](http://i1.piimg.com/4851/2751ae8db2071d40.png)  

##实验步骤##
###对example1的源代码分析###
在example1中定义了一个平方进程，具体代码如下：
  
    if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
首先是对判断条件的分析，p->local->index是指当前的位置，该值被初始化为0；__p->local->len__为生产者的长度，若满足当前位置小于生产者的长度，则对变量i进行平方运算。
###修改example1源代码###
实验要求输出位i的三次方，所以我们只需要在__i__平方的基础上再乘以i即可，修改代码如下:  
`i=i*i*i`
###进行编译并运行修改后的代码###
- 这里需要注意一点，在运行修改后的代码前，首先需要删除main文件夹下的已存在的example文件，该文件的具体目录为`dol/build/bin/main`；  
- 删除后进行编译，编译指令已在实验注意事项中说明；  
- 运行修改后的代码，需要先进入文件所在目录，指令为`cd dol/build/bin/main`  
运行example1,指令为`sudo ant -f runexample.xml -Dnumber=1`
###成功截图    
![result1](http://i1.piimg.com/4851/28924ea139be63d6.png)  
从上图结果可以看到，生产者长度为20，输出了0-19每个数的三次方。  
  
接下来分析并实现example2。

###对example2的源代码分析###
    <variable value="3" name="N"/>  
以上源代码中定义了三个square模块，对于各个模块之间的连接已在课堂讲过，在此不赘述。
###修改example2的源代码###
实验只需要输出2个square模块，所以只需要把value的值改为2即可。  
`variable value="2" name="N"/` 
###运行修改后的代码###
运行指令为：`sudo ant -f runexample.xml -Dnumber=2`
###成功截图###
- 在运行成功后，我们可以在`dol/build/bin/main/example2`的文件夹下，看到`example2.dot`文件。  
- 如果你的Ubuntu未安装打开dot文件的软件，双击该文件后会有对话框提示你安装类似软件，这里我安装了Xdot，安装指令为  
    `sudo apt-get install xdot`
- 安装成功后，我们就可以双击打__dot__文件了！
- 最后截图为：  
![result3](http://p1.bpimg.com/4851/4ae62db66ff378af.png)  
  

##实验感想##
此次实验比较简单，且实验课TA也详细分析了每个example中的源代码及其实现功能，实验做起来还是很快的，唯一遇到的问题就是在运行example1的时候没有先删除之前已经存在的example文件，该文件是在进行Lab1的时候为了测试配置环境是否成功而留下的文件，若不删除则会有Build Failed的提示，删除后就可以完美运行了。 