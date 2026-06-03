# 사용자용 릴리스 노트 작성 규칙

이 디렉토리(`./release/release_notes/`)는 **사용자에게 자연어로 설명하는** 버전별 릴리스 노트를 관리합니다.

> 버전별 노트 **색인(최신순 표)**은 repo 루트 [`../README.md`](../README.md)에서 관리합니다.
> 색인은 `.claude/scripts/gen_release_notes_index.py`가 이 디렉토리를 스캔해 자동 생성합니다.

## 개발자 기술 일지(`Project/dev_notes/`)와의 구분

| 구분 | 위치 | 대상 독자 | 내용 성격 |
| --- | --- | --- | --- |
| 개발자 기술 일지 | `Project/dev_notes/vX.Y.Z.md` | 개발자 | 리비전(_rNNN) 이력, 기술 구현 세부, 함수/파일명 등 |
| 사용자 릴리스 노트 | `./release/release_notes/vX.Y.Z.md` | 일반 사용자 | 자연어 기능 설명, 개선/버그픽스 요약, 사용 방법 중심 |

## 파일 구조

- 위치: `./release/release_notes/vX.Y.Z.md`
- 파일명: 앱 버전을 그대로 사용 (예: `v1.0.47.md`)
- git 추적 대상 (`./release/` repo에 커밋됨 — EXE/ZIP과 달리 `.gitignore` 제외 대상 아님)

## 작성 시점

- 새 버전 EXE 빌드 완료 후 작성
- 작성 후 `./release/` repo에 커밋 + push (메인 개발 repo와 독립)
- 소급 마이그레이션: 신규 릴리스(v1.0.47+)부터 바로 이 디렉토리에 작성
- 노트 작성 후 `python .claude/scripts/gen_release_notes_index.py`를 실행해 루트 README 색인을 갱신

## 필수 포함 항목

```markdown
# JP's Codeless Macro Tool vX.Y.Z 업데이트

출시일: YYYY-MM-DD

## 새로운 기능
- (기능 설명, 비기술 자연어)

## 개선 사항
- (성능/UX 개선)

## 버그 수정
- (수정된 문제)

## 설치 및 다운로드
최신 버전 다운로드: https://plcman.tistory.com/209
```

## blog-release-writer 연동

`blog-release-writer` 에이전트가 티스토리 Step 2 패치노트 새 글(버전별 신규 글)을 작성할 때
이 디렉토리의 `vX.Y.Z.md`를 1차 소스로 사용합니다.

- **글 제목 형식**: `[릴리즈] JP's Codeless Macro Tool vX.Y.Z 패치노트`
- **본문 하단 고정 링크**: 최신 버전 다운로드 -> https://plcman.tistory.com/209
- **발행 후**: `./release/version.json`의 `notes_url`을 새 글 URL로 갱신
