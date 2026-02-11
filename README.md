# Where should we go?

이 저장소는 단일 `index.html` 파일로 구성된 Firebase Firestore 기반 여행 투표 웹앱입니다.

## 현재 코드 상태 요약
- 포함된 SDK: Firebase App, Firestore (`firebase-app-compat.js`, `firebase-firestore-compat.js`)
- 미포함 SDK: Firebase Auth (`firebase-auth-compat.js`)
- 투표 중복 제어: `localStorage` 키(`voted_item`, `voted_month`) 기반

## 왜 "배포본에는 구글 로그인 있었던 것 같은데"가 발생할 수 있나?
다음 중 하나일 가능성이 큽니다.
1. 다른 브랜치/다른 리포지토리에 인증 코드가 있음
2. 배포 시점에 로컬 미커밋 파일을 사용함
3. Firebase Hosting 타깃/프로젝트를 다르게 배포함

## 복구 체크리스트
1. `firebase.json`, `.firebaserc` 존재 여부 확인
2. Git 히스토리에서 Auth 키워드 검색
   - `firebase-auth-compat.js`
   - `GoogleAuthProvider`
   - `signInWithPopup`
   - `onAuthStateChanged`
3. Hosting에 실제 업로드된 정적 파일 원본을 내려받아 현재 `index.html`과 diff
4. Auth 기능 재도입 시 최소 구현
   - Auth SDK 추가
   - Google Provider 로그인 버튼
   - 로그인 상태 UI
   - `uid` 기반 사용자별 투표 문서 구조로 1인 1표 보장

## 다음 권장 작업
- Firestore Rules에 인증 기반 쓰기 제한을 설정
- 클라이언트 localStorage 제어 대신 서버 규칙/문서 모델로 무결성 보장
