---
layout: post
comments: true
title: 'Elantech 터치패드를 사용하는 우분투 랩탑, 먹통 해결법'
tag: [Ubuntu, Elantech, Touchpad, Ubuntu 16.04.2 LTS]
category: blog
date: 2017-08-06 15:00
headerImage: false
author: dogfooter
comments: true
---

펜티엄 프로세서 노트북에서 윈도우에 linux vm을 쓰며 생활했지만, 한계가 보였다. 그래서 갈아엎었다. 우분투로.

집에서 마우스로 사용했을때는 몰랐는데 회사와서 터치패드를 만져보니 문제가 발생했다. 터치패드가 안먹힌다.

## 터치패드 드라이버가 없나?

```bash
xinput
```

xinput 명령어를 통해서 현재 잡혀있는 입력디바이스 (마우스, 키보드)를 확인한다.

![xinput_img](/img/xinput.png)

만일 Elantech Touchpad라는 기기가 보인다면 다음에 제시한 방법으로 문제를 해결해보자.

## 문제 해결

```bash
# shell
# 여기서 vim이 아닌 다른 에디터여도 상관없다.
sudo vim /etc/default/grub

# 에디터에서
# 아래 부분을 다음과 같이 수정한다.
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash i802.kbdreset=1"

# 저장 후 shell
sudo update-grub

# 재부팅
reboot
```

이외에 인터넷에는 i8042의 여러 설정을 바꾸어보는 해결법이 있지만 Elantech Touchpad의 경우는 이 방법이 잘 되는것 같다.



## 출처

[모를 땐 스택오버플로](https://askubuntu.com/questions/636350/elantech-touchpad-not-detected-anymore-on-ubuntu-15)

