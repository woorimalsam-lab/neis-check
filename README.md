# neis-check — 학교생활기록부 점검 도구

나이스(NEIS) 입력 전 맞춤법·글자 수·금지어·유사도를 자율 점검하는 웹 도구입니다.
`index.html` 파일을 브라우저에서 열기만 하면 동작합니다(별도 설치/서버 불필요).

## 학생 명단 (개인정보 보호)

개인정보 보호를 위해 **학생 명단은 코드에 포함되어 있지 않습니다.** 명단은 사용자가 직접
업로드하며, 업로드한 명단은 서버로 전송되지 않고 **해당 브라우저(localStorage)에만 저장**됩니다.

### 사용 방법
1. 상단 헤더의 **📤 명단 불러오기** 버튼을 클릭합니다.
2. 명단 파일을 선택합니다(여러 개를 한 번에 선택 가능).
   - **학생 명단**: 학년 → 학생 배열 형태의 `.json`
   - **교과별 명단**: 학년 → 과목 → 학생 배열 형태의 `.json` 또는 `const SUBJECT_ROSTERS = {...};` 형태의 `.js`
3. 불러오면 자동으로 화면이 새로고침되며 학년/반/학생 선택에 명단이 채워집니다.

### 명단 파일 형식

**학생 명단** (`student_rosters.json`)
```json
{
  "2": [
    { "number": 1, "name": "홍길동", "class": 1, "grade": 2 },
    { "number": 2, "name": "김철수", "class": 1, "grade": 2 }
  ]
}
```

**교과별 명단** (`subject_rosters.js` 또는 `.json`)
```js
const SUBJECT_ROSTERS = {
  "2": {
    "생명과학(3)": [
      { "number": "4", "name": "홍길동", "class": "1" }
    ]
  }
};
```
> `.js` 파일은 `const ... = { ... };` 형태여도 되고, `.json` 파일이면 `{ ... }` 객체만 있어도 됩니다.

### 명단 삭제
브라우저 개발자도구 콘솔에서 다음을 실행하거나 사이트 데이터를 지우면 명단이 삭제됩니다.
```js
localStorage.removeItem("roster_students_data");
localStorage.removeItem("roster_subjects_data");
```
