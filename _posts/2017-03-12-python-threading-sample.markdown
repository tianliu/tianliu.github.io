---
layout: post
title:  "Python Threading simple code "
date:   2017-03-12
categories: tutorials
---


### Python Multi-Threading simple code ###

```python
def func1():
    pass

def func2():
    pass

if __name__ == '__main__':
    func1()
    func2()

import threading
t1_func1 = threading.Thread(target=func1,args=(Truple))
t2_func2 = threading.Thread(target=func2,args=(Truple))

threads = []
threads.appends(t1_func1)
threads.appends(t2_func2)


for t in threads:
　　t.setDaemon(True)
　　t.start()

for t in threads:
    t.join


```