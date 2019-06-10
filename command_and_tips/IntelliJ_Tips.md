## IntelliJ Tips

### 1. Terminal, Console에서 한글 출력
IntelliJ 실행 시 VM에 인코딩 옵션을 줘야 한다.

#### Windows의 경우
idea64.exe.vmoptions에 아래 내용 추가  
<pre>-Dfile.encoding=utf-8</pre>

#### OSX의 경우
Applications/IntelliJ IDEA.app을 "패키지 내용 보기"한 후 Contents/bin/idea.vmoptions에 아래 내용 추가  
<pre>-Dfile.encoding=utf-8</pre>

#### WAS(Tomcat) Log 출력 시 한글이 깨지는 경우
Tomcat 설정에서 vm option에 <pre>-Dfile.encoding=utf-8</pre> 추가

### 2. *.properties 에서 한글 처리
Preference > Editor > File Encodings 의 Properties Files 블럭에서 ``Transparent native-to-ascii conversion``을 체크한다.
