
# [비상사태 기술 블로그](https://visangfel.github.io/)
[![Gem Version](https://badge.fury.io/rb/alembic-jekyll-theme.svg)](https://badge.fury.io/rb/alembic-jekyll-theme)

## 블로그 소개
안녕하세요. 에듀테크 컴퍼니 소속 비상사태의 기술 블로그입니다.  

더 많은 이들에게 교육의 기회를 제공하자는 회사의 이념을 확장하여,  
**"개발자들이 함께 성장할 수 있는 개발 문화"** 를 만들고자 매일 노력합니다.
![greeting.png](/assets/images/readme/greeting.png)  {: width="450px"}

## 문서 소개
본 문서는 Jekyll(정적페이지 생성 툴) 환경설정 & 블로그 포스팅 작성을 안내합니다. 

## 목차
* 로컬에서 실행
    * 프로젝트 clone
    * jekyll 설치
    * 프로젝트 실행
* 포스팅 작성법
* 블로그 환경 설정 방법
  * font 수정
  * 유용한 assets
    * alembic 테마 사용법
* 기타
    * 블로그 생성 도구 
    * 블로그 테마 
  
## 로컬에서 실행
### 1. 프로젝트 clone
`$ git clone https://github.com/visangfel/visangfel.github.io.git` 

### 2. Jekyll 설치
`$ gem install jekyll`

### 3. 프로젝트 실행
3.1 `$ cd visangfel.github.io.git` (프로젝트 내부로 이동)  
3.2 `$ bundle install` (패키지 설치)  
3.3 `$ jekyll serve` (서버 실행)  
3.4 브라우저에서 [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 접속시 블로그 화면 정상 출력 확인  
** 이후에는 `jekyll serve` 명령어로 서버를 로컬에서 띄우면 됩니다. 

## 페이지 구조
### 기본
- 홈: index.md
- 404 페이지: 404.md
### 메뉴
- 팀 소개&채용: hire.md
- 개발팀에 문의하기: contact.md
- 검색: search.md

## 포스팅 작성법
1. 포스팅은 마크다운 문법으로 작성합니다.  
예) index.md 파일을 작성후 `jekyll serve` 실행시 `_site` 폴더 밑에 index.html이 생성됩니다.
   
2. 옵션값 ([참고](https://github.com/daviddarnes/alembic#page-and-post-options/))
![posting-options.png](/assets/images/readme/posting-options.png)
- title: 브라우저 탭에 노출되는 제목을 설정합니다.  
- feature_image: 포스팅 최상단에 노출될 이미지를 설정합니다. 
- feature_text: feature_image의 가운데에 노출될 텍스트를 지정할 수 있습니다.
- aside: 포스팅 오른쪽에 블로그 소개글을 노출할지 정합니다. (true: 노출, false: 비노출)

## 블로그 환경 설정 방법
### font 수정
- _config.xml 내 fonts 수정  
  ![font-setting-1.png](/assets/images/readme/font-setting-1.png)  
- _sass/_settings.scss 내 $bodytype, $headingtype 수정  
  ![font-setting-2.png](/assets/images/readme/font-setting-2.png)

### 유용한 Assets
1. Alembic 테마 사용법 : markdown/how-to-use-alembic-theme.md 참고
2. 마크업 예제, 코드 스니펫, 이메일 폼, 지도, 비디오, 이미지 예시: markdown/elements.md 참고
3. 엘리먼트: markdown/elements.md

## 기타
###  블로그 생성 도구
본 블로그는 [Jekyll](https://jekyllrb.com/) 과 [GitHub Pages](https://pages.github.com/) 기반으로 동작합니다. 

### 블로그 테마
[Alembic](https://github.com/daviddarnes/alembic/)