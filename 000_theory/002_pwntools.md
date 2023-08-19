# pwntools 기본 설정

#### context 설정
```python
from pwn import *

context(arch='i386', os='linux')
or
context(arch='amd64', os='linux')
context.log_level = 'DEBUG'
```


#### log 출력
```python
>>> log.success("hello success")
[+] hello success
>>> log.info("hello infomation")
[*] hello infomation
>>> log.error("hello error")
[ERROR] hello error
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/user/.local/lib/python3.10/site-packages/pwnlib/log.py", line 439, in error
    raise PwnlibException(message % args)
pwnlib.exception.PwnlibException: hello error
>>>
```


#### elf 와 libc 설정
```python
filename = './binary'
elf = context.binary = ELF(filename)
libc = elf.libc
conn = process()
```


#### libc 에서 /bin/sh 문자 주소 검색
```python
>>> hex(next(libc.search(b"/bin/sh\x00")))
'0x1d8698'
>>> 
```


#### libc_base_address 를 libc.address ELF 클래스 변수 libc.address 에 저장
```python
## libc.address = 0x0 (default value)
# save libc_base_addr
libc.address = puts_leak - libc.sym['puts']
# how to use about libc_base_addr
libc.sym['system']
next(libc.search(b'/bin/sh\x00'))
```


#### libc_base_address 를 libc.address 수동 변수 저장
```python
system_offset = libc.sym["system"]
system_addr = libc_base + system_offset
```


#### 함수 주소 확인 방법
##### puts.plt(puts.got) payload 로 유출되는 주소는 puts 의 libc offset 이다.
```python
## libc 라이브러리에 있는 puts 함수의 libc_base 에서의 offset(거리)
libc.sym["puts"]
libc.symbols["puts"]
# 32-bit) : 0x73260
# 64-bit) : 0x80ed0

## binary 에 있는 puts.plt 주소
elf.plt["puts"]

## binary 에 있는 puts.got 호출 주소
elf.got["puts"]
# 32-bit) : 0xf7d33260
# 64-bit) : 0x7f3070306ed0
```



#### pwntools ROP 로 gadget 검색
```python
>>> from pwn import *
>>>
>>> elf = context.binary = ELF('./binary')
[*] '/binary'
    Arch:     amd64-64-little
    RELRO:    No RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x400000)
>>> rop = ROP(elf)
[*] Loaded 8 cached gadgets for './binary'
>>>
>>> rop.vuln_func(elf.sym['vuln_func'])
>>>
>>> print(rop.dump())
0x0000:         0x40119e pop rdi; ret
0x0008:         0x4011a7 [arg0] rdi = vuln_func
0x0010:         0x4011a7 vuln_func
>>> hex(rop.find_gadget(['pop rdi', 'ret']).address)
'0x40119e'
>>>
