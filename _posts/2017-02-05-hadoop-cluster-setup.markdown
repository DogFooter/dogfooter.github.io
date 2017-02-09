---
layout: post
comments: true
title: '[번역] 하둡 클러스터 셋업 다중 노드'
tags: [하둡, Hadoop]
---

## 목적
이 문서는 하둡 클러스터를 다양한 갯수의 노드들로 설치하고 설정하는지 설명한다. 하둡을 사용하기 위해서 단일 시스템에 하둡을 설치해야한다.

싱글노드 [원문]() ,[번역본 : 오피셜이 아닌 제가 번역한 링크입니다]()

## 필요한 것들

* Java를 설치해야한다. [하둡 위키]()를 보고 맞는 버전을 찾을 수 있다.
* 하둡 stable 버전을 아파치 미러에서 다운로드 받는다.

## 설치

하둡 클러스터를 설치하는건 전형적으로 소프트웨어를 모든 머신들에 언패키징하는 방법이나 운영체제에 알맞은 패키징 시스템으로 설치하는 방법을 뜻한다.

## Non-Secure 모드로 하둡 설정

하둡의 자바 설정은 두 종류의 중요한 설정 파일로 구동된다.

* Read-only 기본 설정 - `` core-default.xml `` , `` hdfs-default.xml ``, `` yarn-default.xml ``,  `` mapred-default.xml ``
* Site-specific 설정 - `` etc/hadoop/core-site.xml ``, `` etc/hadoop/hefs-site.xml ``, `` etc/hadoop/yarn-site.xml``, ``etc/hadoop/mapred-site.xml``

추가적으로 배포판에 `` bin/ `` 디렉토리안에있는 하둡 스크립트를 제어할 수 있는데 `` etc/hadoop/hadoop-env.sh``와 `` etc/hadoop/yarn-env.sh `` 를 통하여서 site-specific한 값들을 설정해주면 된다.

하둡 클러스터를 설정하기 위해서 하둡 데몬이 실행되는 `` environment ``와 하둡 데몬의 `` cofiguration arameters``을 설정해주어야 한다.

HDFS 데몬들은 NameNode, SecondaryNameNode, DataNode이다. YARN 데몬ㅇ들은 ResourceManager, NodeManager, WebAppProxy이다. 맵리듀스가 사용되어야한다면, MapReduce Job History Server도 돌아가야한다. 대형 설치의 경우 일반적으로 별도의 호스트에서 실행된다.

### 하둡 데몬의 환경 설정

Admin은 하둡 데몬 프로세스 환경의 site-specific한 커스터마이징을 위해 `` etc/hadoop/hadoop-env.sh``와 선택적으로 `` etc/hadoop/yarn-site.xml``, ``etc/hadoop/mapred-site.xml`` 스크립트를 사용해야한다.

아주 최소한 JAVA_HOME은 꼭 설정해야한다. 각 remote-node들에 정확히 설정해야한다.

Admin은 다음 테이블에 나온 설정 옵션을 사용해 각각의 데몬설정을 할 수 있다.

|데몬|환경 변수|
|--|--|
|NameNode|HADOOP_NAMENODE_OPTS|
|DataNode|HADOOP_DATANODE_OPTS|
|SecondaryNameNode|HADOOP_SECONDARYNAMENODE_OPTS|
|ResourceManager|YARN_RESOURCEMANAGER_OPTS|
|NodeManager|YARN_NODEMANAGER_OPTS|
|WebAppProxy|YARN_PROXYSERVER_OPTS|
|Map Reduce Job History Server|HADOOP_JOB_HISTORYSERVER_OPTS|

예를 들면, Namende가 parallelGC를 사용하도록 설정하기 위해서, 다음의 문장이 ``hadoop-env.sh``에 추가되어야한다.

```bash
export HADOOP_NAMENODE_OPTS="-XX:+UserPrallelGC"
```

다른 예시를 위해 ``etc/hadoop/hdoop-env.sh``를 보자.

* HADOOP_PID_DIR - 데몬들의 프로세스 아이디 파일들이 저장될 디렉토리
* HADOOP_LOG_DIR - 데몬들의 로그 파일들이 저장될 디렉토리. 로그들은 자동으로 생성된다.
* HADOOP_HEAPSIZE/YARN_HEAPSIZE - MB 단위로 사용할 수 있는 최대 Heapsize의 양. 만약 변수가 1000으로 설정되어 있으면 1000MB로 heap이 설정될 것이다. 데몬의 힙사이즈를 설정하는 값이다. 기본값은 1000이다. 각 데몬마다 다른 값을 주고 싶을때 사용할 수 있다.

대부분의 경우 HADOOP_LOG_DIR과 HADOOP_PID_DIR의 디렉토리의 경우 하둡 데몬을 실행시킬 유저가 작성할수 있는 디렉토리로 설정한다. 그렇지 않으면 symlink attack등의 위험이 있다.

또한 시스템 전반의 쉘 환경 설정에서 HADOOP_PREFIX를 설정하는것은 일반적이다. 예를 들면 ``etc/profile.d``에있는 스크립트파일과 같은 것이다.

```bash
HADOOP_PREFIX=/path/to/hadoop
export HADOOP_PREFIX
```

### 하둡 데몬 설정

이번 섹션에선 다음에 주어진 설정파일들의 중요한 파라미터들을 다룰것이다.

* ``etc/hadoop/core-site.xml``

|Parameter |Value |Notes |
|--- |--- |--- |
|fs.defaultFS|NameNode URI|hdfs://host:port/|
|io.file.buffer.size|131072|ㅣSequenceFiles에서 사용될 read/write buffer size|

* ``etc/hadoop/hdfs-site.xml``
* NameNode를 위한 설정

|Parameter |Value |Notes |
|--- |--- |--- |
|dfs.namenode.name.dir|NameNode가 namespace와 transactions log들을 영구적으로 저장하기위한 로컬 파일시스템 path.|만약 디렉토리 리스트가 컴마 ','로 구분되어 있다면 해당 디렉토리에 복사해서 저장한다. 이는 redundancy를 위해서다|
|dfs.hosts / dfs.hosts.exclude|허가하거나 제외한 DataNode들의 리스트.|필요에 따라서 이 파일을 허락할 수있는 datanode들의 리스트를 컨트롤하기위해서 사용할 수 있다.|
|dfs.blocksize|268435456|대용량 파일시스템의 HDFS 블록 크기는 256MB이다.|
|dfs.namenode.handler.count|100|많은 수의 DataNode들로 부터 RPC들을 다루기위한 NameNode server thread가 많다.|

* DataNode를 위한 설정

|Parameter |Value |Notes |
|--- |--- |--- |
|dfs.datanode.data.dir|컴마로 구분된 DataNode의 로컬 파일시스템 path. data node의 block들을 저장해야한다.|컴마로 구분된 디렉토리 리스트라면 데이터는 모든 주어진 디렉토리에 저장될 것이다. 일반적으로 다른 장치에 있다.|


* ``etc/hadoop/yarn-site.xml``
* ResourceManager, NodeManager를 위한 설정

|Parameter |Value |Notes |
|--- |--- |--- |
|yarn.acl.enable|true / false|ACL들을 가능하게 할 것인가? 기본값은 false이다.|
|yarn.admin.acl|Admin ACL|ACL to set admins on the cluster. ACLs are of for comma-separated-usersspacecomma-separated-groups. Defaults to special value of * which means anyone. Special value of just space means no one has access.|
|yarn.log-aggregation-enable|false|Configuration to enable or disable log aggregation|

