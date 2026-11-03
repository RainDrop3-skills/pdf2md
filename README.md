# pdf2md

강의자료 PDF를 한 페이지씩 빠짐없이 분석해 **페이지별 한국어 설명 md 노트**로 만드는 Claude Code 스킬입니다.

- 모든 페이지에 `## p.N` 섹션을 하나씩 씁니다. 표지나 Q&A 페이지도 빠뜨리지 않습니다.
- 영어 원문은 그대로 두고 바로 아래에 한국어 번역을 답니다.
- 그림·표·퀴즈, 흰 글씨로 숨긴 정답(`[숨은 답]`)까지 페이지 단위로 정리합니다.
- 슬라이드에 없는 보충 지식은 `[배경]`으로 구분합니다. 오픈북 시험에서 슬라이드 문구와 섞이지 않게 하기 위해서입니다.
- `--everytime` 옵션을 붙이면 같은 폴더의 에브리타임 기출 캡처와 매핑 md를 찾아 관련 페이지에 `📌 에타 Qn` 표시를 답니다.

주제별로 다시 묶은 읽기 자료(HTML)가 필요하면 [pdf2html](https://github.com/RainDrop3-skills/pdf2html)을 쓰세요.

## 설치

Claude Code 개인 스킬 폴더에 넣습니다.

```bash
# macOS / Linux / Git Bash
git clone https://github.com/RainDrop3-skills/pdf2md.git ~/.claude/skills/pdf2md
```

```powershell
# Windows PowerShell
git clone https://github.com/RainDrop3-skills/pdf2md.git "$env:USERPROFILE\.claude\skills\pdf2md"
```

필요한 것
- Python 3 (외부 패키지 설치 없음)
- poppler (`pdfinfo`, `pdftotext`, `pdftoppm`). Windows는 `winget install oschwartz10612.Poppler`

## 사용

PDF가 있는 폴더에서 Claude Code에 이렇게 말하면 됩니다.

- "4장 품질요구사항 PDF 페이지별로 정리해줘"
- "Introduction 자료 md로 풀어줘"
- "아직 설명 md 없는 PDF 전부 해줘"
- "1장 페이지별 설명 만들어줘 --everytime"

결과는 PDF와 같은 폴더에 `NN-<제목>-페이지별-설명.md`로 저장됩니다.

## 구조

| 경로 | 내용 |
|---|---|
| `SKILL.md` | 작업 절차와 출력 형식 (Claude가 읽는 지침) |
| `scripts/extract_pages.py` | PDF → 페이지별 텍스트·이미지·요약 |
| `references/everytime.md` | `--everytime` 옵션 규칙 |
| `evals/evals.json` | 스킬 평가용 프롬프트와 확인 항목 |

## 한계

- 학습 보조 자료입니다. 시험 기준은 원본 슬라이드 문구입니다.
- `evals/evals.json`이 가리키는 입력 PDF는 강의자료라 레포에 넣지 않았습니다.
