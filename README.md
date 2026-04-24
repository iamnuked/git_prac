# git_prac

팀 협업 대비 Git / GitHub 사용 연습 저장소입니다.

## 목표

이 저장소에서는 4명이 함께 아래 흐름을 연습합니다.

1. 저장소 clone
2. 각자 branch 생성
3. 파일 수정 후 commit / push
4. Pull Request 생성 및 merge
5. 같은 줄을 수정해서 conflict 발생
6. conflict 직접 해결 후 다시 push

## 권장 역할

- A: 기준 브랜치 정리 담당
- B: 기능 1 담당
- C: 기능 2 담당
- D: 리뷰 및 conflict 해결 보조 담당

역할은 고정일 필요는 없고, 한 번씩 돌아가며 맡아보는 것을 추천합니다.

## 기본 규칙

- 기본 브랜치는 `main` 사용
- 작업 전 항상 `git pull origin main`
- 기능 작업은 반드시 새 브랜치에서 진행
- 브랜치 이름 예시
  - `feature/member-a`
  - `feature/member-b`
  - `feature/member-c`
  - `feature/member-d`

## 1차 실습: 브랜치와 PR 익히기

각 팀원은 아래 순서로 진행합니다.

```bash
git clone <repo-url>
cd git_prac
git checkout -b feature/member-a
```

`README.md` 아래에 자기 소개 한 줄을 추가합니다.

예시:

```md
## 팀원 소개

- A: 백엔드에 관심이 있습니다.
```

작업 후 commit / push:

```bash
git add README.md
git commit -m "docs: add member A intro"
git push origin feature/member-a
```

그 다음 GitHub에서 Pull Request를 만들고 merge합니다.

모든 팀원이 한 번씩 PR을 만들어보면 1차 실습 완료입니다.

## 2차 실습: 일부러 conflict 내보기

이번에는 모두가 `README.md`의 같은 줄을 수정해서 충돌을 일부러 만듭니다.

아래 섹션을 사용하세요.

```md
## 오늘의 목표

우리는 GitHub 협업을 연습합니다.
```

### 진행 순서

1. A가 `main`에서 문장을 먼저 수정하고 merge합니다.
2. B, C, D는 A가 merge되기 전에 같은 줄을 각자 다른 문장으로 수정합니다.
3. B, C, D가 나중에 `main`을 pull 하거나 merge하려고 하면 conflict가 발생합니다.

예시로 각자 이렇게 바꿔보세요.

- A: 우리는 GitHub 협업과 PR 리뷰를 연습합니다.
- B: 우리는 GitHub 협업과 merge conflict 해결을 연습합니다.
- C: 우리는 GitHub 협업과 branch 전략을 연습합니다.
- D: 우리는 GitHub 협업과 코드 리뷰 문화를 연습합니다.

## conflict 해결 실습

예를 들어 B 브랜치에서 conflict가 났다면:

```bash
git checkout feature/member-b
git pull origin main
```

또는:

```bash
git fetch origin
git merge origin/main
```

conflict가 나면 `README.md`에 아래처럼 표시됩니다.

```md
<<<<<<< HEAD
우리는 GitHub 협업과 merge conflict 해결을 연습합니다.
=======
우리는 GitHub 협업과 PR 리뷰를 연습합니다.
>>>>>>> main
```

Nick
### 해결 방법 


1. `<<<<<<<`, `=======`, `>>>>>>>` 표시를 찾습니다.
2. 어떤 내용을 남길지 팀원끼리 합의합니다.
3. 표시 문자를 모두 지우고 최종 문장만 남깁니다.

예시:

```md
우리는 GitHub 협업, PR 리뷰, conflict 해결을 함께 연습합니다.
```

그 다음 아래 순서로 마무리합니다.

```bash
git add README.md
git commit -m "fix: resolve merge conflict in README"
git push origin feature/member-b
```

## 자주 헷갈리는 포인트

- `pull`은 보통 `fetch + merge`입니다.
- conflict는 실패가 아니라 협업 중 자연스럽게 생기는 상황입니다.
- conflict가 났을 때 중요한 것은 "누가 맞는가"보다 "최종 내용을 어떻게 합칠까"입니다.
- 해결 후에는 반드시 `git add`를 다시 해야 합니다.
- conflict 해결 후 push가 안 되면 현재 브랜치를 다시 확인하세요.

## 추천 실습 순서

1. 4명 모두 clone
2. 각자 branch 생성
3. 자기 소개 추가 후 PR 생성
4. 1명씩 merge
5. 같은 줄 수정으로 conflict 유도
6. 각자 conflict 해결
7. 마지막으로 서로의 PR 리뷰 코멘트 남기기

## 추가 미션

- 한 명은 `rebase` 방식으로 `main`을 반영해보기
- 한 명은 `merge` 방식으로 `main`을 반영해보기
- 둘의 히스토리 차이를 `git log --oneline --graph --all`로 비교해보기

## 체크리스트

- branch를 직접 만들 수 있다
- commit / push를 할 수 있다
- PR을 열고 merge할 수 있다
- conflict 표시를 읽을 수 있다
- conflict를 수정하고 다시 commit 할 수 있다
- 팀원 변경 사항을 내 작업과 안전하게 합칠 수 있다
