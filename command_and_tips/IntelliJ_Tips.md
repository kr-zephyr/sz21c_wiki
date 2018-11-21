## IntelliJ Tips

### 1. Terminal, Console에서 한글 출력
IntelliJ 실행 시 VM에 인코딩 옵션을 줘야 한다.

#### Windows의 경우
idea64.exe.vmoptions에 아래 내용 추가  
-Dfile.encoding=utf-8

#### OSX의 경우
Applications/IntelliJ IDEA.app을 "패키지 내용 보기"한 후 Contents/bin/idea.vmoptions에 아래 내용 추가  
-Dfile.encoding=utf-8

Tomcat 설정에서 vm option에 -Dfile.encoding=utf-8 추가