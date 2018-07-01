---
layout: post
title: ML persistence
date: 2018-07-01 06:31 +0000
---

# Scikit learning
* [en](http://scikit-learn.org/stable/modules/model_persistence.html)
* [cn](http://sklearn.apachecn.org/cn/stable/modules/model_persistence.html)
* [`pickle` Python object serialization](https://docs.python.org/2/library/pickle.html)
* [ref](https://blog.csdn.net/marsjhao/article/details/78712628)
* [image regnize](https://machinelearningmastery.com/save-load-machine-learning-models-python-scikit-learn/)

```python
import pickle
from sklearn import svm
from sklearn import datasets
from sklearn.externals import joblib

clf = svm.SVC()
iris = datasets.load_iris()
X, y = iris.data, iris.target
clf.fit(X, y)

s = pickle.dumps(clf)
clf2 = pickle.loads(s)
clf2.predict(X[0:1])

joblib.dump(clf, 'joblib.pickle.pkl')
```

# Tensorflow
* [model persistence](https://blog.csdn.net/michael_yt/article/details/74737489)

## CKPT
* [example of sl](https://blog.csdn.net/marsjhao/article/details/72829635)

```python
import tensorflow as tf
import shutil
import os.path

MODEL_DIR = "model/ckpt"
MODEL_NAME = "model.ckpt"

# if os.path.exists(MODEL_DIR): 删除目录
#     shutil.rmtree(MODEL_DIR)
if not tf.gfile.Exists(MODEL_DIR): #创建目录
    tf.gfile.MakeDirs(MODEL_DIR)

#下面的过程你可以替换成CNN、RNN等你想做的训练过程，这里只是简单的一个计算公式
input_holder = tf.placeholder(tf.float32, shape=[1], name="input_holder") #输入占位符，并指定名字，后续模型读取可能会用的
W1 = tf.Variable(tf.constant(5.0, shape=[1]), name="W1")
B1 = tf.Variable(tf.constant(1.0, shape=[1]), name="B1")
_y = (input_holder * W1) + B1
predictions = tf.greater(_y, 50, name="predictions") #输出节点名字，后续模型读取会用到，比50大返回true，否则返回false

init = tf.global_variables_initializer()
saver = tf.train.Saver() #声明saver用于保存模型

with tf.Session() as sess:
    sess.run(init)
    print("predictions : ", sess.run(predictions, feed_dict={input_holder: [10.0]}))  # 输入一个数据测试一下
    saver.save(sess, os.path.join(MODEL_DIR, MODEL_NAME)) #模型保存
    print("%d ops in the final graph." % len(tf.get_default_graph().as_graph_def().node)) #得到当前图有几个操作节点

for op in tf.get_default_graph().get_operations(): #打印模型节点信息
    print (op.name, op.values())
```
## PB
* [example](https://zhuanlan.zhihu.com/p/32887066)
* [example](http://ai.51cto.com/art/201710/554450.htm)

```python
# coding=UTF-8
import tensorflow as tf
import shutil
import os.path
from tensorflow.python.framework import graph_util


MODEL_DIR = "model/pb"
MODEL_NAME = "addmodel.pb"

# if os.path.exists(MODEL_DIR): 删除目录
#     shutil.rmtree(MODEL_DIR)
#
if not tf.gfile.Exists(MODEL_DIR): #创建目录
    tf.gfile.MakeDirs(MODEL_DIR)

output_graph = "model/pb/add_model.pb"

#下面的过程你可以替换成CNN、RNN等你想做的训练过程，这里只是简单的一个计算公式
input_holder = tf.placeholder(tf.float32, shape=[1], name="input_holder")
W1 = tf.Variable(tf.constant(5.0, shape=[1]), name="W1")
B1 = tf.Variable(tf.constant(1.0, shape=[1]), name="B1")
_y = (input_holder * W1) + B1
# predictions = tf.greater(_y, 50, name="predictions") #比50大返回true，否则返回false
predictions = tf.add(_y, 10,name="predictions") #做一个加法运算

init = tf.global_variables_initializer()

with tf.Session() as sess:
    sess.run(init)
    print("predictions : ", sess.run(predictions, feed_dict={input_holder: [10.0]}))
    graph_def = tf.get_default_graph().as_graph_def() #得到当前的图的 GraphDef 部分，通过这个部分就可以完成重输入层到输出层的计算过程

    output_graph_def = graph_util.convert_variables_to_constants(  # 模型持久化，将变量值固定
        sess,
        graph_def,
        ["predictions"] #需要保存节点的名字
    )
    with tf.gfile.GFile(output_graph, "wb") as f:  # 保存模型
        f.write(output_graph_def.SerializeToString())  # 序列化输出
    print("%d ops in the final graph." % len(output_graph_def.node))
    print (predictions)

for op in tf.get_default_graph().get_operations(): #打印模型节点信息
    print (op.name)
```

# Spark
* [introduction DataFrame](https://blog.csdn.net/github_39261590/article/details/77600491)
* [spark dataframe](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* [spark MLlib](https://spark.apache.org/docs/latest/ml-guide.html)
* [pandas dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)
