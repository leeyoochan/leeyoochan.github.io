# CLAUDE.md

## 사이트 목적

2026-2027 academic job market용 개인 학술 홈페이지. 채용위원회(faculty search committee)가 주요 타겟 독자.

## 기술 스택

- Jekyll + al-folio 테마
- GitHub Pages (gh-pages 브랜치로 배포)
- SCSS: `_sass/_variables.scss`, `_sass/_themes.scss`, `_sass/_base.scss`

## 배포

```bash
bin/deploy
```
- master에서 빌드 → gh-pages 브랜치로 push
- 커밋되지 않은 변경사항이 있으면 실패함 → 먼저 commit 필요
- interactive prompt 있음 → `echo "y" | bin/deploy`로 자동화 가능

## 주요 파일 구조

| 파일 | 용도 |
|------|------|
| `_pages/about.md` | 메인 페이지 (bio, research interests, job market alert, news, selected papers, talks, social) |
| `_pages/publications.md` | 논문 목록 + Talks 섹션 |
| `_pages/cv.md` | CV 페이지 (PDF embed) |
| `_bibliography/papers.bib` | 논문 데이터 (jekyll-scholar) |
| `_data/talks.yml` | 발표 데이터 |
| `_data/cv.yml` | CV 데이터 |
| `_config.yml` | 사이트 설정 |
| `_layouts/about.html` | 메인 페이지 레이아웃 |
| `_includes/talks.html` | Talks 렌더링 템플릿 |

## 논문 관리 (`_bibliography/papers.bib`)

- `selected = {true}` → 메인 페이지 "Selected publications"에 표시
- `abbr={S&P}` → 학회 배지 표시
- `bibtex_show={true}` → BibTeX 복사 버튼 표시
- `note = {To appear}` → camera-ready 전 논문에 사용. camera-ready 완료 시 `pdf={}` 추가하고 `note` 제거
- `pdf={filename.pdf}` → `assets/pdf/` 디렉토리에 파일 배치

## Talks 관리 (`_data/talks.yml`)

```yaml
- title: "Talk Title"
  venue: Conference Name 2026
  year: 2026
  location: "City, Country"
  category: academic    # academic 또는 industry (섹션 분리됨)
  type: invited         # invited면 배지 표시, 생략 가능
```

- `category: academic` → "Academic" 섹션 (상단)
- `category: industry` → "Industry" 섹션 (하단)
- 각 섹션 내에서 year 기준 내림차순 정렬

## 테마 컬러

- 라이트 모드: `$purple-color` (#2D3A8C, navy-indigo)
- 다크 모드: `$cyan-color` (#7B8FE0, light indigo)
- `_themes.scss`가 이 변수를 참조하므로 `_variables.scss`만 수정하면 반영됨

## News 추가

`_news/` 디렉토리에 마크다운 파일 추가:

```markdown
---
layout: post
date: 2026-03-17
inline: true
---
News content here.
```

## 주의사항

- `.gitignore`: `_site/`, `.jekyll-cache/`, `CV/` 무시됨
- ImageMagick 미설치 경고는 무시 가능 (WebP 최적화용, 사이트 동작에 영향 없음)
- 한국어로 소통
