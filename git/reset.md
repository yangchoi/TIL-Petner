
참고 : https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Reset-%EB%AA%85%ED%99%95%ED%9E%88-%EC%95%8C%EA%B3%A0-%EA%B0%80%EA%B8%B0


### git reset 
- 트리 : 파일의 묶음 ( 자료구조의 트리가 아님 ) 
- git은 일반적으로 세가지 트리를 관리하는 시스템 
- HEAD : 마지막 커밋 스냅샷, 다음 커밋의 부모 커밋
- Index : 다음에 커밋할 스냅샷
- 워킹 디렉토리 : 샌드박스 


#### HEAD 
- 현재 브랜치를 가리키는 포인터 
- 브랜치에 담긴 커밋 중 가장 마지막 커밋 
- 지금의 HEAD를 가리키는 커밋은 바로 다음 커밋의 부모가 됨 

##### HEAD가 가리키는 스냅샷 살펴보기 
- HEAD 스냅샷의 디렉토리 리스팅과 각 파일의 SHA-1 체크섬 보여주는 에제 

```cmd 
$ git cat-file -p HEAD
tree cfda3bf379e4f8dba8717dee55aab78aef7f4daf
author Scott Chacon  1301511835 -0700
committer Scott Chacon  1301511835 -0700

initial commit

$ git ls-tree -r HEAD
100644 blob a906cb2a4a904a152...   README
100644 blob 8f94139338f9404f2...   Rakefile
040000 tree 99f1a6d12cb4b6f19...   lib
```

- cat-file, ls-tree 명령은 일상적으로 잘 사용하지 않는 저수준 명령 ( plumbing ) 
- git 이 실제로 무슨 일을 하는지 볼 때 유용 

#### Index 
- 바로 다음에 커밋할 것들 ( Staging Area ) 
- Staging Area : 사용자가 git commit 명령 실행시 git 이 처리할 것들이 있는 곳 
- index 는 워킹 디렉토리에서 마지막으로 checkout 한 브랜치의 파일 목록과 파일 내용으로 채워짐 
- 이후 파일 변경 작업을 하고 변경한 내용으로 index 업데이트 할 수 있음 
- 이렇게 업데이트하고 git commit 명령 실행시 index 는 새 커밋으로 변경됨 

```cmd
$ git ls-files -s
100644 a906cb2a4a904a152e80877d4088654daad0c859 0	README
100644 8f94139338f9404f26296befa88755fc2598c289 0	Rakefile
100644 47c6340d6459e05787f644c2447d2595f5d3a54b 0	lib/simplegit.rb

```
- 또 다른 저수준 git ls-files 명령은 훨씬 더 장막 뒤에 가려져 있는 명령으로 실행시 현재 index가 어떤 상태인지 확인 가능 
- index 는 엄밀히 말하면 트리구조가 아님


#### 워킹 디렉토리 
- 위의 두 트리는 파일, 내용들을 효율적 형태로 .git 디렉토리에 저장함. 하지만 사람이 알아보기 어려움
- 워킹 디렉토리는 실제 파일로 존재 
- 바로 눈에 보이기 때문에 사용자가 편집하기 수월함 
- 샌드박스로 생각 
- 커밋하기 전에는 index(staging area)에 올려놓고 얼마든지 변경 가능 

```cmd
$ tree
.
├── README
├── Rakefile
└── lib
    └── simplegit.rb

1 directory, 3 files
```
#### 워크플로 
- git 의 주목적은 프로젝트의 스냅샷을 지속적으로 저장하는 것 
- 트리 세개를 이요해 더 나은 상태로 관리함 

![image](https://user-images.githubusercontent.com/48708746/111997165-1b87bf80-8b5e-11eb-83e4-c563dfb16266.png)

_____ 시각화 _____

- 파일이 하나있는 디렉토리로 이동 ( v1 , 파란색 )
- git init 명령 실행시 git 저장소 생성. HEAD는 아직 없는 브랜치 가리킴 (master 아직 없음) 

![image](https://user-images.githubusercontent.com/48708746/111997320-47a34080-8b5e-11eb-9f7c-7718f707a4b9.png)


![image](https://user-images.githubusercontent.com/48708746/111997371-54279900-8b5e-11eb-863b-6408f33c5b9b.png)

- 이 시점에서는 워킹 디렉토리 트리에만 데이터 있음
- 파일 커밋 시작 
- git add 명령으로 워킹 디렉토리 내용을 index로 복사 

![image](https://user-images.githubusercontent.com/48708746/111997498-70c3d100-8b5e-11eb-95b3-e2fab21eca7c.png)


- git commit 명령 실행 
- index 내용을 스냅샷으로 영구하게 저장하고 해당 스냅샷을 가리키는 커밋 객체 생성 
- 그러곤 master가 그 커밋 객체 가리키도록 함 

![image](https://user-images.githubusercontent.com/48708746/111997665-9cdf5200-8b5e-11eb-9ef8-a596984569be.png)


- 이때 git status 명령 실행시 변경사항이 없다고 나옴 > 세 트리 모두 같기 
