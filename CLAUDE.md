# 작업 정책 (Claude memory)

## 1. Figma `visible=false` 레이어는 절대 코드로 구현하지 않는다
- 카드/컴포넌트를 코드화하기 전, **모든 자손 노드의 `visible` 속성을 점검**한다.
- `visible=false`인 자식은 마크업·CSS·SVG `<symbol>` 어디에도 남기지 않는다.
- 적용 대상 예시 (이 repo 기준):
  - 859:28311 Likelist의 `Comments`, `Bookmark` 그룹
  - Like/Share 그룹 안의 카운트 텍스트(`2`, `3`)
  - 카드 우하단 `의견 보내기` 텍스트
  - 카드의 `DROP_SHADOW` effect (effect.visible=false)
- **검사 시점**: 새 카드/컴포넌트 추출 전 1회, 그리고 변경 후 push 전 1회.

## 2. 배포 흐름
1. Figma 변경/요청을 코드에 반영
2. `python3 -m http.server` 로 로컬 미리보기 띄우기
3. **사용자에게 로컬 링크 공유 후 검수 대기**
4. 사용자 OK 후에만 `git push` (main → GitHub Pages)
5. 검수 전에 자체 판단으로 push 금지
