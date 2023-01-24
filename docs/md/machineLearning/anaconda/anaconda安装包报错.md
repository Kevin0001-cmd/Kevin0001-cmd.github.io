# 问题
在安装包时，出现如下错误
```
Collecting package metadata (repodata.json): failed

UnavailableInvalidChannel: The channel is not accessible or is invalid.
  channel name: simple
  channel url: http://pypi.douban.com/simple
  error code: 404

You will need to adjust your conda configuration to proceed.
Use `conda config --show channels` to view your configuration's current state,
and use `conda config --show-sources` to view config file locations.

```
错误原因是镜像源无法连接了。

# 解决
恢复默认镜像源
```
conda config --remove-key channels
```
修改镜像源
```
# 配置镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/

# 设置搜索时显示通道地址
conda config --set show_channel_urls yes
```
显示已经配置的源
```
conda config --show channels
```
# 国内的镜像源
 阿里云 http://mirrors.aliyun.com/pypi/simple/
 
 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
 
 豆瓣(douban) http://pypi.douban.com/simple/
 
 清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
 
 中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/