# Google Colaboratory中如何查看是否使用了GPU？
```
import tensorflow as tf
# 获取当前主机上某种特定运算设备类型（如GPU或CPU）的列表
print(tf.config.list_physical_devices('GPU'))

import torch
# 返回GPU名字，设备索引默认从0开始
print(torch.cuda.get_device_name(0))
# cuda是否可用
print(torch.cuda.is_available())
# 返回当前设备的索引
print(torch.cuda.current_device())
# 返回GPU的数量
print(torch.cuda.device_count())
```



# Google Col中的%和！

在Google Colab中

* 当使用!时，它将直接在子shell中执行bash命令
* 当使用%时，它将执行IPython中定义的魔术命令之一

两者相似，但实现细节不同。

魔术命令是IPython的特殊命令，这些命令以百分号开头，通过%quickref或%magic命令可以查看所有的命令。

