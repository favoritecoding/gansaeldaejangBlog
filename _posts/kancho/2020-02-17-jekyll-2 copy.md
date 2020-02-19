---
layout: post
title:  "jekyll-3. jekyll 로컬 개발환경 셋팅"
date:   2020-02-18T13:00:52-05:00
author: kancho
categories: kancho
tags:	[jekyll, github Pages]
cover:  "/assets/instacode.png"
---

## jekyll 로컬 개발환경 셋팅의 필요성
* 매번 수정된 코드를 확인 하기 위해 github에 git push를 하면 배포가 되기까지는 시간이 걸립니다. (빨리 반영될때도 있지만 그렇지 않은 경우도 있습니다.)
   개인이 운영하는 블로그일 경우에는 git push하여 수정된 코드를 배포하며 확인 할 수 있지만, 좋코는 팀블로그여서 그렇게 했다가는 충돌이 날겁니다.
   충돌을 방지하고 실시간으로 확인하기위해서 로컬 개발환경을 셋팅합니다. 팀원들은 각자의 PC에서 코드를 수정하고 확인하며, 완성된 코드를 git push 하기로했습니다.

<br/>

- - -

<br/>

## 루비 설치
  
keyll를 사용하기 위해서는 루비가 필요합니다.
루비를 설치하도록 하겠습니다. (window 64bit 운영체제 기준)

[루비 다운로드 링크][ruby-download] : https://rubyinstaller.org/downloads/


<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-1.PNG" | relative_url }}' alt='absolute'>

<br/>

<br/>

 
다운로드된 파일을 실행시켜 설치를 합니다 (계속 Next를 누릅니다.)

설치가 완료된 파일은 윈도우키를 눌러 확인 할 수 있습니다. 

<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-1-2.PNG" | relative_url }}' alt='absolute'>
 
<br/>

<br/>


Start Command Prompt with Ruby를 실행시키고 설치된 ruby의 버전을 확인해보겠습니다

{% highlight html %}
ruby -v
{% endhighlight %}

<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-2.PNG" | relative_url }}' alt='absolute'>


## Prompt를 UTF-8로 인코딩 

ruby가 제대로 설치 되었다면 Start Command Prompt with Ruby 창을 UTF-8로 인코딩 해주는 설정을 하겠습니다.
(설정을 안할시 명령어가 제대로 실행이 안됩니다.)

{% highlight html %}
chcp 65001
{% endhighlight %}

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-5.PNG" | relative_url }}' alt='absolute'>

<br/>

<br/>


## jekyll 설치

인코딩 설정이 완료되면 jekyll를 설치하도록 하겠습니다.
<br/>

{% highlight html %}
gem install jekyll bundler
{% endhighlight %}

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-3.PNG" | relative_url }}' alt='absolute'> 

<br/>

<br/>



jekyll의 설치가 잘 되었는지 확인해보도록 하겠습니다.
<br/>

{% highlight html %}
jekyll -v
{% endhighlight %}

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-4.PNG" | relative_url }}' alt='absolute'> 

<br/>

<br/>

## jekyll 실행하기


일단 prompt창에서 내 블로그파일의 경로까지 이동합니다.
<br/>

#### 이동을 위한 간단한 명령어 정리
{% highlight html %}
cd / 			    : c드라이브로 이동
dir 			    : 현재 내가 위치한 디렉토리의 하위 폴더 목록을 볼 수 있음
cd 하위폴더명      	 : 해당 폴더로 이동
{% endhighlight %}

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-4-1.PNG" | relative_url }}' alt='absolute'>

위의 이미지는 제 PC에 블로그 파일이있는 경로입니다.


<br/>

<br/>
  

번들(플러그인)을 설치를 하도록하겠습니다.
아래 명령어를 입력하면 설치가 시작됩니다. 

{% highlight html %}
bundle install
{% endhighlight %}

<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-10.PNG" | relative_url }}' alt='absolute'>


만약 bundle install시 충돌이 날 경우에는 플러그인 전체 삭제 명령어를 실행한 후 다시 bundle install를 해주시면됩니다.

설치된 플러그인 전체 삭제 명령어

{% highlight html %}
gem uninstall -alx
{% endhighlight %}

<br/>

<br/>

번들 설치가 완료되면 로컬에서 서버를 실행하도록 하겠습니다

{% highlight html %}
 bundle exec jekyll serve
{% endhighlight %}

<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-13.PNG" | relative_url }}' alt='absolute'> 

<br/>

ERROR가 뜹니다! ERROR가 뜨는 이유는 _config.yml에서 url과 baseurl에 git page 주소와 연결되어 있기 때문입니다.
일단 작업을 중지시키고 ERROR를 잡도록 하겠습니다. 컨트롤키와 C를 함께 눌러주면 작업이 중지됩니다(ctrl-c)
<br/>
ERROR를 잡기위해 _config.yml에서 url과 baseurl를 수정해줍니다.
아래의 사진처럼 개발을 할때는 개발 usl과 baseurl의 주석을 풀어주고 배포용 url과 baserul을 주석처리해줍니다.
(*git에 push를 할때는 반대로 배포용의 주석을 풀고 개발은 주석처리를 해주셔야합니다!)

<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-14.PNG" | relative_url }}' alt='absolute'> 

<br/>

다시 bundle exec jekyll serve 명령어를 입력해주면 아까와는 다르게 ERROR가 안뜨는걸 볼 수 있습니다.
아래 이미지의 빨간색 박스를 보면 접속주소를 알려줍니다.
<br/>

<img data-action="zoom" src='{{ "/assets/kanchoImg/jekyll/2-15.PNG" | relative_url }}' alt='absolute'> 

<br/>

http://127.0.0.1:4000/ 를 인터넷 주소창에 쳤을때 화면이 제대로 나오면 로컬 개발환경 셋팅은 끝난겁니다!

<br/>

<br/>

<br/>





[ruby-download]:    https://rubyinstaller.org/downloads/