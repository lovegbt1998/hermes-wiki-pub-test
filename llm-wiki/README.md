# LLM Wiki (프로젝트 지식 베이스)

이 프로젝트의 개발 과정에서 생긴 지식을 축적하는 저장소.
단순 문서함이 아니라 **Issue·PR·코드변경·결정·리뷰를 LLM 에이전트가 읽고 구조화해 유지**하는 지식 베이스다.
Hermes 협업 에이전트가 `project-bootstrap` 으로 이 프로젝트를 만들 때 함께 시딩된다.

## 구조

```text
llm-wiki/
  README.md               ← 이 파일
  _templates/
    wiki-page-template.md  ← wiki/*.md 작성 표준 구조
  raw/                     ← 원본 자료(가공 전)
    issues/ pull-requests/ meetings/ decisions/ reviews/ logs/
  wiki/                    ← LLM이 사람용으로 정리한 지식 (이 폴더만 GitHub Wiki로 발행)
    Home.md · Change-Log.md · Decision-Records.md · Issue-Summary.md · (프로젝트가 커지면 PRD·Architecture… 추가)
```

| 위치 | 성격 |
|---|---|
| `raw/` | Issue/PR 원문·리뷰·결정 등 **원본 그대로** |
| `wiki/` | 사람이 읽기 좋게 **정리된 문서** — GitHub Wiki로 발행 |

## 갱신 규약
- `wiki/*.md` 는 `_templates/wiki-page-template.md` 구조를 따른다.
- **PR merge 후** `Change-Log.md`(변경 이력), 중요 결정은 `Decision-Records.md`, 이슈 완료는 `Issue-Summary.md` 를 갱신.
- 새 산출물(PRD·아키텍처·API 명세·DB 스키마·테스트 등)이 생기면 템플릿으로 해당 `wiki/<Doc>.md` 를 추가.

## GitHub Wiki 발행
- `main` 에 `llm-wiki/wiki/**` 변경이 push 되면 `.github/workflows/publish-wiki.yml` 이 저장소 Wiki 탭으로 자동 발행.
- ⚠️ **무료 플랜 + 비공개 저장소는 Wiki 탭을 사용할 수 없다**(GitHub 제약). 이 경우 발행 워크플로는 조용히 건너뛰고
  지식은 **이 폴더(in-repo llm-wiki)** 로만 유지된다. Wiki 탭이 필요하면 저장소 공개 전환 또는 GitHub Pro 필요.
