# Obsidian 설정

Obsidian 볼트의 `.obsidian/` 설정 중 **기기 간 공유할 항목만** 담은 저장소입니다.
노트 본문과 플러그인 데이터는 포함하지 않습니다.

## 구성

| 항목 | 내용 |
|---|---|
| `appearance.json` | 활성 스니펫 목록, 기본 글자 크기, 라이트/다크 모드, 강조색 |
| `snippets/*.css` | CSS 스니펫 |
| `app.json`, `core-plugins.json` | 기본 동작·코어 플러그인 설정 |

## 다른 PC에 적용하기

1. 이 저장소를 클론하거나 ZIP으로 내려받습니다.
2. **Obsidian을 완전히 종료합니다.** (실행 중에 복사하면 앱이 메모리에 있는 기존 설정으로 덮어씁니다)
3. 대상 볼트에 파일을 복사합니다.
   - `snippets/*.css` → `<볼트>/.obsidian/snippets/`
   - `appearance.json` → `<볼트>/.obsidian/`
4. Obsidian을 다시 실행합니다.

`appearance.json`을 덮어쓰고 싶지 않다면(기기별로 글자 크기 등을 다르게 쓰는 경우), CSS 파일만 복사한 뒤 **설정 → 모양 → CSS 스니펫**에서 아래 항목을 직접 켜면 됩니다.

```
iterm2-interface
headings-github
github-style
bullet-list-live-preview-highlight-active
bullet-list-live-preview-highlight-hover
bullet-list-live-preview-threading-active
bullet-list-live-preview-threading-hover
bullet_threading
```

## 스니펫 구분

### 직접 작성 (이 볼트 전용)

- **`github-style.css`** — 본문을 GitHub 마크다운 스타일로 렌더링. 폰트·코드블록·테이블·인용문·링크 스타일 포함.
  색상 변수는 `.workspace-leaf-content[data-type="markdown"]`로 스코프를 한정해 사이드바·버튼 등 앱 UI를 침범하지 않습니다.
- **`headings-github.css`** — h1~h6 크기를 본문 글자 크기 대비 +1px씩 선형 증가(`calc(1em + Npx)`). 본문 크기를 바꿔도 비율이 유지됩니다.
- **`iterm2-interface.css`** — 사이드바·탭바·상태바 등 UI를 iTerm2 터미널 톤으로. 라이트/다크 팔레트 분리, 사이드바 글자 크기·줄 간격 조정, 파일 탐색기 폴더 아이콘(GitHub Octicon), 선택된 파일이 들어 있는 폴더 강조 포함.

### 외부에서 받은 스니펫

`bullet-list-live-preview-*.css` (리스트 계층 하이라이트·연결선), `bullet_threading.css`, `CSS.Banners.css`, `MCL *.css`, `betterexportpdf.css`, `obsidian.css`

## 알아둘 점

- **`appearance.json`은 Obsidian이 실행 중일 때 앱이 수시로 덮어씁니다.** 저장소 내용과 로컬이 어긋나면 앱을 종료한 상태에서 복사하세요.
- CSS 변수를 `calc(var(--x) + n)`처럼 **자기 자신을 참조하는 형태로 쓰면 순환 참조로 무효 처리**되어 적용되지 않습니다. 크기 조정은 절대값으로 지정해야 합니다.
- 사이드바 글자 크기는 `--font-ui-small`이 아니라 **`--nav-item-size`** 가 결정합니다. 행 높이의 대부분은 `line-height`(기본 1.3)가 차지하며, 폴더 행은 `--nav-item-parent-padding`을 따로 사용합니다.
