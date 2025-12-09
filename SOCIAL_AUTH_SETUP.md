# 소셜 로그인 API 설정 가이드

이 문서는 Google, Kakao, Naver 소셜 로그인 API를 설정하는 방법을 안내합니다.

## 1. Google OAuth 설정

### 1.1 Google Cloud Console 설정
1. [Google Cloud Console](https://console.cloud.google.com/)에 접속
2. 새 프로젝트 생성 또는 기존 프로젝트 선택
3. "API 및 서비스" > "사용자 인증 정보"로 이동
4. "사용자 인증 정보 만들기" > "OAuth 클라이언트 ID" 선택
5. 애플리케이션 유형: "웹 애플리케이션" 선택
6. 승인된 자바스크립트 원본에 도메인 추가 (예: `http://localhost:3000`)
7. 승인된 리디렉션 URI에 콜백 URL 추가
8. 생성된 Client ID를 복사

### 1.2 코드에 적용
`social-auth.js` 파일의 `SOCIAL_CONFIG` 객체에서 다음을 수정:
```javascript
google: {
    clientId: '여기에_Google_Client_ID_입력',
    scope: 'profile email'
}
```

## 2. Kakao OAuth 설정

### 2.1 Kakao Developers 설정
1. [Kakao Developers](https://developers.kakao.com/)에 접속
2. 내 애플리케이션 > 애플리케이션 추가하기
3. 앱 이름, 사업자명 입력 후 생성
4. "앱 키" 메뉴에서 JavaScript 키 복사
5. "플랫폼" 메뉴에서 Web 플랫폼 등록
   - 사이트 도메인: `http://localhost:3000` (개발용)
   - 사이트 도메인: 실제 도메인 (운영용)
6. "카카오 로그인" > "활성화 설정" ON
7. "Redirect URI" 등록: `http://localhost:3000/login.html` (개발용)

### 2.2 코드에 적용
`social-auth.js` 파일의 `SOCIAL_CONFIG` 객체에서 다음을 수정:
```javascript
kakao: {
    jsKey: '여기에_Kakao_JavaScript_Key_입력',
    redirectUri: window.location.origin + '/login.html'
}
```

## 3. Naver OAuth 설정

### 3.1 Naver Developers 설정
1. [Naver Developers](https://developers.naver.com/)에 접속
2. "Application" > "애플리케이션 등록"
3. 애플리케이션 이름, 사용 API 선택 (네이버 로그인 필수)
4. 서비스 URL: `http://localhost:3000` (개발용)
5. Callback URL: `http://localhost:3000/login.html` (개발용)
6. 생성된 Client ID와 Client Secret 복사

### 3.2 코드에 적용
`social-auth.js` 파일의 `SOCIAL_CONFIG` 객체에서 다음을 수정:
```javascript
naver: {
    clientId: '여기에_Naver_Client_ID_입력',
    callbackUrl: window.location.origin + '/login.html'
}
```

## 4. 보안 주의사항

⚠️ **중요**: 실제 프로덕션 환경에서는:
1. API 키를 환경 변수나 서버 사이드에서 관리
2. 클라이언트 ID만 프론트엔드에 노출 (Secret은 절대 노출 금지)
3. HTTPS 사용 필수
4. CORS 설정 확인
5. 리디렉션 URI 검증

## 5. 테스트 방법

1. 각 소셜 로그인 버튼 클릭
2. 팝업 창에서 로그인 진행
3. 로그인 성공 시 마이페이지로 리디렉션 확인
4. 브라우저 콘솔에서 로그 확인

## 6. 문제 해결

### Google 로그인 오류
- Client ID가 올바른지 확인
- 승인된 자바스크립트 원본에 도메인이 등록되어 있는지 확인
- Google API가 활성화되어 있는지 확인

### Kakao 로그인 오류
- JavaScript 키가 올바른지 확인
- 플랫폼에 Web이 등록되어 있는지 확인
- Redirect URI가 정확히 일치하는지 확인

### Naver 로그인 오류
- Client ID가 올바른지 확인
- Callback URL이 정확히 일치하는지 확인
- 서비스 URL이 등록되어 있는지 확인

