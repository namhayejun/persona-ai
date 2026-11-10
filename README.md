# Persona OS UI

로그인 없는 정적 채팅 UI입니다. 코드 / 생각 / 팩트 3개 모드를 탭으로 전환합니다.
파일은 `index.html` 하나이고, 빌드 과정이 없습니다.

## GitHub에 올리기
1. GitHub에서 새 저장소(예: `persona-os`)를 만듭니다.
2. `index.html`과 `README.md`를 저장소 맨 위(루트)에 올립니다.

## Cloudflare Pages로 배포하기
1. Cloudflare 대시보드 → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. 위에서 만든 GitHub 저장소를 선택합니다.
3. 빌드 설정:
   - Framework preset: **None**
   - Build command: (비워 둠)
   - Build output directory: `/`
4. **Save and Deploy**를 누르면 `https://<프로젝트이름>.pages.dev` 주소가 생깁니다.
   이후 GitHub에 push할 때마다 자동으로 다시 배포됩니다.

## 모델 서버 연결하기 (나중에)
`index.html` 위쪽의 `API_URL`을 모델 서버 주소로 바꿉니다. 비워 두면 데모 모드입니다.

요청 (POST, JSON):
```json
{ "mode": "code | think | fact",
  "messages": [ { "role": "user", "content": "..." } ] }
```
응답:
```json
{ "answer": "최종 답변", "thinking": "추론 과정 (think 모드일 때만, 선택)" }
```

> Cloudflare Pages는 화면(HTML)만 호스팅합니다. Gemma 모델은 GPU가 있는 별도 서버에서 돌려야 하고,
> 그 서버가 위 형식으로 응답하도록 만들어야 합니다. 서버는 CORS에서 Pages 주소를 허용해야 합니다.
