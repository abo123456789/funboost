####  这个里面是实现各种并发池，框架使用不同种类的并发池从而使用不同的并发模式来执行函数任务。


```python

'''
各种并发池的api都实现了submit，然后就自动执行函数。类似concurrent.futures包的api
'''


def fun(x):
    print(x)

pool = Pool(50)
pool.submit(fun,1)


```

```
实现的池包括


gevent

eventlet

asyncio

custom_threadpool_executor.py 可变有界线程池,可变是指线程池嫩自动扩大，最厉害的是能自动缩小线程数量，官方不具备此功能。
如果线程池submit任务稀疏，即使设置500并发，但不会开到500线程，官方不具备此功能。 


flexible_thread_pool.py  从新开始写的，完全没有任何官方半点代码的线程池，和 custom_threadpool_executor.py 功能一样，
可变有界线程池，可以自动扩大也能自动缩小，增加了支持运行 async def 的函数。

```