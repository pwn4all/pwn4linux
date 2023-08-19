# pwntools 기본 설정

##### context 설정
```python
from pwn import *

context(arch='i386', os='linux')
or
context(arch='amd64', os='linux')
context.log_level = 'DEBUG'
```

##### elf 와 libc 설정
```python
filename = './binary'
elf = context.binary = ELF(filename)
libc = elf.libc
conn = process()
```

##### libc_base_address 를 libc.address ELF 클래스 변수 libc.address 에 저장
```python
## libc.address = 0x0 (default value)
# save libc_base_addr
libc.address = puts_leak - libc.sym['puts']
# how to use about libc_base_addr
libc.sym['system']
next(libc.search(b'/bin/sh\x00'))
```


##### libc_base_address 를 libc.address 수동 변수 저장
```python
system_offset = libc.sym["system"]
system_addr = libc_base + system_offset
```


##### 함수 주소 확인 방법
```python
## libc 라이브러리에 있는 puts 함수의 libc_base 에서의 offset(거리)
libc.sym["puts"]
libc.symbols["puts"]
# 32-bit) : 0x73260
# 64-bit) : 0x80ed0

## binary 에 있는 puts.plt 주소
elf.plt["puts"]

## binary 에 있는 puts.got 주소
elf.got["puts"]
# 32-bit) : 0xf7d33260
# 64-bit) : 0x7f3070306ed0
```
