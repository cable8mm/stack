# svn 저장소를 git으로 이전하기

svn 저장소가 source forge 혹은 자사 서버에 업로드 되어 있다면 github에서 제공하는 마이그레이션 툴로 한번에 변환이 가능합니다. 반면, 로컬에 저장소가 있을 경우 git 으로 변환할 수도 있는데요, 그 방법을 간략히 소개합니다.

우선, svn과 git 과의 차이가 하나 있는데요, git 의 계정엔 이메일 주소가 반드시 필요하지만 svn은 그렇지 않다는 사실만 알아두면 좋습니다.

### 필요한 소프트웨어

svn의 저장소를 git으로 변환하기 위한 툴을 설치합니다.

```sh
brew install git-svn
```

### 이전하기

svn 서버가 없고 dump 파일이 있다면 로컬에 `svnadmin`을 띄운 후 svn 서버에 dump 파일을 로드합니다.

```sh
svnadmin load [저장소 path] < [dump 파일]
```

저장소가 준비되었다면, 체크아웃을 합니다.

```sh
svn co <저장소 주소> <체크아웃 path>

cd <체크아웃 path>
```

그 후에 svn 계정을 git에서 필요한 이메일 계정으로 변경하기 위한 파일을 만듭니다.

```sh
svn log -q | grep -e '^r' | awk 'BEGIN { FS = "|" } ; { print $2" = "$2 }' | sed 's/^[ \t]*//' | sort | uniq > authors.txt

# svn_accout = svn_account 을 아래와 같이 변경합니다.
# svn_account = git <git@github.com>
```

위의 커맨드를 실행하면 authors.txt에 svn 계정 리스트가 담기는데요, 우측을 주석과 같이 이메일 계정으로 변경합니다.

여기까지 되었다면 svn에서 git으로 cloning 합니다.

```sh
git svn clone -s [체크아웃 주소] [클로닝 path] —authors-file [authors.txt 파일 절대 경로]authors.txt
```

### 마무리

이 내용에 대한 가장 정확한 정보는 깃헙에서 제공하는 문서입니다.

[Importing a Subversion repository](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/importing-a-subversion-repository)

소스만을 복사해서 git으로 만들면 이전의 커밋 리스트가 삭제되므로 되도록이면 이력까지 가져오는 것이 좋습니다.

개발자 입장에서 svn은 git에 비해서 서버가 반드시 필요하다는 단점이 있으나, 만약 기업이라면 소스를 관리할 수 있기 때문에 반드시 git을 써야되는 것은 아닙니다.

하지만, 현대 대부분의 개발 도구들이 svn을 지원하지 않고 있기 때문에 더 이상 기업 입장에서도 git을 이용하지 않으면 생산성 저하를 겪을 수 밖에 없겠죠.

이런 이슈가 없다면, git 기반의 도구를 사용하는 것이 베스트 입니다.
