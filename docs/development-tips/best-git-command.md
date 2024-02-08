# 베스트 깃(Git) 커맨드

Github이 Git의 생태계를 넒혀가고 있습니다. CI/CD가 보편화 되면서 소스 저장소의 역할이 버전 관리에만 국한되지 않고, 코드의 표준화와 각종 코드의 빌드 및 배포의 핵심이 되었습니다.

따라서, 몇 명이 개발을 하던 소기업이던 대기업이던 Git을 이용하고 Github을 이용해서 협업을 하는 경우가 빠르게 늘고 있습니다. Github의 주인인 마이크로 소프트는 자사의 오픈소스 에디터인 VSCode에서 공식 확장을 이용해서 Github과의 협업을 하나의 툴로 만들어서 제공하고 있습니다.

워낙 자주 사용하는 툴이기 때문에 Git과 Github 을 통해 어떻게 개발을 하는게 베스트인지를 생각 해 봅니다.

## Github에 코드를 올리는 두가지 방법, Commit and PR

오픈소스 프로젝트의 경우 운용상의 이유로 Commit을 이용한 저장소 코드 올리기는 허용하지 않는 경우가 많습니다. 대신, PR을 만들면 각종 테스트와 리뷰, 테스트가 이루어 지고 리뷰어가 승인을 할 경우 main 브랜치에 머지 됩니다.

개발자 입장에서는 PR을 이용한 개발에 두가지 상황이 있을 수 있습니다.

1. 내가 브랜치를 만들어서 PR을 생성하는 경우
2. PR을 Pull 해서 개발을 한 후 PR에 다시 Commit 하는 경우

한가지 중요한 점은 현대 개발을 단일 Commit이 작을 수록 관리가 편해지는 경향이 생겼습니다. 그 이유는 CI/CD로 인해 빌드에 대한 모든 것이 자동화 되었기 때문입니다. 과거에는 빌드 매니저가 빌드를 하기까지 몇 주가 걸리는 경우도 있던 시절과는 전혀 다른 양상입니다.

따라서, 이 두가지 상황 모두 하루에도 몇번 씩 발생하고 있습니다. 이 경우 아래 커맨드가 도움을 줄 수 있습니다.

## 커맨드를 활용하자

### 내가 브랜치를 만들어서 PR을 생성하는 경우

브랜치를 생성하고 이동할 때 아래 세개의 커맨드를 사용합니다.

```sh
alias gc="git checkout"
alias gcb="git checkout -b"
alias gb="git branch"
alias gbclean="git branch | grep -v "main" | xargs git branch -D"
```

`hello`라는 브랜치로 예를 들어 보겠습니다.

```sh
# hello 브랜치 생성 후 이동
gcb hello

# main 브랜치로 이동
gc main

#hello 브랜치로 이동
gb hello

# PR이 머지된 후 로컬에서 main 브랜치 이외의 모든 브랜치를 삭제
gbclean
```

전 머지는 Github에서 이루어 지기 때문에 로컬에서는 위 네가지 명령어만으로 개발을 합니다.

### PR을 Pull 해서 개발을 한 후 PR에 다시 Commit 하는 경우

PR은 번호가 강조되고 브랜치 이름은 상대적으로 중요하지 않습니다. 따라서, 아래와 같은 명령어를 이용합니다.

```sh
#pull request clean
function prc()
{
    git for-each-ref refs/heads/pr/ --format='%(refname)' | while read ref ; do branch=${ref#refs/heads/} ; git branch -D $branch ; done
}

#pull request pull
function prp()
{
    if [ $# -eq 0 ]; then
        echo 'Pull request number need.'
    else
        git fetch -fu ${2:-origin} refs/pull/$1/head:pr/$1 && git checkout pr/$1
    fi
}

#delete branch
function brc()
{
    if [ $# -eq 0 ]; then
        echo 'Branch name need.'
    else
        git for-each-ref "refs/heads/**/*$1*" --format='%(refname)' | while read ref ; do branch=${ref#refs/heads/} ; git branch -D $branch ; done
    fi
}
```

이 명령어도 예를 들어 봅니다.

```sh
# 3번 PR을 pull
prp 3

# 3번 PR의 브랜치를 삭제
prc 3

# PR 브랜치에서 다시 브랜치를 만들었을 경우 브랜치 이름 매칭이 된 브랜치 전체를 삭제
brc <브랜치 이름 중 일부>
```

`git push` 이나 `git merge main`과 같은 경우는 별도의 명령어를 만들지 않고 git 명령어 그대로 사용합니다.

다음 번에는 Github에서 제공하는 여러가지 머지 방법에 대해서 이야기 해 보도록 하겠습니다.
