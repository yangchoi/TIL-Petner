
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


- 이때 git status 명령 실행시 변경사항이 없다고 나옴 > 세 트리 모두 같기 때문 
- 다시 파일 내용 내용 바꾸고 커밋하면 어떻게 될까
- 먼저 워킹 디렉토리 파일고침
- 파일 v2

![image](https://user-images.githubusercontent.com/48708746/111998567-7b329a80-8b5f-11eb-8536-2a247ecc8e15.png)

- 이때 git status 실행시 Changes not staged for commit 
- index 와 워킹 디렉토리가 다른 내용 담고 있기 때문 
- git add로 변경사항을 index 로 올려줌 

![image](https://user-images.githubusercontent.com/48708746/111998696-a0270d80-8b5f-11eb-95d3-1b8574f08d06.png)

- 여기서 git status 사용시 Changes to commited 
- index 와 HEAD의 다른 파일들이 여기에 표시됨 
- 즉, 다음 커밋할 것과 지금의 마지막 커밋이 다르다는 말 
- git commit 으로 커밋함

![image](https://user-images.githubusercontent.com/48708746/111998894-cea4e880-8b5f-11eb-8741-42ff61501b2f.png)

- 여기서 git status 실행시 아무것도 출력 안됨 
- 세개의 트리가 같아졌기 때문 
- 브랜치 변경이나 clone 명령도 내부에서는 비슷한 절차
- 브랜치를 checkout 하면 HEAD가 새로운 브랜치 가리키도록 바ㅜ끼고 새로운 커밋 스냅샷을 index 에 놓음 
- 그리고 index 내용을 워킹 디렉토리로 복사함 


### Reset 역할
- 예를 들어 file.txt 파일 하나를 수정하고 커밋
- 이를 세번 반복시에 히스토리는 아래와 같이 됨 

![image](https://user-images.githubusercontent.com/48708746/112001718-8f2bcb80-8b62-11eb-9699-9fed282f7149.png)


- reset 명령은 이 세 트리를 간단하고 예측가능한 방법으로 조작함 
- 트리 조작 동작은 세 단계 이하로 이루어짐 


### 1단계 : HEAD 이동 
- reset 명령이 하는 첫번째 일은 HEAD 브랜치 이동시킴 
- checkout 명령처럼 HEAD 가 가리키는 브랜치를 바꾸지 않음 
- HEAD는 계속 현재 브랜치 가리키고 있고 현재 브랜치가 가리키는 커밋을 바꿈 
- HEAD가 master 브랜치를 가리키고 있다면 git reset 9e5e6a4 명령은 master 브랜치가 9e5e6a4를 가리키게 만듦 

![image](https://user-images.githubusercontent.com/48708746/112002182-f9dd0700-8b62-11eb-976d-66d7c00bd6cf.png)

- reset 명령에 커밋 넘기고 실행하면 언제나 이런 작업 수행
- reset --soft 옵션 사용시 여기까지 진행하고 동작 멈춤

- reset 명령은 가장 최근의 git commit 명령 되돌림
- git commit 명령 실행 시 git은 새로운 커밋 생성하고 HEAD가 가리키는 브랜치가 새로운 커밋을 가리키도록 업뎃함 
- reset 명령 뒤에 HEAD~(HEAD 부모커밋) 주면 index나 워킹 디렉토리는 그대로 두고 브랜치가 가리키는 커밋만 이전으로 되돌림 
- index를 업뎃한 다음에 git commit 명령 실행시 git commit --ammed 명령의 결과와 같아짐

### 2단계 : index 업데이트(--mixed)
- 여기서 git status 실행 시 index와 reset 명령으로 이동시킨 HEAD의 다른 점이 녹색으로 출력됨
- reset 명령은 여기서 한발짝 더 나아가 index를 현재 HEAD가 가리키는 스냅샷으로 업뎃 가능

![image](https://user-images.githubusercontent.com/48708746/112002740-90112d00-8b63-11eb-98e5-c0e1f8696b40.png)

- --mixed 옵션주고 실행시 reset 명령은 여기까지 하고 멈춤 
- reset 명령 실행시 아무 옵션 주지 않으면 기본적으로 --mixed 옵션으로 동작

- 가리키는 대상을 가장 최근의 커밋으로 되돌리는 것은 같음
- 그러고 나서 staging area를 비우기까지 함
- git commit 명령도 되돌리고 git add 명령까지 되돌리는 것 


### 3단계 : 워킹 디렉토리 업데이트(--hard)
- --hard 옵션 사용시 reset 명령은 이 단계까지 수행 


![image](https://user-images.githubusercontent.com/48708746/112002992-d070ab00-8b63-11eb-9ee1-dafc5165b54a.png)

- reset 명령통해 git add, git commit 명령으로 생성한 마지막 커밋 되돌리고 워킹 디렉토리 내용까지도 되돌림
- --hard 는 reset 명령을 위험하게 만드는 유일한 옵션
- git 에는 실제로 데이터를 삭제하는 방법이 별로 없으나 이 방법이 그 중 하나
- reset 을 사용해서 간단히 결과를 되돌릴 수 있지만 --hard 옵션은 그렇지 않음
- 이 옵션 사용시 워킹 디렉토리의 파일까지 강제로 덮어 씀
- 본 예제 파일은 v3 버전을 아직 git 이 커밋으로 보관하고 있기 때문에 reflog 이용해 다시 복원할 수 있음
- 만약 커밋한 적 없다면 git이 덮어쓴 데이터는 복원 불가 







