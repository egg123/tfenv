need glibc 2.17, but 2.12 in CentOS6

Download 2.17 from CentOS7
# curl -O http://ftp.riken.jp/Linux/centos/7/os/x86_64/Packages/glibc-2.17-222.el7.x86_64.rpm
# curl -O http://ftp.riken.jp/Linux/centos/7/os/x86_64/Packages/glibc-devel-2.17-222.el7.x86_64.rpm
# curl -O http://ftp.riken.jp/Linux/centos/7/os/x86_64/Packages/libstdc++-4.8.5-28.el7.x86_64.rpm
# curl -O http://ftp.riken.jp/Linux/centos/7/os/x86_64/Packages/libstdc++-devel-4.8.5-28.el7.x86_64.rpm

uncompress the above rpm

for example, 
glibc/glibc-devel to /opt/glibc6_2.17
libstdc++/libstdc++-devel to /opt/libstdc++_4.8.5

[root@localhost glibc6_2.17]# rpm2cpio glibc-2.17-222.el7.x86_64.rpm | cpio -id
[root@localhost glibc6_2.17]# rpm2cpio glibc-devel-2.17-222.el7.x86_64.rpm | cpio -id
[root@localhost libstdc++_4.8.5]# rpm2cpio libstdc++-devel-4.8.5-28.el7.x86_64.rpm | cpio -id
[root@localhost libstdc++_4.8.5]# rpm2cpio libstdc++-4.8.5-28.el7.x86_64.rpm | cpio -id

test
# /opt/glibc6_2.17/lib64/ld-2.17.so --library-path /opt/glibc6_2.17/lib64:/opt/libstdc++_4.8.5/usr/lib64 /root/.pyenv/versions/tf/bin/python

define as an alias command
alias tspy='/opt/glibc6_2.17/lib64/ld-2.17.so --library-path /opt/glibc6_2.17/lib64:/opt/libstdc++
_4.8.5/usr/lib64 /root/.pyenv/versions/tf/bin/python'
Python 2.7.14 (default, Nov  8 2018, 09:28:40)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-23)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>>
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess  = tf.Session()
2018-11-08 15:06:48.854860: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
>>> print(sess.run(hello))
Hello, TensorFlow!
>>>
>>> from keras.datasets import mnist
Using TensorFlow backend.
>>> mnist.load_data()
>>>
>>> exit()

# tspy

