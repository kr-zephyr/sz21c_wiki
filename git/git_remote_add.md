# Remote Repository에 Local Repository 연결하기
- Remote에 Repository를 생성한다.
	- 로컬에서 workspace를 만들어 .gitignore 등을 만드는 경우 충돌나지 않도록 Remote에서 Repository 생성 시 제외시켜야 한다.
- Local Repository에 .gitignore를 만든다.
	- stage에 올라가면 안되는 확장자, 경로등을 미리 정리해 둔다.
- Local Repository를 생성한다.
	- git 초기화 수행
	- bare(--bare 옵션)로 생성 시 work tree가 생성되지 않으므로 바로 git repository를 활성화하려면 bare로 생성하지 않는다.
```
git init
```
- Remote Repository를 연결한다.
```
git remote add origin {Remote Repository 경로-url}
```
- Remote Repository에 push한다.
	- 미리 Local Repository에 commit된 내용이 있어야 한다.
```
git push origin master
```

