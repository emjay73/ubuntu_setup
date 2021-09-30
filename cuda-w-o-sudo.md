# Install  cuda w/o sudo



### cuda install runfile실행

```text
chmod +x ./runblabla
sh ./runblabla
```

### 체크해제 

\[ \] Driver 

\[ \] samples

\[ \] demo

\[ \] doc

![](.gitbook/assets/image%20%286%29.png)

### Options &gt; Library install path &gt; 경로입력 

\(sudo 권한이 필요 없는 곳으로 변경\)

기존 : blank, which means.. /usr/local/cuda/lib64

변경 : /home/minjungkim/Install/cuda-11.0/lib64 

![](.gitbook/assets/image%20%289%29.png)

![](.gitbook/assets/image%20%2814%29.png)

### Advanced mode 진입

+가 있는 줄에서 A를 누르면 Advanced options로 들어감

![](.gitbook/assets/image%20%288%29.png)



### 체크 해제 : change symbolic link from /usr/local/cuda

![](.gitbook/assets/image%20%2810%29.png)



### Change Toolkit Install Path 변경

sudo 권한이 필요 없는 곳으로 변경

기존 : /usr/local/cuda-11.0/

변경후 : /home/minjungkim/Install/cuda-11.0/

![](.gitbook/assets/image%20%2813%29.png)

### 

### Resulting Output

![](.gitbook/assets/image%20%2812%29.png)



### 환경변수 설정

```text
vim ~/.bashrc

# add the following lined
export PATH=/usr/local/cuda-10.2/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```



## Reference

{% embed url="https://stackoverflow.com/questions/39379792/install-cuda-without-root" %}



{% embed url="https://yunmorning.tistory.com/30" %}



