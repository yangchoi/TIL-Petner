## Active Storage

### Active Storage? 
- Active Storage 는 Amazon S3, Google Cloud Storage, Microsoft Azure Storage와 같은 클라우드 저장소에 파일을 업로드 하거나, <br>
해당 파일들을 Active Record 객체로 Attaching 할 수 있게 해줌
<br>

#### setup
- Active Storage 는 데이터베이스에서 active_storage_blobs, active_storage_attachments 라는 이름으로 두개의 테이블로 존재함
- 새 애플리케이션을 만들거나 레일즈를 5.2로 버전업 한 뒤에 이 테이블들을 만들기 위해서 bin/rails active_storage:install 을 실행해 마이그레이트 해주어야함

> active_storage_attachments 는 polymorphic join table로 model의 클래스 이름을 저장함 <br>
  만약 모델 이름이 바뀐다면 해당 테이블을 마이그레이트 해주어야하고, record_type으로 되어 있는 모델 클래스 명을 변경해주어야함 
  

### Attaching files to records 
1. has_one_attached
레코드들과 파일 간의 one-to-one 매핑을 해주는 매크로 <br>
한 레코드 당 한 파일이 attach 됨

2. has_many_attached
레코드들과 파일들 간의 one-to-many 매핑을 해주는 매크로 <br>


#### rails sync:assets 는 나는 권한이 없어서 못한다. 다른 권한있는 사람이 하면 됨
#### rails sync:db 시에는 local의 모든 것을 꺼야 실행됨.(db 포함)
