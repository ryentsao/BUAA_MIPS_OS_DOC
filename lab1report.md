						                                                       	Lab1实验报告
Part1
Think2.1
·如果小明之前用git add将printf.c提交到了暂存区，用git checkout printf.c指令就可以把该文件重新恢复到工作区。
·小明可以用git reset HEAD printf.c，然后在用git checkout printf.c两条指令将该文件恢复到工作区。
·用git rm --cached Tucao.txt指令就可以取消对Tucao.txt文件的跟踪，即将它从暂存区中删除，但不从工作区删除。
Think2.2
1、	这句话是正确的，clone会将远程仓库里的所有分支都克隆下来，但是只有HEAD指向的分支（master）才会被检出，
其余的分支需要用户自己手动checkout来把远程分支取到本地。资料参考自http://blog.csdn.net/xqs83/article/details/7382074。
同时，通过第一次实验课的git clone也可以看出来，clone之后所有的分支都被克隆下来了，但只有lab1分支才在本地检出。
2、	这个说法正确。
首先来了解这四个指令的作用，git log的作用是查看最近提交修改的历史记录，按照时间排序。git status的作用是查看当前目录下
所有还没有被git管理的文件和被git管理且被修改但还未提交(git commit)的文件。git checkout的作用主要是更改HEAD指针指向和重
写工作区。git commit的作用是将改变之后的索引内容添加记录到仓库中去。可以看到，这些指令都是在本地工作区和本地仓库中完成的，
而且clone之后，按照http://web.mit.edu/~mkgray/project/silk/root/afs/sipb/project/git/git-doc/git-clone.html 中的说法：
Clone a repository into a new director。是将远程仓库克隆到本地的一个目录下，即本地已经有了远程仓库的所有内容，因此此时
的上述操作都可以在本地完成，不需要再访问远程仓库。

3、这个说法错误，与第一个说法矛盾。
4、这个说法是正确的，在git clone 时，如果用到git clone –b <name>指令，则会检出<name>分支并将当前HEAD指针指向 <name> 分支，
但如果不使用-b的话，检出的是默认的HEAD指向的分支，即master分支，并且HEAD指针指向该分支。参考自
http://web.mit.edu/~mkgray/project/silk/root/afs/sipb/project/git/git-doc/git-clone.html
-b <name>
Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository’s HEAD, point to <name> branch
instead. In a non-bare repository, this is the branch that will be checked out. --branch can also take tags and detaches the 
HEAD at that commit in the resulting repository.


Part2
本次试验总共有五个部分：修改include.mk（使得Makefile文件中的交叉编译器的路径正确），修改scse0_3.lds（将内核调整到正确的位置上，
通过mmu.h可以看到，本次实验内核应该被调整到0x80010000），修改start.S（将sp寄存器设置为内核栈空间所在的位置，即0x80400000），补
全print.c中的lp_Print()函数（实现字符输出），最后一部分是git的学习和使用。
在整个实验中，我感觉最难的部分是补全lp_Print()函数，因为写这个函数的过程中，会调用很多其它的函数，这些函数都包含在其他文件中，
要补全lp_Print()函数，必须首先弄懂调用的函数的功能。比如其中有一个OUTPUT(void*,char* s, int l),这个函数实现的功能是输出字符串s的前l位。
为了弄清lp_Print()这个过程，我画了一个简易的流程图，以便理解。 


Part3
正如学长所说，操作系统实验的入门难度比oo高多了，虽然磕磕绊绊地用两周时间完成了lab1的所有实验，也大概了解到了内核是如何启动的，
但是对操作系统还是没有一个特别形象的认识，可能是学习还不够到位。
到目前为止，虽然只是完成了较为简单的实验一，但对于一个之前没有接触过操作系统的小白来说，学习到的东西已经非常多了。此外当遇到困
难的时候，通过在网上查资料也可以学到很多关联的知识，受益匪浅。都说篮球相较足球来说更难入门，一旦学会了打篮球，就非常容易变成高
手，而足球的门槛非常低，但踢得好的并不多。操作系统也是这样吧，虽然门槛高，但如果能跨过这个门槛，今后的学习会轻松很多吧。

Part4
在刚刚接触到exercise的时候，我完全是脑中一片空白，无从下手，我认为如果在指导书中可以有一点引导会更好。

Part5
在修改scse0_3.lds时，只设置了.data, .bss., 和.text三部分内容，但是通过查看ELF文件，还有很多其他的内容，都没有设置，难道启动内
核都不会用到吗？设置之后会有什么不同？
