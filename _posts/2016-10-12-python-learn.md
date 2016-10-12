---
layout: post
title: "Python:文件遍历与MD5提取"
date:   2016-10-12
excerpt: "python实现遍历目录并提取文件MD5"
tag:
- Python
---
## 文件遍历
  使用os.work()实现，该函数原型为:os.walk(top.topdown=True,onerror=None,followlinks=False)。  
  其中，top.topdown指明遍历顺序，onerror的参数应为一个function或者为空，用于异常处理。work()函数的followlinks控制函数是否会进入符号链接，该参数默认为False，所以walk()默认不会进入符号目录。  
  该函数返回值为一个三元组(dirpath, dirnames, filenames)，通过循环即可完成对目录内所有文件的遍历。  
  demo：  
    import os
    s = os.sep
    root = "d:" + s + "ll" + s
    for rt, dirs, files in os.walk(root):
      for f in files:
      fname = os.path.splitext(f)
      new = fname[0] + 'b' + fname[1]
      os.rename(os.path.join(rt,f),os.path.join(rt,new))
  os.walk文档：https://docs.python.org/2/library/os.html?highlight=os.walk#os.walk
  该函数可以实现的是对某分区内所有文件进行遍历，所以我们还需要检测系统有哪些分区。可以通过ctype包来实现。
    import ctypes
    def FindAllDesk():
      result=[]
	    lpBuffer = ctypes.create_string_buffer(78)
      ctypes.windll.kernel32.GetLogicalDriveStringsA(ctypes.sizeof(lpBuffer), lpBuffer)
      vol = lpBuffer.raw.split('\x00'.encode())
      for i in vol:
        if i:
        result.append(i.decode().strip('\\'))
	    return result</code>
  将返回的result进行处理并赋给os.walk的top参数，也即路径。

## 计算MD5
  Python里计算MD5
