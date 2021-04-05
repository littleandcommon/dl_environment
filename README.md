# dl_environment
深度学习的环境配置的过程
学习jupter (很多地方都提到过)使用Docker配置管理环境似乎更加清晰
安装cuda cudnn 查看显卡配置等
先查看下硬盘的挂载情况再自行选择安装目录，查看挂载情况的语句是df -h
打开文件的常用操作：
打开profile文件：

vi /etc/profile
在文件最后加入如下语句（路径需要根据自己的安装位置更改）：

PATH=$PATH:/opt/anaconda3/bin
export PATH
按住shift键+:键，输入wq，保存文件并退出。最后使用如下命令刷新环境变量即可：

source /etc/profile
echo $PATH

anconda虚拟环境命令
Anaconda创建环境：

conda create -n py37(环境名) python=3.7(指定的python版本)[注意这里使用的如果是conda create--name的话会报错不知道原因]

删除环境（不要乱删）：

conda remove -n py37 --all

进入环境：

conda activate py37

退出环境：

conda deactivate
一个服务器上各个用户可以安装不同的cuda和cudnn，
注意cuda和cudnn的版本需要对应，但不是一一对应，主要是看tensorflow的版本需要的python和cuda和cudnn的版本 自己使用和服务器上的成员共同使用可以分别使用添加进系统变量和用户环境变量
添加清华源，增加下载速度：
直接在激活的虚拟环境中添加
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --set show_channel_urls yes
linux操作系统上的下载安装指令：使用wget+下载链接地址
安装tensorflow:conda install tensorflow-gpu==（版本号）
价差自己是否安装成功
import torch  # 导入安装的pytorch包
torch.cuda.is_available()  # 检查cuda是否可以使用
添加完了清华源之后出现了一些问题，所以解决方案是重新安装一个虚拟环境 或者将清华源删除了
常见的linux操作系统的常用知识
bin 存放二进制可执行文件(ls,cat,mkdir等)
boot 存放用于系统引导时使用的各种文件
dev 用于存放设备文件
etc 存放系统配置文件
home 存放所有用户文件的根目录
lib 存放跟文件系统中的程序运行所需要的共享库及内核模块
mnt 系统管理员安装临时文件系统的安装点
opt 额外安装的可选应用程序包所放置的位置
proc 虚拟文件系统，存放当前内存的映射
root 超级用户目录
sbin 存放二进制可执行文件，只有root才能访问
tmp 用于存放各种临时文件
usr 用于存放系统应用程序，比较重要的目录/usr/local 本地管理员软件安装目录
var 用于存放运行时需要改变数据的文件
使用xshell来操作服务非常方便，传文件也比较方便。
就是使用rz，sz
首先，服务器要安装了rz，sz
yum install lrzsz
当然你的本地windows主机也通过ssh连接了linux服务器
运行rz，会将windows的文件传到linux服务器
运行sz filename，会将文件下载到windows本地
文件权限的问题：使用chmod u+x 文件名
文件运行一般是 python 文件名或者./文件名
目录的一些操作 cd ~直接回用户主目录 cd ..返回上一级
（9）目录操作时，“.” 表示 当前目录 ；
（10）目录操作时，“..” 表示 上一级目录 ；
（11）目录操作时，“-” 表示 上一次工作目录 ；
（12）目录操作时，“~” 表示 用户主目录 ；
文件操作
ls：显示文件或目录信息
mkdir：当前目录下创建一个空目录
rmdir：要求目录为空
touch：生成一个空文件或更改文件的时间
cp：复制文件或目录
mv：移动文件或目录、文件或目录改名
rm：删除文件或目录
ln：建立链接文件
find：查找文件
file/stat：查看文件类型或文件属性信息
cat：查看文本文件内容
more：可以分页看
less：不仅可以分页，还可以方便地搜索，回翻等操作
tail -10： 查看文件的尾部的10行
head -20：查看文件的头部20行
echo：把内容重定向到指定的文件中 ，有则打开，无则创建
管道命令 | ：将前面的结果给后面的命令，例如：ls -la | wc，将ls的结果加油wc命令来统计字数
重定向 > 是覆盖模式，>> 是追加模式，例如：echo "Java3y,zhen de hen xihuan ni" > qingshu.txt把左边的输出放到右边的文件里去
文件编辑

添加源的语句conda install -c conda-forge <package>


关于deepfashion的项目，数据集和预训练模型的位置需要放置正确，作者的数据集使用了一些预训练解析模型生成的 
生成一些测试标签：使用已经开源的模型：https://github.com/levindabhi/Self-Correction-Human-Parsing-for-ACGPN
两个项目：https://github.com/minar09/ACGPN
放在服务器上跟在window一样先是出现了没有tensorboard和cv2模块直接在虚拟环境中pip安装（项目运行要在配置好的虚拟环境下）
bug1：出现了list和int类型不匹配的问题，原因是torchvision版本不匹配的问题重新下载更新了
bug2:出现__new__() got an unexpected keyword argument 'serialized_options'问题，这个问题有人说直接将protobuf更新一下（使用语句pip install -u protobuf）不过也有人说3.5的版本出现问题换成3。4反而好了，我将其从3.15换成3.6的版本这个bug消失了，注意anaconda中安装了tensorflow和pytorch会出现两个protobuf，一个是libprotobuf另一个是protobuf
bug3:pytorch中缺少模块，直接更新pytorch




