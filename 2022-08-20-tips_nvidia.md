1. 禁止系统内核更新(uname.txt)

2. 在软件和更新的附加驱动里选择nvidia-driver-470(tested)

3. 在关机前运行sudo prime-select intel（切换集显，方便开机，如果忘了就需要进ubuntu高级选项、recovery、root）

4. 开机后运行
   
   - sudo prime-select nvidia（切换独显）
   - sudo modprobe nvidia（挂载独显驱动）
   - nvidia-smi（显示独显信息）
   
5. 安装CUDA
   - 	下载地址：https://developer.nvidia.com/cuda-toolkit-archive
   - 	安装时用空格取消安装驱动（因为已经安装过了）
   - 	查看版本：nvcc -V

6. 设置环境变量
   - 	export PATH=/usr/local/cuda/bin:\$PATH
   - 	export LD_LIBRARY_PATH=/usr/local/cuda/lib64:\$LD_LIBRARY_PATH

7. 安装cuDNN
   - 	下载地址：https://developer.nvidia.com/rdp/cudnn-archive
   - 	先后运行deb、dev.deb、samples.deb

8. 安装anaconda
   - 	https://repo.anaconda.com/archive/
   - 	(更新时用：conda update --all conda upgrade --all 这两条命令完全一致，没有区别)
   	打开：anaconda-navigator

9. 安装pytorch
   - 	conda create -n conda_pytorch
   - 	conda activate conda_pytorch
   - 	conda install pytorch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0
   - 	cudatoolkit=11.3 -c pytorch

	验证：在conda_pytorch环境下:
	
	```python
	import torch
	torch.__version__
	torch.version.cuda
	from torch.backends import cudnn
	cudnn.is_available()
	torch.backends.cudnn.version()
	```
	
	实测不提前装cuda和cudnn，只装pytorch上述指令的输出也正常（必须启用独显）
	
10. 安装terminator
    
    - sudo apt install terminator
    - Ctrl+Shift+T	打开终端
    - Ctrl+Shift+E	水平分割终端
    - Ctrl+Shift+O	垂直分割终端
    - Ctrl+Shift+W	关闭当前终端
    - Ctrl+Shift+Q	关闭所有终端