---
#layout:post
#title: "None"
date: 2023-05-04
description: "None"
categories: blog
tags:
- writing
- None
---
oreilly 어떻게 했는지 모르겠는데 일단 로그인하고 비밀번호 바꿔서 됨

깃허브 : jekyll v3.9.3 로컬은 v4.3.2(최신)

나중에 다시 설치할때를 대비해서
1. jekyll new . 로 프로젝트 생성
2. 테마 복붙, 중복되는거는 다 대치
3. 수정수정
	```
	config.yml에
	plugins:
	  - jekyll-include-cache
	
	gemfile에
	gem 'jekyll-include-cache'
  - 
4. bundle build 로 파일 설치
5. bundle exec jekyll serve (아마 안될거임)
6. bundle add webrick
7. bundle exec jekyll serve


error
Address already in use - bind(2) for 127.0.0.1:4000 (Errno::EADDRINUSE)
```bash
lsof -i tcp:4000

kill -9 PID

//or

bundle exec puma -C config/puma.rb -b tcp://127.0.0.1:4000
```

This bears some explanation these days, as systems programming is unfamiliar to most working programmers. Yet it underlies everything we do.

resource-constrained 

constant width : 고정폭

parallel programming : 병렬 프로그래밍

flawed : 금이간

Behavior, upon use of a nonportable or erroneous program construct or of erroneous data, for which this International Standard imposes no requirements

1.  터미널에서 repository local 폴더로 이동
2.  find . -name .DS_Store -print0 | xargs -0 git rm --ignore-unmatch -f 
3.  echo .DS_Store >> .gitignore  
4.  git commit -m "Del  .DS_Store"
`
!exclamation mark  
"double quote, double quotation mark  
#hash, number, pound  
$dollar  
%percent  
&ampersand  
'single quote, apostrophe  
()paren, parenthesis, round brackets  
-hyphen, minus, dash, bar  
=equal  
^caret, hat, up arrow  
~tilde  
\yen  
|pipe, vertical bar

@at mark  
`back quote  
[]brackets, square brackets  
{}braces, curly brackets

;semicolon  
+plus  
:colon  
*asterisk, star

,comma  
.dot, period, point  
<>angle brackets  
/slash  
?question mark  
\backslash  
_underscore, underbar, underline

`
common sense : 상식
