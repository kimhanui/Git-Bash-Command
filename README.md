## 목록
- status(상태)
- branch
- pull
- push
- fetch
- merge
- remote
- stash
- 로컬 저장소 git으로 만들기
- 그래프로 보고싶을 때

## status
```$ git status``` git 을 사용하면서 안정감을 느끼게 해주는 명령어
 - git 관리하의 파일들 중 어떤 변경사항이 있는지 알려줌.
 
## branch
```$ git branch``` 브랜치 목록 조회   
```$ git branch -r``` 원격 브랜치 목록 조회
```$ git checkout develop``` develop브랜치**로** 체크아웃
> 체크아웃하면 '아웃'이라 나간다고 착각하는데 그 브랜치로 입주하는거임  

```$ git checkout -b develop``` develop브랜치 생성하면서 체크아웃
```$ git branch -d feature/1``` feature/1브랜치 삭제

## pull
```$ git pull origin develop``` origin의 develop브랜치에서 최신정보를 받아옴.  

## push
```$ git push origin feature/1``` 원격 브랜치(feature/1)에 푸시  

## fetch
```$ git fetch origin develop``` origin의 develop에서 최신정보를 가져만 옴. **브랜치에 적용x**   
적용하려면 ```$ git merge origin/develop```

### pull과 다른점?
내부적으로 보면 pull = fetch + merge임.   
따라서 remote repo에서 가져온 최신정보를 내 브랜치에 바로 적용시키려면 pull,   
안정성을 위해 merge는 미루려면 fetch.

## merge ~머지가 머지?의 그 머지다~
feature/1브랜치를 develop로 병합
```
$ git checkout develop
$ git merge feature/1
```
### merge conflict란?
브랜치 A와 B를 merge하는 도중 merge conflict가 뜰 수 있다.
이는 같은 파일의 같은 부분을 다르게 수정했을 때 발생함.
  - 파일이 다르면 무조건 자동으로 합쳐준다.
  - 파일이 같아도 수정한 부분이 다르다면 자동으로 합쳐준다. (버전관리를 사용하는 정말 중요한 이유중의 하나)
개발자가 직접 충돌하는 부분을 찾아가 둘 중 어떤쪽을 반영할지 판단하고 직접 수정해야됨.
  
  
  - 어떻게 알고 찾아감? ```$ git status```로 변경된 파일목록을 보고 직접찾아간다. 
  - 어느부분인 줄 알고 고침? conflict가 일어나는 부분에는 표식이 남아있다.(아래 참고)
    > intellij 처럼 버전관리툴을 지원하는 툴에선 ui가 이쁘게 되어있으니 몇번의 클릭으로 details까지 한눈에 알 수 있다.
    
    ![image](https://user-images.githubusercontent.com/30483337/72628262-4c37fc00-3991-11ea-9c3e-3304e8cabb84.png)

예를들어  
브랜치A - main.class
```
...
46줄 | public void method1(int a){
47줄 |  a=5;
48줄 |         }
```
브랜치B - main.class
```
...
46줄 | public void METHOD1(int a){
47줄 |  a=3;
48줄 | }
```
conflict 표식. 둘 중 한쪽을 적용한다.
```
<<<<<<< HEAD              # 현재 checkout 한 브랜치 A의 상태
46줄 | public void METHOD1(int a){
47줄 |  a=3;
48줄 | }  
=======                   # 구분자 ====================
46줄 | public void METHOD1(int a){
47줄 |  a=3;
48줄 | }      
>>>>>>> B         # 병합하려는 대상인 B 브랜치의 상태
```

## remote  
```$ git remote``` 현재 리포지토리에 연결된 원격저장소 조회(이름만 나옴)    
```$ git remote -v``` 이름 + 주소까지 조회  
```$ git remote add upstream 주소```원격저장소 이름 upstream으로 추가  
```$ git push origin work``` **브랜치 없으면 추가** & push   

## stash
```$ git stash``` 스태시  
```$ git stash list``` 스태시 리스트 조회   
```$ git stash pop``` 마지막 스태시 복원, 목록에서 제거   

## 로컬 저장소 git으로 만들기 
```$ git init```   
```$ git add .``` 변경사항 stage에 올려놓기   
```$ git commit -m 'initial commit'``` 커밋메시지 입력(-m) 후 커밋   
까지 했을 때 **디렉토리에 관리대상이 생겼으므로** 버전관리 시작.   

## 다른 원격 저장소를 로컬 저장소에 가져오기(위와 동일x)
```$ git init``` (후 아무것도 커밋하지 않고 백지상태에서 가져와야한다.)  
```$ git remote add origin ~~``` 원격 저장소 등록  
```$ git pull origin master``` 원격저장소의 master 브랜치 적용.  
```$ git branch develop``` master브랜치에서 develop 생성  
```$ git pull origin develop``` 원격저장소의 develop 브랜치 적용.   
까지 하고 내 브랜치 만들어 작업시작...

## 그래프로 보고싶을 때
```$ git log --branches --graph --decorate --oneline```   


## 참고링크
https://kwonnam.pe.kr/wiki/git/cheatsheet   
https://git-scm.com/book/ko/v2   
