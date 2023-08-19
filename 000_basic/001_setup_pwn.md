# Ubuntu 22.04 (python3.10)

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


##### Ubuntu 23.04 에서의 기본 설정
```bash
# python3.11 가상환경
$ sudo mkdir /venv
$ sudo chown user:user /venv
$ cd /venv

$ sudo apt install python3.11-venv
$ python3 -m venv python311
$ source /venv/python311/bin/activate

##### utils dir
(python311) $ sudo mkdir /utils
(python311) $ sudo chown user:user /utils
(python311) $ mkdir /utils/peda
(python311) $ mkdir /utils/pwndbg
(python311) $ mkdir /utils/gef
```


##### 기본 패키지
```bash
(python311) $ sudo apt install gcc gcc-multilib gdb gdb-multiarch python3 python3-pip python3-dev git libffi-dev build-essential
```


##### pwndbg
```bash
(python311) $ git clone https://github.com/pwndbg/pwndbg.git /utils/pwndbg
(python311) $ cd /utils/pwndbg
(python311) $ ./setup.sh
(python311) $ echo "source /utils/pwndbg/gdbinit.py" >> ~/.gdbinit
```


##### peda
```bash
(python311) $ git clone https://github.com/longld/peda.git /utils/peda
(python311) $ echo "source /utils/peda/peda.py" >> ~/.gdbinit
```


##### gef
```bash
(python311) $ cd /utils/gef
(python311) $ wget -O gdbinit-gef.py -q https://gef.blah.cat/py
(python311) $ echo "source /utils/peda/peda.py" >> ~/.gdbinit
```

##### 기타 유틸
```bash
(python311) $ pip install pwntools
(python311) $ pip install ROPgadget

(python311) $ sudo apt install ruby
(python311) $ sudo gem install one_gadget
```

##### libc database
<kbd style="background-color: #f0f0f0; font-size: 24px;">
  <a href="https://libc.blukat.me/" target="_blank">
    <span style="font-size: 24px;">https://libc.blukat.me/</span>
  </a>
</kbd>
