---
title: github에 블로그 만들기
layout: post
date: 2020-04-05
description: 
image: smile.gif
categories: ["IT"]
---


오래된(?) 인간이라 솔직히 개발은 하지만 Git은 사용을 안해봐서 잘모르는 사람인데

Github은 즐겨 이용한다

최근 티스토리가 별로 관리도 안하는 것 같고 데이터 백업도 힘든것 같아

이제는 신변잡기적은 내용은 모르지만 기술적인 내용은 다른 곳으로 옮길까 고민중에

Github에 블로그를 만들수 있다고 해서 한번 만들어 보았다


# 1. github에 가입을 한다

 이부분은 설명이 필요 없고 알아서 가입을

# 2. Repositories 를 하나 생성한다

 Repositories 이름은 [id].github.io 로 생성을 해줘야 나중에 블로그로 접속이 가능하다

# 3. Jekyll theme를 하나 골라서 업로드 한다

 http://jekyllthemes.org/

 jekyllthemes.org 에 접속해 보면 github에서 사용할 수 있는 theme들이 엄청나게 많다

 나는 그냥 

 https://github.com/sharadcodes/jekyll-theme-milo

 sharadcodes/jekyll-theme-milo

 이 테마를 사용했다

 로컬에서 Git 명령어로 세팅을 하는 방법이 있던데 git 사용법을 잘 모르는(이제 공부를...) ㅅ으로 그냥 

 테마를 다운받아 만든 [id].github.io 에 그냥 업로드를 했다


# 4. jekyll theme 설정을 한다

 업로드 된 테마에서 제일 먼저 

```
_config.yml 
```

 파일을 편집한다

```
title: "Milo"

about: "Bootstrap theme for jekyll"
markdown: kramdown
url: ""
baseurl: "/jekyll-theme-milo"
disqus_short_name: disqus-demo-page
```

 상단에 있는 이 부분을

 본인의 블로그에 맞게 수정한다

 당연히 title, about은 원하는 문구로 수정을 하고

 결정적으로

 url 은 아까 만든 [id].github.io 로 수정을 하고

 baseurl 은 "/" 로 수정한다

 
 그리고 이제 개인적으로 원하는 방향으로 커스토마이징을 한다 
```
about.md, author.md 
```
 수정하고

 https://[id].github.io 로 접속한 다음 화면을 보면서 원하는 형태로 수정을 한다

 물론
```
_layouts 
_includes
```

 에 있는 파일이나  안의 파일 내용을 자알 해석해서 수정을 한다

 개인적으로 이미지 덕지 덕지 뜨는것이 싫어서 이미지 붙는 것은 빼버렸다(text 신봉주의자)

# 5. 이제 새글을 하나 써보자

 github.com 에 접속해서 로긴을 하고 

 [id].github.io Repositories 에 들어가서 
```
_posts 
```

 에 파일을 하나 만든다 

 파일명은 yyyy-mm-dd-문서제목.md  형태이고

 문서 헤더에는 
```
---
title: 게시물 제목
layout: post
date: 2020-04-05
description: 
image: xxxx.jpg
categories: ["categories 명"]
---
```
 당연히 원하는 게시물로 값을 입력해야 한다

 이미지는 게시물을 대표하는 이미지로 img 폴더에 있는 이미지 파일명을 써주면 되지만 개인적으로 이미지 뜨는건 싫어서 이미지는 제거 했다

 이렇게 헤더를 쓴 다음 내용을 markdown 포맷으로 쭈우욱 적어주면 게시물이 완성된다

 블로그 https://[id].github.io 에 접속해 보면 새로 쓴 게시물이 보인다.....

 향후 게시물을 이렇게 써 주면된다...

