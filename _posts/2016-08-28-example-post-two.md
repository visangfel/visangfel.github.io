---
title: |
  SonarQube 도입하기 (부재:응답하라 2019)
categories:
- Code Quality
excerpt: 소나큐브 설치, 사용 방법, 도입 이유를 소개합니다.
feature_text: |
  **#리팩토링 병아리🐣 #레거시에서 하나씩 고치기**  
  리팩토링 한 줄조차 막막해했던 과거의 제게 보내는 글입니다. 💌
feature_image: "https://images.unsplash.com/photo-1518655048521-f130df041f66?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80"
---

## 팀에 SonarQube를 도입한 이유
안녕하세요. 비상교육 에듀테크컴퍼니에서 백엔드 개발자로 일하고 있는 '차다희'입니다.  
현재 팀에서 일한지 2년이 지났는데요 (오늘이 딱 입사 2년차👏👏)  
**레거시를 개선하자**는 선배의 제안에 어디서부터 무엇을 고쳐야할지 몰라 동공 지진하던 2019년도의 제가 떠올랐습니다.
{% include figure.html image="https://img.animalplanet.co.kr/news/2019/11/07/700/jt2v590h58s0016316k3.jpg" caption="ㅅ..살려줘.." width="300" %}

이 글은 (1) 동일한 고민 중인 개발자들, 그리고 (2) 2019년도의 저를 위해 작성했습니다.

리팩토링하는 경우는 2가지입니다.  

case 1. 사수의 지시로 특정 모둘을 개선한다.  
case 2. 알아서 찾아서 고치기  

2019년에 첫 리팩토링 작업을 진행할 당시, 수정할 부분을 지시 받았기에 작업을 빠르게 시작할 수 있었습니다. (1번 케이스)    
문제는 실무를 진행하면서 생겼는데요. 어느 부분을 고칠 것인지 스스로 판단해야하는 것이었습니다. 즉, **문제 정의 능력**이 필요했습니다. (2번 케이스)  

*<center>"꼭 고쳐야하는 코드는 어떤것인가?"</center>*  

