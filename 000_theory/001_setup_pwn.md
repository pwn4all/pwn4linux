# 구축 환경 : Ubuntu 22.04 (python3.10)

##### 기본 업데이트
```bash
$ sudo apt update
$ sudo apt install vim
$ sudo apt install openssh-server
$ sudo vi /etc/ssh/sshd_config
.
.
PasswordAuthentication yes
.
.
$ sudo systemctl restart ssh


$ sudo vi /etc/vim/vimrc
.
.
"====================================================================
set tabstop=2
set shiftwidth=2
set expandtab
"====================================================================
```


##### 기본 패키지
```bash
$ sudo apt install gcc gcc-multilib gdb gdb-multiarch python3 python3-pip python3-dev git libffi-dev build-essential
```


##### pwndbg
```bash
$ git clone https://github.com/pwndbg/pwndbg.git /utils/pwndbg
$ cd /utils/pwndbg
$ ./setup.sh
$ echo "source /utils/pwndbg/gdbinit.py" >> ~/.gdbinit
```


##### peda
```bash
$ git clone https://github.com/longld/peda.git /utils/peda
$ echo "source /utils/peda/peda.py" >> ~/.gdbinit
```


##### gef
```bash
$ cd /utils/gef
$ wget -O gdbinit-gef.py -q https://gef.blah.cat/py
$ echo "source /utils/peda/peda.py" >> ~/.gdbinit
```

##### 기타 유틸
```bash
$ pip install pwntools
$ pip install ROPgadget

$ sudo apt install ruby
$ sudo gem install one_gadget
```

##### libc database
<kbd style="background-color: #f0f0f0; font-size: 24px;">
  <a href="https://libc.blukat.me/" target="_blank">
    <span style="font-size: 24px;">https://libc.blukat.me/</span>
  </a>
</kbd>
