# tf.GradientTape()
作用：可以监视变量的变化，主要用于求导
> 是tf.gradients的替代



# 用法

```python
initializer = tf.keras.initializers.GlorotNormal()
w1 = tf.Variable(name='w1', initial_value=initializer(shape=[3]))
w2 = tf.Variable(name='w2', initial_value=initializer(shape=[3]))
w3 = tf.Variable(name='w3', initial_value=initializer(shape=[3]))
w4 = tf.Variable(name='w4', initial_value=initializer(shape=[3]))
with tf.GradientTape() as g:
    # g.watch(w1)
    # g.watch(w2)
    # g.watch(w3)
    # g.watch(w4)
    z1 = 3 * w1 + 2 * w2 + w3
    z2 = w1 + -1 * w3 + w4
	grads = g.gradient([z1, z2], [w1, w2, w3, w4])
print(type(grads))
print(len(grads))
print(grads)

#输出结果
<class 'list'>
4
[<tf.Tensor: shape=(3,), dtype=float32, numpy=array([4., 4., 4.], dtype=float32)>, <tf.Tensor: shape=(3,), dtype=float32, numpy=array([2., 2., 2.], dtype=float32)>, <tf.Tensor: shape=(3,), dtype=float32, numpy=array([0., 0., 0.], dtype=float32)>, <tf.Tensor: shape=(3,), dtype=float32, numpy=array([1., 1., 1.], dtype=float32)>]
```

注意：变量的初始化可以写在with语句之前，但要计算导数的公式（z1,z2）必须在with语句之内。

`g.gradient([z1, z2], [w1, w2, w3, w4])`表示求对于`[w1,w2,w3,w4]`的`[z1,z2]`的导数。求出结果的len与`[w1,w2,w3,w4]`相同，为4。grads其中一个元素的len和w的len相同，比如[4., 4., 4.]的长度为3，是因为w1的长度为3.

求出的导数是一个list，包含了len([w1, w2, w3, w4])个元素，即4个元素。

具体的求导方式：

上面的例子中，第一个求导结果`[4., 4., 4.]`，是dz1/w1+dz2/w1=3+1=4。也就是说，求得是z1和z2对w1的导数之和。其他的依此类推。



# 参数

## persistent

含义：默认值为`False`，表示此时创建的`tape`不是持久化的，只能调用一次`gradient`。如果值为`True`，则可以多次调用`gradient`。但是最后要del tape。

```python
x = tf.Variable(3.)
with tf.GradientTape(persistent=True) as tape:
    tape.watch(x)
    y = tf.pow(x, 4)        # y = x^4
    z = tf.multiply(x, 3)   # z = 3*x
    dy_dx = tape.gradient(y, x)
    dz_dx = tape.gradient(z, x)
    print(dy_dx)
    print(dz_dx)
del tape
```



# 方法

## stop_recording

作用：加上这一句后，执行的操作不会被tape记录，有利于减少追踪计算所使用的内存。

```python
 with tf.GradientTape(persistent=True) as t:
        loss = compute_loss(model)
        with t.stop_recording():
          # The gradient computation below is not traced, saving memory.
          grads = t.gradient(loss, model.variables)
```



# 拓展

## 二阶梯度计算

```python
x = tf.Variable(1.)
with tf.GradientTape() as tape1:
    tape1.watch(x)
    with tf.GradientTape() as tape2:
        tape2.watch(x)
        y = tf.pow(x, 4)
        dy_dx = tape2.gradient(y, x) # y' = 4x^3
        print(dy_dx)
    dy2_dx2 = tape1.gradient(dy_dx, x) # y'' = 12x^2
    print(dy2_dx2)
del tape1,tape2
```

还可以写三阶，四阶，n阶梯度计算。