제겐 Code smells를 찾는 개코가 없었기에 인공 개코를 찾아나섭니다. 🐶
{% include figure.html image="https://t1.daumcdn.net/cfile/tistory/257BEE3A586AA0DB21" caption="언제봐도 귀여운 강아지 코" width="300" %}
타 회사에서는 어떻게 **코드 개선점**을 발견하고, **코드 퀄리티를 개선**할까?  
많이 언급되는 방법 중 하나가 '정적 코드 분석 툴' [소나큐브](https://www.sonarqube.org/){:target="_blank"}였습니다.

## SonarQube? 그게 뭐야? 🤔
>소나큐브(SonarQube, 이전 이름: 소나/Sonar)[2]는 20개 이상의 프로그래밍 언어에서 **버그, 코드 스멜, 보안 취약점**을 발견할 목적으로 정적 코드 분석으로 자동 리뷰를 수행하기 위한 지속적인 **코드 품질 검사용 오픈 소스 플랫폼**이다. 소나소스(SonarSource)가 개발하였다. 소나큐브는 **중복 코드, 코딩 표준, 유닛 테스트, 코드 커버리지, 코드 복잡도, 주석, 버그 및 보안 취약점의 보고서**를 제공한다.  
(출처: [위키피디아](https://ko.wikipedia.org/wiki/%EC%86%8C%EB%82%98%ED%81%90%EB%B8%8C){:target="_blank"})

조금 덧붙이자면, **정적분석**은 소스코드 or 컴파일된 코드를 분석하여 코드 상의 문제점을 찾아냅니다. 

## SonarQube를 선택한 이유
- 여러 언어 분석 지원
- 다양한 플러그인 지원
- 오픈 소스로 지속적 업데이트
- 무료  
  (developer버전에서 지원되는 추가 기능이 있지만 현재 팀에서는 필요하지 않다고 판단했습니다.)  
위처럼 다양한 이유가 있지만 **레퍼런스가 많다**는 장점이 1순위였습니다.
  
## 프로젝트에 적용하기
"소나큐브 도입 어렵지 않아요! 설치 금방해요-"라는 후기가 대다수.  
저는 그 말에 용기를 얻어 서버에 설치를 시작합니다. ~~(그렇게 시작된 삽질의 여정)~~
{% include figure.html image="https://2runzzal.com/uploads/zpicture/org/A3qTQbP86P.png" caption="삽질이_모여_실력이_될거야_룰루.jpg" width="300" %}

### 개발 및 인프라 환경 확인  
**개발**  
  👉 JAVA 8   
  👉 Spring Boot 2.4.4   
  👉 Maven 3.6.3  

**인프라**  
  👉 Centos 7.5  
  👉 Jenkins 2.303.3

### 로컬에서 테스트 해보자
**1. 다운로드**  
[커뮤니티 버전](https://www.sonarqube.org/downloads/){:target="_blank"} 으로 다운로드해주세요.  
※ Developer 버전을 사용하면 각 브랜치별로 분석이 가능하지만, community 버전은 브랜치 하나만 분석 가능합니다.  
저희는 main 브랜치에 merge하기 전 품질 테스트를 하기로 결정하여, community 버전을 사용했습니다. 

**2. 실행**  
`sh sonar.sh start`  
![1.png](/assets/images/posts/1/1.png)  

**3.localhost:9000으로 접속**  
id와 패스워드는 각각 기본 값 admin입니다.  
![2.png](/assets/images/posts/1/2.png)  

**4. 프로젝트 생성**  
**4.1 create project - Manually 선택**
![3.png](/assets/images/posts/1/3.png)  

**4.2 프로젝트명 설정**  
SonarQube 대시보드에 노출될 프로젝트명을 생성합니다.
![4.png](/assets/images/posts/1/4.png)  

**4.3 CI 툴 설정**  
운영에서 SonarQube를 사용할 경우, CI툴을 별도로 설정 합니다. (예. Jenkins 배포시, 코드 분석 작업 자동 실행)
지금은 테스트 단계이므로, 수동 분석만 하도록 Locally를 클릭합니다.
![5.png](/assets/images/posts/1/5.png) 

**4.4 token 생성**  
토큰 이름을 입력해줍니다. 저는 기억하기 쉽게 프로젝트 이름을 사용했습니다.
![6.png](/assets/images/posts/1/6.png)  

**4.5 프로젝트 분석**  
생성된 토큰은 메모장에 복사하여 로컬에 잘 보관해주세요.  
![7.png](/assets/images/posts/1/7.png)

프로젝트의 빌드 툴을 선택해주세요. (예. Maven)  
이후, 생성된 명령어를 메모장에 보관해주세요.  
![8.png](/assets/images/posts/1/8.png)  

터미널에서 프로젝트 repository로 이동한 후, 앞에서 생성한 명령어를 입력해줍니다.
![9.png](/assets/images/posts/1/9.png)  

**4.6 분석 결과 확인**  
분석 종료시 소나큐브 대시보드 (localhost:9000)이 자동으로 새로고침 되면서, 분석 결과가 제공됩니다.  
각 분석 결과 지표가 의미하는 바는 아래에서 자세히 설명하도록 하겠습니다. 
![10.png](/assets/images/posts/1/10.png)  

### 서버에 설치하자
SonarQube를 설치하는 방법은 (1)Docker를 사용하는 방법, 그리고 (2)시스템에 직접 설치하는 방법이 있습니다. 
현재 팀에서는 Docker를 사용하고 있지않고, 테스트 단계인 관계로 시스템에 직접 설치했습니다.  
👉 👉 소나큐브 설치 환경에선 JAVA8을 사용하는 관계로, JAVA8을 지원하는 마지막 버전인 **소나큐브 7.8**을 사용했습니다. (현재 최신 버전: 9.2)

**1.Requirements 설정**  
설치에 앞서 설치 환경 설정이 필요합니다.
**❗❗소나큐브 버전에 따라 requirements 값이 다를 수 있습니다. [Prerequisites and Overview](https://docs.sonarqube.org/7.8/requirements/requirements/){:target="_blank"}) 에서 원하는 버전으로 바꾸어 requirement 값을 체크해주세요**  

👉 현재 설정된 값 확인 방법: 아래 명령어 4개 실행  
```shell
sysctl vm.max_map_count
sysctl fs.file-max
ulimit -n
ulimit -u
```

👉 설정된 값이 최소 요구치보다 적을 경우 두가지 방법을 사용하여 수치를 변경할 수 있습니다.  
1.1 터미널 내 명령어 사용  
```shell
sysctl vm.max_map_count=262144
sysctl fs.file-max=65536
ulimit -n 65536
ulimit -u 4096
```

1.2 별도의 파일에 값 설정  
❗팀에서는 1.2의 방법을 사용했습니다.❗  
  *1.2.1 /etc/sysctl.conf*  
  ![11.png](/assets/images/posts/1/11.png)  
  *1.2.2 /etc/security/limits.conf*
  ![12.png](/assets/images/posts/1/12.png)

**2. 서버에 sonarqube 설치**  
```shell
# 설치
wget https://binaries.sonarsource.com/CommercialDistribution/sonarqube-developer/sonarqube-developer-7.8.zip
# 압축 해제
unzip sonarqube-developer-7.8.zip
# 압축 파일 제거
rm -rf sonarqube-developer-7.8.zip
``` 

**3. 사용자 추가**  
sonarqube폴더 관리를 위해 별도의 사용자 추가 필요  
```shell
adduser -M -r sonarqube
```

**4. 폴더 사용자 권한 변경**  
```shell
chown -R sonarqube /opt/sonarqube
```

**5. PostgreSQL 설치**  
[다운로드 링크](https://www.postgresql.org/download/linux/redhat/){:target="_blank"}에서 
사용하려는 소나큐브 버전의 requirement 환경에 맞게 설정 값 클릭 후, 자동으로 생성된 script를 서버에서 실행해줍니다.  
(설정 예시)  
![13.png](/assets/images/posts/1/13.png)  
(소나큐브 7.8 버전 기준 스크립트 예시)  
```shell
# Install the repository RPM:
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
# Install PostgreSQL:
sudo yum install -y postgresql10-server
```

**6. PostgreSQL 설정**  
**6.1 로그인**
```shell
su - postgres
```
예)  
![14.png](/assets/images/posts/1/14.png)

**6.2 사용자 생성**
```shell
psql
CREATE USER sonar WITH ENCRYPTED password 'sonar';
CREATE DATABASE sonar WITH ENCODING 'UTF8' OWNER sonar TEMPLATE=template0;
```
예) 
![15.png](/assets/images/posts/1/15.png)

**6.3 사용자 인증 방식 수정**  
`/var/lib/pgsql/10/data/pg_hba.conf` 에서 `md5`방식으로 변경  
![16.png](/assets/images/posts/1/16.png)

**6.4 디비 재기동**
```shell
systemctl restart postgresql-10
```

**7. conf 설정**
```shell
vi /opt/sonarqube/conf/sonar.properties

# User credentials.
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
#----- PostgreSQL 9.3 or greater
sonar.jdbc.url=jdbc:postgresql://127.0.0.1/sonar
# OTHERS
sonar.path.data=/var/sonarqube/data
sonar.path.temp=/var/sonarqube/temp
```

**8. 소나큐브 시작**
```shell
/opt/sonarqube/bin/linux-x86-64/sonar.sh start
```
![17.png](/assets/images/posts/1/17.png)

**9. 소나큐브 서비스 등록**  
서버 재기동시 자동으로 실행할 수있도록 서비스 등록을 합니다.   
9.1 `vi /etc/systemd/system/sonarqube.service`  
9.2 내용 입력
```shell
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

User=sonarqube
Group=sonarqube

ExecStart=/bin/nohup /opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop

LimitNOFILE=65536
LimitNPROC=8192

RestartSec=120
Restart=always

[Install]
WantedBy=multi-user.target
```

**9.3 서비스 갱신**
```shell
sudo systemctl daemon-reload
```

**9.4 서비스 정상 동작 여부 확인**
![18.png](/assets/images/posts/1/18.png)

여기까지 끝내셨다면 축하드립니다 (삽질을 끝내고 히죽거리던 과거의 제게도 축하를 보냅니다 흐흐🥂🥂)
{% include figure.html image="https://mblogthumb-phinf.pstatic.net/20150708_30/vysegirlv_1436362830408tgAwE_JPEG/20140514_150837_80945085.jpg?type=w2" caption="3일간의_삽질_끝에_성공.jpg" width="300" %}


## Reference
* [Linux SonarQube 설치](https://confluence.curvc.com/pages/viewpage.action?pageId=6160585){:target="_blank"}  
* [Prerequisites and Overview](https://docs.sonarqube.org/7.8/requirements/requirements/){:target="_blank"}  
* [코드 분석 도구 적용기 - 3편, SonarQube 적용하기](https://seller-lee.github.io/static-code-analysis-part3){:target="_blank"}  