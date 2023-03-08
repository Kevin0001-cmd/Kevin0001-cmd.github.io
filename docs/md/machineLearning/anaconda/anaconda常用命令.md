打开Anaconda Prompt后（按照实际情况，看是否需要使用管理员身份打开），输入指令及响应
# conda

conda --version：查看conda版本

conda list：列出所有已经安装的库及其版本

conda list 库名：列出指定的库的信息

conda search 库名：查找库的信息

conda install 库名：安装某个库
> 如果已经安装了某个包，但是版本不对，需要安装新版本的包：conda install 库名=版本号
> 例如：conda install tensorflow=2.11.0

conda update 库名：同上

conda update --all：更新所有库

conda update conda：更新conda自身

conda update anaconda：更新anaconda自身

conda uninstall 库名：卸载某个库

# conda 创建/删除环境

## 列出所有环境

```bash
conda info -envs或者(-e)
```

## 创建并激活一个环境
使用”conda create”命令，后边跟上你希望用来称呼它的任何名字：

```bash
conda create --name snowflake python=3.6
```

这条命令将会给python3.6创建一个新的环境，位置在Anaconda安装文件的/envs/snowflakes

激活这个新环境
Linux，OS X:

```
source activate snowflakes
```
Windows：
```
activate snowflake
```

> tips：新的开发环境会被默认安装在你conda目录下的envs文件目录下。你可以指定一个其他的路径；可以通过
> `conda create -h`了解更多信息。

## 退出环境

如果要从你当前工作环境的路径切换到系统根目录时，键入：
Linux，OS X:

```
source deactivate
```
Windows:
```
deactivate
```

## 克隆环境

如果想迁移的是base环境，因此需要先克隆（base环境不能直打包）

```
conda create -n 新环境的名称 --clone 老环境名称
```

## 删除环境

```
conda env remove -n 环境名称
```



# conda clean

## 删除从不使用地包

```
$ conda clean --packages
```

## 删除tar包

```
$ conda clean --tarballs
```

## 删除索引缓存、锁定文件、未使用过的包和tar包

```
$ conda clean -a
```


# pip

pip install 库名：安装某个库
或
pip install tensorflow==2.0.0 -i https://pypi.tuna.tsinghua.edu.cn/simple：指定安装源

pip install 库名 --upgrade：更新某个库

pip install 库名\=\=version ：安装库的某个版本
> 可以通过`pip install 库名==`查看库的所有版本，然后再安装指定的版本

pip uninstall 库名：卸载某个库

