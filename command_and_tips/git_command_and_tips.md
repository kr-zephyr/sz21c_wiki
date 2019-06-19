## git 명령어들

- git pull origin {{branch name}}
	- 현재 로컬 branch에 remote의 지정된 branch를 pull 받는다.
	- remote의 branch를 checkout 받고, 로컬의 branch와 merge하는 것과 같은 효과를 보이려나?
	- origin master는 pull할 수 없다.

- git push origin {{branch name}}
	- 로컬에서 생성한 branch를 remote로 올린다.
	- 만약 remote에 해당 branch가 없으면 생성된다.