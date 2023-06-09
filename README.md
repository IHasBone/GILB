*GILBypass* (GILB) is a python package that allows you to bypass the Global Interpreter Lock (GIL) in Python. GILB stands for Global Interpreter Lock Bypass. The GIL makes it so that only one thread can run at a time. This is a problem for programs that are CPU bound, because they can't use multiple cores. GILB allows you to bypass the GIL and use multiple cores.

Installation:
-
```shell
pip install GILBypass
```

Import as:
-
```python
import GILB
```

Example program:
-
```python
from GILB import bypass

if __name__ == '__main__':
    bypass('file.py', 10, gilb_chunk='chunk', gilb_global='global', gilb_header='header', gilb_footer='footer')
```
In this example, the file 'file.py' will be run using 10 processes. The file looks like this:
```python
# global
import time
# global

# header
import time
start = time.time()
# header

# footer
end = time.time() - start
print("Finished in", end, "seconds.")
# footer

time.sleep(1)
print("1 Finished Sleeping")
# chunk
time.sleep(1)
print("2 Finished Sleeping")
# chunk
time.sleep(1)
print("3 Finished Sleeping")
# chunk
time.sleep(1)
print("4 Finished Sleeping")
# chunk
time.sleep(1)
print("5 Finished Sleeping")
# chunk
time.sleep(1)
print("6 Finished Sleeping")
# chunk
time.sleep(1)
print("7 Finished Sleeping")
```
The output is the following:
```shell
1 Finished Sleeping
Finished in 1.0006422996520996 seconds.
2 Finished Sleeping
Finished in 1.000640630722046 seconds.
4 Finished Sleeping
Finished in 1.0006122589111328 seconds.
5 Finished Sleeping
Finished in 1.0001180171966553 seconds.
6 Finished Sleeping
Finished in 1.000612497329712 seconds.
7 Finished Sleeping
Finished in 1.000640630722046 seconds.
3 Finished Sleeping
Finished in 1.000584363937378 seconds.
```
Note that it can be in another order. This is because the processes are running at the same time.
Global is code that every process can access. It is run in every process, so the processes don't share globals.
Header is code that is at the top of the execution. It is run once in every process.
Footer is code that is at the bottom of the execution. It is run once in every process.

NOTE: The 'global' cannot access the 'header' or 'footer'. The 'header' and 'footer' cannot access the 'global'. The 'footer' can access the 'header'.

---
**All the parameters for GILB.bypass() are:**
* file: Relative or absolute path to the file to be run.
* processes: The amount of processes to run. If the amount of chunks is smaller than the amount of processes, processes=len(chunks). Defaults to multiprocessing.cpu_count()
* executor: The function to execute the code. Defaults to pythons built-in 'exec'.
* gilb_global: Name for the global tag. Defaults to 'gilb:global'
* gilb_chunk: Name for the global tag. Defaults to 'gilb:chunk'
* gilb_header: Name for the global tag. Defaults to 'gilb:header'
* gilb_footer: Name for the global tag. Defaults to 'gilb:footer'

---
# Ideas
* Have some kind of return value.
* Be able to bypass the file without a special syntax.
* Make it possible to have a shared resource, that all processes can access.
* Make it possible to use the file as a module (import it and use its functions).

---
### For more functionality, visit the [GitHub](https://github.com/IHasBone/GILB).
