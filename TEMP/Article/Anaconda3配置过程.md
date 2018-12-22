# DeepLabCut安装篇（一）：环境配置

**使用Anaconda3容器环境进行使用**

Anaconda3我所使用的版本自带的是Python3.7，但是发现Python3.7在接下来安装wxPyhton的时候提示

```
wxPython-4.0.3-cp36-cp36m-linux_x86_64.whl is not a supported wheel on this platform.
```

不支持这个平台，于是放弃。

# 创建容器环境

```shell
conda create -n houiin-deeplabcut-py36 python=3.6
```

其中`houiin-deeplabcut-py36`是我对这个容器的命名

```
$ conda create -n houiin-deeplabcut-py36 python=3.6
Solving environment: done

==> WARNING: A newer version of conda exists. <==
  current version: 4.5.11
  latest version: 4.5.12

Please update conda by running

    $ conda update -n base -c defaults conda

## Package Plan ##

  environment location: /home/houiin/.conda/envs/houiin-deeplabcut-py36

  added / updated specs: 
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    python-3.6.7               |       h0371630_0        34.3 MB

The following NEW packages will be INSTALLED:

    ca-certificates: 2018.03.07-0           
    certifi:         2018.11.29-py36_0      
    libedit:         3.1.20170329-h6b74fdf_2
    libffi:          3.2.1-hd88cf55_4       
    libgcc-ng:       8.2.0-hdf63c60_1       
    libstdcxx-ng:    8.2.0-hdf63c60_1       
    ncurses:         6.1-he6710b0_1         
    openssl:         1.1.1a-h7b6447c_0      
    pip:             18.1-py36_0            
    python:          3.6.7-h0371630_0       
    readline:        7.0-h7b6447c_5         
    setuptools:      40.6.3-py36_0          
    sqlite:          3.26.0-h7b6447c_0      
    tk:              8.6.8-hbc83047_0       
    wheel:           0.32.3-py36_0          
    xz:              5.2.4-h14c3975_4       
    zlib:            1.2.11-h7b6447c_3      

Proceed ([y]/n)? 
```

**输入y自动配置环境**

国内网络环境比较尴尬，需要话费很长时间进行下载。

基本环境配置完成

![](https://raw.githubusercontent.com/Houiin/houiin-pic1/master/Pic/csdn/blog20181221134117.png)

激活这个环境

```
conda activate houiin-deeplabcut-py36

conda activate deeplabcut-py37
```

![](https://raw.githubusercontent.com/Houiin/houiin-pic1/master/Pic/csdn/blog20181221134347.png)

可以看到用户名之前已经 标出了这个环境的名字，如果创建错的话可以直接`conda remove 环境名字` 对其移除



如果需要退出这个环境则可以使用 `conda deactivate`

# 安装deeplabcut

```
pip install deeplabcut 
```

 ![](https://raw.githubusercontent.com/Houiin/houiin-pic1/master/Pic/csdn/blog20181221134627.png)

### 安装wxPython

```
pip install https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04/wxPython-4.0.3-cp36-cp36m-linux_x86_64.whl
```

但是直接下载的网速很慢。。。推荐先用Aria2等其他多线程下载工具下载完成后本地安装

# 安装TensorFlow

**TensorFlow官网需要使用科学的办法才能访问，自己想办法**

CPU ONLY:

```
pip install --ignore-installed tensorflow==1.10
```

GPU:（tensorflow官方的命令）

```
pip install tensorflow-gpu //这一条我安装失败了
```

> 目前GPU最新的版本是1.12
>
> 执行这个命令下载的文件是https://files.pythonhosted.org/packages/55/7e/bec4d62e9dc95e828922c6cec38acd9461af8abe749f7c9def25ec4b2fdb/tensorflow_gpu-1.12.0-cp36-cp36m-manylinux1_x86_64.whl
>
> *网络不好的朋友可以先下载再本地安装——比如我自己orz....*

`错误提示：Could not find a version that satisfies the requirement grpcio>=1.8.6 (from tensorflow-gpu) (from versions: )
No matching distribution found for grpcio>=1.8.6 (from tensorflow-gpu)`

**DeepLabCut实例使用的是1.8**

```
pip install tensorflow-gpu==1.8 //执行成功，我最终还是屈服在了官方脚下，不知道为啥1.12版本报 //执行成功，我最终还是屈服在了官方脚下，不知道为啥1.12版本报错
```

**当然，这一切都在Anaconda的容器环境中**

# 验证TensorFlow是否安装成功

启动ipython

```
ipython

import tensorflow as tf
```

![无法载入TF运行库](https://raw.githubusercontent.com/Houiin/houiin-pic1/master/Pic/csdn/blog20181221142525.png)

比较尴尬的是....无法导入TensorFlow的模块，不过可以肯定的是TensorFlow一定已经存在于anaconda环境中，因为退出环境后新开一个终端直接提示 *找不到模块* 

![](https://raw.githubusercontent.com/Houiin/houiin-pic1/master/Pic/csdn/blog20181221142850.png)



我认输。。。。。。。。

# TensorFlow错误解决办法-结果装了CUDNN还是报错

参考链接：https://stackoverflow.com/questions/43942185/failed-to-load-the-native-tensorflow-runtime-python-3-5-2



### 1. 下载CuDNN

选择和自己CUDA版本匹配的

![](https://ws1.sinaimg.cn/large/dfb8453aly1fyfk3qjgakj212u0er0v4.jpg)

![](https://ws1.sinaimg.cn/large/dfb8453aly1fyfk5nrp8bj20yv09hgmw.jpg)
