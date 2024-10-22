```python
import threading
import time

var_i=None
def worker_2():
    i=0
    global var_i
    while True:
        result=i**2
        print(result)
        i+=1
        if i>10:
            break

def worker_3():
    i=0
    global var_i
    while True:
        result=i**3
        print(result)
        i+=1
        if i>10:
            break

t = threading.Thread(target=worker_2)
t2 = threading.Thread(target=worker_3)
t.start()
t2.start()
```

    0
    1
    4
    9
    16
    25
    36
    49
    64
    81
    100
    0
    1
    8
    27
    64
    125
    216
    343
    512
    729
    1000
    


```python
import threading
import time

var_i = None
def worker():
    global var_i
    i=1
    while True:
        print(i)
        i+=1
        
        if var_i is not None:
            break
        time.sleep(1)
t = threading.Thread(target=worker)
t.start()
t2 = threading.Thread(target=worker)
t2.start()
t3 = threading.Thread(target=worker)
t3.start()
time.sleep(10)
var_i = 1

```


```python
import asyncio
import time
# 4 3 5 6 7 8 1
numbers = [4, 3, 5, 6, 7, 8, 1]

async def square():
    global numbers
    for i in numbers:
        quad = i**2
        print (f'{i} в квадрате - {quad}')
        await asyncio.sleep(1)
    print("Посчитано.")

async def cube():
    cube_num = input(print("введите для куба"))
    a=cube_num.split()
    for i in a:
        cub = int(i)**3
        print (f'{i} в кубе - {cub}')
        await asyncio.sleep(1.5)
    print("Посчитаны кубы!.")

async def main():
    task1 = asyncio.create_task(square())  
    task2 = asyncio.create_task(cube())

    await task1
    await task2

asyncio.run(main())

#await square()
```


    ---------------------------------------------------------------------------

    RuntimeError                              Traceback (most recent call last)

    Cell In[8], line 30
         27     await task1
         28     await task2
    ---> 30 asyncio.run(main())
    

    File D:\Python\Lib\asyncio\runners.py:190, in run(main, debug, loop_factory)
        161 """Execute the coroutine and return the result.
        162 
        163 This function runs the passed coroutine, taking care of
       (...)
        186     asyncio.run(main())
        187 """
        188 if events._get_running_loop() is not None:
        189     # fail fast with short traceback
    --> 190     raise RuntimeError(
        191         "asyncio.run() cannot be called from a running event loop")
        193 with Runner(debug=debug, loop_factory=loop_factory) as runner:
        194     return runner.run(main)
    

    RuntimeError: asyncio.run() cannot be called from a running event loop



```python
import os
from multiprocessing import Process


def factorial(number):
    result = 1
    for i in range (1, number+1):
        result*=i
    proc = os.getpid()
    print(f'{i} факториал = {result} номер процесса {proc}'.format(
        number, result, proc))


if __name__ == '__main__':
    numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    procs = []

    for index, number in enumerate(numbers):
        proc = Process(target=factorial, args=(number,))
        procs.append(proc)
        proc.start()

    for proc in procs:
        proc.join()

    
"""
#определение C из n по k для заданного n при k от 1 до n

def C_n_k (n, k, m):
    n_fact = 1
    k_fact = 1
    n_k_fact = 1
    for o in range (1, n+1):
        n_fact*=o
    for p in range (1, k+1):
        k_fact*=p
    for q in range (1, m+1):
        n_k_fact*=q
    proc = os.getpid()
    result = n_fact/(k_fact*n_k_fact)
    print(f'C из {n} по {k} = {result}, номер процесса {proc}'.format(n, k, result, proc))
    


if __name__ == '__main__':
    #numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    procs = []
    n=int(input(print("Введите n для перебора C из n по k")))
    for i in range (1, n+1):
        k=n-i
        proc = Process(target=C_n_k, args=(n, i, k,))
        procs.append(proc)
        proc.start()


    for proc in procs:
        proc.join()"""

```


