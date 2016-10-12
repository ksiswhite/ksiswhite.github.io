---
layout: post
title: "Python:文件遍历与MD5提取"
date:   2016-10-9
excerpt: "python实现遍历目录并提取文件MD5"
tag:
- Python
---
<h2>文件遍历</h2>

<p>　　使用os.work()实现，该函数原型为:os.walk<br>
(top.topdown=True,onerror=None,followlinks=False)。<br>
　　其中，top.topdown指明遍历顺序，onerror的参数应为一个function或者为空，用于异常处理。work()函数的followlinks控制函数是否会进入符号链接，该参数默认为False，所以walk()默认不会进入符号目录。<br>
　　该函数返回值为一个三元组(dirpath, dirnames, filenames)，通过循环即可完成对目录内所有文件的遍历。<br><br>
demo：  </p>

<blockquote>
<p>import os<br>
s = os.sep<br>
root = "d:" + s + "ll" + s<br>
for rt, dirs, files in os.walk(root):<br>
　　for f in files:<br>
　　　　fname = os.path.splitext(f)<br>
　　　　new = fname[0] + 'b' + fname[1]<br>
　　　　os.rename(os.path.join(rt,f),os.path.join(rt,new))</p>
</blockquote>

<p>　　os.walk文档:<a href="https://docs.python.org/2/library/os.html?highlight=os.walk#os.walk">https://docs.python.org/2/library/os.html?highlight=os.walk#os.walk</a><br>
　　该函数可以实现的是对某分区内所有文件进行遍历，所以我们还需要检测系统有哪些分区。可以通过ctype包来实现。</p>

<blockquote>
<p>import ctypes</p>

<p>def FindAllDesk():<br>
　　result=[]<br>
　　lpBuffer = ctypes.create_string_buffer(78)<br>
　　ctypes.windll.kernel32.GetLogicalDriveStringsA(ctypes.sizeof(lpBuffer), lpBuffer)<br>
　　vol = lpBuffer.raw.split('\x00'.encode())<br>
　　for i in vol:<br>
　　　　if i:<br>
    result.append(i.decode().strip('\\'))<br>
   return result<br>
  将返回的result进行处理并赋给os.walk的top参数，也即路径。</p>
</blockquote>

<h2>计算MD5</h2>

<p>　　Python里计算MD5只需要导入hashlib即可。<br>
　　当计算简单的字符串的MD5时，只要通过以下代码即可：</p>

<blockquote>
<p>def GetStrMd5(src):<br>
　　m=hashlib.md5()<br>
　　m.update(src)<br>
　　return m.hexdigest()</p>
</blockquote>

<p>　　大文件在计算MD5时需要分成多块计算。原理相同，只需要对文件进行多次读取和多次update()即可。代码如下：</p>

<blockquote>
<p>#大文件的MD5值<br>
def GetFileMd5(filename):<br>
　　if not os.path.isfile(filename):<br>
　　　　return<br>
　　myhash = hashlib.md5()<br>
　　f = file(filename,'rb')<br>
　　while True:<br>
　　　　b = f.read(8096)<br>
　　　　if not b :<br>
　　　　　　break<br>
　　　　myhash.update(b)<br>
　　f.close()<br>
　　return myhash.hexdigest()</p>
</blockquote>
