# symbolic links

## Symbolic \(soft\) link 

```text
ln -s 경로1 경로2
```

​경로1 : "soft link 위치에서" 참조하고자하는 원본의 상대경로.

경로2 : soft link 파일 경로. 현재 내 위치 기준으로 상대위치/절대위치 다 가능. 파일을 어디 만들것인지 알려주는 용도.

## Symbolic links of default commands

update-alternatives명령어로 가능

자주 사용하는 옵션으로는 remove-all, install, config가 있다.

### --install

Add a group of alternatives to the system.

```text
update-alternatives --install link name path priority [--slave link name path]...
```

* **link**: the generic name for the **master link**
* **name**: name of its symlink in the alternatives directory
* **path**: the **alternative** being introduced for the master link.
* **priority**: higher number means higher priority
* **The arguments after slave**: same as the master. \(generic name, symlink name, alternative path for the slave link\). Note that the master alternative must exist or the call will fail. However if a slave alternative doesn't exist, slave alternative link will simply not be installed
* 
### --remove-all

```text
update-alternatives --remove-all name
```

Remove all alternatives and all of their associated slave links.



### --config

Show available alternatives for a link group and allow the user to interactively select which one to use.

```text
update-alternatives --config name
```



## Examples

### 1. gcc

```text
sudo update-alternatives --remove-all gcc
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 90 --slave /usr/bin/g++ g++ /usr/bin/g++-5
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 80 --slave /usr/bin/g++ g++ /usr/bin/g++-6
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 70 --slave /usr/bin/g++ g++ /usr/bin/g++-7

sudo update-alternatives --config gcc

```

### 2. python

```text
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 9
sudo update-alternatives --config python
```





## Ref

[http://manpages.ubuntu.com/manpages/trusty/man8/update-alternatives.8.html](http://manpages.ubuntu.com/manpages/trusty/man8/update-alternatives.8.html)

[https://linuxhint.com/update\_alternatives\_ubuntu/](https://linuxhint.com/update_alternatives_ubuntu/)





