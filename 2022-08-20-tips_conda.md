conda换源

1. 生成配置文件

   ​	conda config --set show_channel_urls yes

2. gedit ~/.condarc

   ​	内容如下：

   channels:

     \- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

     \- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

     \- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

     \- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/

   ssl_verify: true