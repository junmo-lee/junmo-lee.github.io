rules
1. write daily
2. write in english as much as possible 

post에 있는 .md 파일들은 아이클라우드 동기화 시키기

현재 공부하는것과 공부할 것 첫 페이지에 적어놓기 .readme처럼

블로그를 쓰는 목적:
내가 공부한 것을 기록하기 위해서
2개로 나누어서 생각
1. 매일 쓰는 일기같은거
2. 일기들을 모아서 정리해 포스트


layout
title : 


태그 사용하기 → 메타데이터 사용
https://wormwlrm.github.io/2019/09/22/How-to-add-tags-on-Jekyll.html


마크다운 기본 문법 최대한 사용 → 옵시디언 or typora
옵시디언 : daily note나 표와 같은 여러 플러그인 사용 가능
제텔카스텐 사용가능

typora : 마크다운에 가장 충실한 기본적, 유로임..

to do list 사용, 시간까지 기록
무엇을 공부했는지 적어놓기
각 공부한 것들의 기간 적어놓기

노트 필기법 좋은거 찾아서 그것만 사용하기

이미지 애매하면 https://unsplash.com/ko


[jekyll 문서](https://jekyllrb-ko.github.io/docs/)

## 젬

젬은 루비 프로젝트에 포함시킬 수 있는 코드입니다. 기능들을 패키지화해서 다른 사람들이나 프로젝트에 공유할 수 있게 해줍니다. 젬은 다음과 같은 기능을 가질 수 있습니다:

-   루비 오브젝트를 JSON 으로 변환
-   페이지 나누기
-   GitHub 과 같은 API 와 연동
-   Jekyll 자체도 [jekyll-feed](https://github.com/jekyll/jekyll-feed) 와 [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag), [jekyll-archives](https://github.com/jekyll/jekyll-archives) 같은 Jekyll 플러그인과 마찬가지로 하나의 젬이다.

`Gemfile` 은 사이트에 필요한 젬들의 목록입니다. 단순한 Jekyll 사이트를 예로 들면 이렇게 생겼습니다:

bundler : Gemfile에 있는 젬들을 설치

[디렉토리 구조 docs](http://jekyllrb-ko.github.io/docs/structure/)
https://labs.brandi.co.kr/2018/05/14/chunbs.html

-   **1. 반드시 변경**
    -   _featured_tags/ : 카테고리 대분류 폴더
    -   _featured_categories/ : 카테고리 소분류(태그) 폴더
    -   _data/ : 개발자 및 운영자, 기타 정보 폴더 (author.yml 수정이 필요)
    -   _config.yml : 가장 중요한 환경변수 설정 파일
    -   README.md : GitHub 프로젝트 애서 소개하게 될 글
    -   favicon.ico : 블로그 접속 시 브라우저 주소창에 표시되는 대표 아이콘
    -   about.md : About 메뉴 클릭 시 나타나는 블로그에 대한 소개글
-   **2. 필요시 변경**
    -   assets/ : 이미지, CSS 등을 저장 폴더
    -   _layouts/ : 포스트를 감싸기 위한 레이아웃 정의 폴더(페이지, 구성요소 등 UI변경 시 수정)
    -   _includes/ : 재사용을 위한 기본 페이지 폴더
    -   Gemfile.lock : Gemfile에 기록한 레일 기반 라이브러리를 설치 후 기록하는 파일(중복설치 방지)
    -   Gemfile : 필요한 레일 기반 라이브러리를 자동으로 설치하고 싶을 때 명시하는 설정 파일
    -   .gitignore : GitHub에 올리고 싶지 않은 파일들은 이 파일에 경로지정 가능(예: _site 산출물, 환경설정, 개인정보, 작성중인 글 등)
    -   sitemap.xml : 테마의 사이트맵
    -   search.html : Tipue Search 설치 시, 검색결과를 출력하는 페이지로 활용
    -   robots.xml : 구글 웹로봇 등 검색엔진 수집 등에 대한 정책을 명시하는 설정파일
    -   posts.md : 포스트 작성 관련 설정파일
-   **3. 변경 필요없음(참고)**
    -   _posts/ : 포스트를 저장하는 폴더
    -   .git/ : GitHub 연동을 위한 상태정보가 담긴 폴더
    -   _site/ : Jekyll 빌드 생성 결과물 폴더(실제 GitPages에서 WEB으로 보여지는 산출물)
    -   .sass-cache/ : 레일 엔진에서 사용하는 캐시 저장폴더(변하지 않는 산출물들에 대한 파싱을 하지 않아 속도보장)
    -   _sass/ : 일종의 CSS 조각파일 저장 폴더
    -   _js/ : JavaScript 저장 폴더
    -   _plugins/ : 플로그인 저장 폴더(크롬 정책상 어차피 사용안함)
    -   LICENSE.md : 테마 개발자의 라이센스 설명
    -   index.html : 블로그 최초 접속 페이지
    -   googlea0d1f22cc8208170.html : 구글 검색엔진에 블로그를 등록하는 과정의 소유권 확인 파일
    -   feed.xml : RSS Feed 활용을 위한 XML
    -   browserconfig.xml : 윈도우8 이상 IE11 접속 시 클라이언트가 요청하는 환경설정 파일(윈도우의 표준 파괴 본능은 여기에도 숨어있다. ㅡ,.ㅡ)
    -   404.md : 404 Not Found Page(블로그에 없는 페이지 요청 시 등장하는 페이지)
    -   .eslintrc : EcmaScript Lint(자바스크립트 협업 개발을 위한 규칙 정의) 환경설정 파일
    -   .eslintignore : EcmaScript Lint 무시할 규칙 지정(전역변수 에러표시 예외처리 등)
    -   .babelrc : Babel(자바스크립트 컴파일러) 설정파일

https://theorydb.github.io/envops/2019/05/03/envops-blog-github-pages-jekyll/



테마를 골라보아요
https://github.com/poole/lanyon
켜고끄는 사이드바 하나, 깔끔함

https://github.com/poole/hyde
항상있는 사이드바

일단 사용한 테마 두개를 섞은거  https://github.com/hydecorp/hydejack 



나중에 직접 만들때 참고
https://jekyllthemes.io/theme/avenco-portfolio-jekyll-theme

노션 비슷하게 만들어보기
https://jekyllthemes.io/theme/dann-blog-jekyll-theme




[이미지와 자료 삽입 ](https://jekyllrb-ko.github.io/docs/posts/)
`... which is shown in the screenshot below: ![My helpful screenshot](/assets/screenshot.jpg)`

dependencies
$ gem install jekyll jekyll-gist jekyll-sitemap jekyll-seo-tag
https://github.com/poole/poole#usage

bundle add webrick

Gemfile에
gem 'jekyll-include-cache' 추가

_config.yml 에
plugins:
  - jekyll-include-cache
https://github.com/mmistakes/minimal-mistakes/issues/1875



github에 올리기
bundle install
bundle exec jekyll serve

-   `jekyll build` - 사이트를 빌드하고 `_site` 라는 디렉토리에 정적 사이트를 생성합니다.
-   `jekyll serve` - 위와 동일한 작업을 하지만 추가로 내용이 변경되면 사이트를 다시 빌드하고 `http://localhost:4000` 주소에 로컬 웹 서버를 구동합니다.

.md 파일은 빌드시 html로 전환
필요한 기능들은 css로



```html
<details>
<summary>제목</summary>
<div>

내용

</div>
</details>
```
<details> <summary>Short Summary</summary> <p>text to hide</p> </details>

- 1
	- 1.1
		- 1.1a
			- 1.1a1
		- 1.1b
		- 1.1c
		- 1.1d
	- 1.2
		- 1.2a
			- 1.2a1
		- 1.2b
		- 1.2c
`- 1
	- 1.1
		- 1.1a
			- 1.1a1
		- 1.1b
		- 1.1c
		- 1.1d
	- 1.2
		- 1.2a
			- 1.2a1
		- 1.2b
		- 1.2c`

Editor > Fold Indent  
(this is the one that makes this bullet points fold work)

Editor > Fold Headings  
(this one is for headings, I recommend you turn this on too)

https://forum.obsidian.md/t/how-to-toggle-like-in-the-notion/9935/7