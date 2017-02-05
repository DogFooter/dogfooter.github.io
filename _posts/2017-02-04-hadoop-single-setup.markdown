---
layout: post
comments: true
title: '[번역] 하둡: 싱글 노드 클러스터를 설정하자'
---

원글 : http://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-common/SingleCluster.html

## 목적

이 문서는 싱글 노드 하둡 설치를 어떻게 설정하고 구성하는지 설명한다. 이번 문서를 통해 간단한 하둡 맵리듀스 혹은 하둡 분산 파일 시스템(HDFS)를 짧은 시간내에 구동해 볼 수 있다.

## 미리 준비할 것

### 지원하는 플랫폼

* GNU/Linux는 개발 생산 플랫폼으로 지원한다. 하둡은 2000개의 노드들을 가진 GNU/Linux cluster에서 데모 시연되었다.
* Windows도 지원된다. 그러나 이번에 작성된 내용들은 리눅스 기준으로 작성되었습니다. 윈도우에서의 하둡은 여기 [위키][1]에서 확인할 수 있다.

### 필요한 소프트웨어

리눅스를 포함해서 필요한 소프트웨어는 다음과 같다.

1. Java가 필수적으로 설치되어 있어야한다. 권장하는 Java의 버전은 [HadoopJavaVersions][2]에서 설명한다.
2. ssh가 무조건 설치되어 있어야한다. 그리고 sshd는 하둡 데몬들을 관리하는 하둡 스크립트를 사용하기위해  무조건 실행되고 있어야한다.

### 소프트웨어 설치

만약 당신의 클러스터에 필수 소프트웨어가 없다면 설치해야한다.
Ubuntu Linux를 예시로

```bash
$ sudo apt-get install ssh
$ sudo apt-get install rsync
```

## 다운로드

하둡 배포판을 받기위해서 최신 안정판(recent stable release)을 [ Apache Download Mirrors ] 중 한곳에서 다운로드 받는다.

## 하둡 클러스터를 시작하기 전 준비

하둡 배포판의 압축을 해제한다. 인자값들을 정의하기 위해 배포판 안에있는 파일중 `` etc/hadoop/hadoop-env.sh ``를 다음과 같이 수정한다.

```bash
# Java가 설치된 root 디렉토리를 설정한다
export JAVA_HOME=/usr/java/latest
```

다음 명령을 실행해보자.

```bash
$ bin/hadoop
```

하둡 스크립트를 위한 사용법을 보여줄것이다.

이제 하둡 클러스터를 시작하기 위한 다음의 세 가지 방법 중 하나를 시도해 볼 준비가 되었다.

* Local (Standalone) Mode
* Pseudo-Distributed Mode
* Fully-Distributed Mode

## Standalone Operation

기본 설정으로 하둡은 분산되지 않은 모드, 하나의 Java 프로세스로서 실행하게 구성되어있다. 이는 디버깅에 매우 유용한다.
다음의 예제는 conf 디렉토리를 인풋으로 이용하여 주어진 정규표현식에 부합하는 결과물을 보여주는것이다. 아웃풋은 주어진 아웃풋 디렉토리에 작성되어진다.

```bash
$ mkdir input
$ cp etc/hadoop/*.xml input
$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'
$ cat output/*
```

## Pseudo-Distributed Operatoin

하둡은 또한 싱글 노드에서 가상의 분산환경 모드를 지원한다. 하둡 데몬들은 각각 분리된 자바 프로세스로 작동한다.

### 구성

다음에 오는것을 사용하라.

``etc/hadoop/core-site.xml``:

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

`` etc/hadoop/hdfs-site.xml ``:

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

### passphraseless ssh (암호 없는 ssh) 설정

이제 localhost로 암호 없이 ssh 접속이 가능한지 체크해본다.

```bash
$ ssh localhost
```

만약 암호없이 접근할 수 없다면, 다음 명령을 실행하라.

```bash
$ ssh-keygen -t rsa -P `` -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

### 실행

다음은 맵리듀스 잡(job)을 로컬에서 실행하는 방법이다. 만약 YARN에서 실행하고 싶다면. YARN on Single Node를 보라.

1. 파일시스템 포맷
	 
		$ bin/hdfs namenode -format 
	

2. 네임노드 데몬, 데이터노드 데몬 실행

	 	$ sbin/start-dfs.sh
	 
	하둡 데몬 로그들은 ```$HADOOP_LOG_DIR``` 디렉토리에 작성된다. (기본적으로  ```$HADOOP_LOG_DIR/logs```)

3. 네임노드를 위한 웹브라우저 인터페이스를 켜라. 기본적으로 다음 주소에서 접속 가능하다:

	http://localhost:50070/

4. 맵리듀스 잡(job) 실행을 위한 HDFS 디렉토리를 만든다.

		$ bin/hdfs dfs -mkdir /user
		$ bin/hdfs dfs -mkdir /user/<username>

5. 분산 파일시스템에 인풋파일을 복사한다.
		$ bin/hdfs dfs -put etc/hadoop input

6. 제공된 예제를 실행한다.

		$  bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'


7. 아웃풋 파일을 검사한다. 분산 파일시스템으로 부터 아웃풋파일을 복사해오고 검사한다.

		$ bin/hdfs dfs -get output output
		$ cat output/*
	
	혹은

	분산 파일시스템에서 바로 아웃풋 파일을 본다.
	
		$ bin/hdfs dfs -cat output/*
	
8. 다했으면 데몬을 종료한다.
	
		$ sbin/stop-dfs.sh

### YARN on Single Node

맵 리듀스 잡(job)을 YARN위에서 pseudo-distributed 모드로 실행할 수 있다. 몇 개의 인자를 바꾸어주고 리소스 매니저 데몬과 노드매니저 데몬을 추가적을 쇨행시키면 된다.

위에서 본 1 ~ 4까지의 순서는 이미 실행했다고 가정한다.

1. 다음과 같이 인자값을 구성하라

	``etc/hadoop/mapred-site.xml`` :
		
		<configuration>
			<property>
				<name>mapreduce.framework.name</name>
				<value>yarn</value>
			</property>
		</configuration>
	
	``etc/hadoop/yarn-site.xml``:
	
		<configuration>
		    <property>
			<name>yarn.nodemanager.aux-services</name>
			<value>mapreduce_shuffle</value>
		    </property>
		</configuration>


2. 리소스 데몬과 노드 메니저 데몬을 실행한다.

		$ sbin/start-yarn.sh

3. 리소스 매니저를 위한 웹 브러우저 인터페이스를 켠다. 기본적으로 다음 주소에서 접속 가능하다.
	
	http://localhost:8088/

4. 맵 리듀스 잡을 실행시킨다.

5. 다 했으면 데몬을 종료한다.

		$ sbin/stop-yarn.sh
		
### Fully-Distributed Operation

다음 번 자료에서 소개할 것이다. (cluster setup)

