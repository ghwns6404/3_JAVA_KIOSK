# JAVA KIOSK 프로젝트 결과보고서

## 팀 구성 및 역할 분담

| 이름 | 역할 | 강점 | 약점 |
|------|------|------|------|
| 박준수 | 프로젝트 조정 및 관리, 파트 간 소통, 팀 미팅 진행 | 프로젝트 관리 | DB 접근 미숙 |
| 이성연 | PPT 제작, 발표 대본 작성, 기능 요구 정리 | 우선순위 기반 개발 전략 | 코드 충돌 처리 미숙 |
| 김기환 | 주요 코드 작성 및 문서화 | Java 이해도 높음 | 예외 처리 미흡 |
| 조재영 | 전체 코드 흐름 이해, GUI 디자인 및 버튼 구현 | 의사소통 능력 | 협업 툴 사용 미숙 |
| 천호준 | 적립금 시스템 및 옵션 기능 개발 | UI 설계 능력 | 예외 처리 미흡 |
| 주재연 | 기능 아이디어 제안, 오류 검토 | 문제 해결 능력 | UI 경험 부족 |

- 카카오톡 및 대면 회의로 매주 코드 점검 진행

---

## 프로젝트 개요

- Java 기반 키오스크 프로그램 개발
- 기존 키오스크에 로그인, 멤버쉽, 관리자 기능 확장
- 데이터는 txt 파일로 저장해 파일 기반 데이터베이스 역할 수행

### 구현 기능

### 1. 회원가입 및 로그인
- ID, 비밀번호, 이름 입력으로 회원가입
- `IDExists()`로 아이디 중복 확인
- 중복 시 `new message()`로 경고 메시지 출력
- 정상일 경우 `sign_save()` 호출해 member.txt 저장
- 관리자는 특정 ID를 사용 불가 처리 (`equalsIgnoreCase`)
- 로그인 시 `sign_read`로 파일에서 정보 읽고 검증
- 회원 정보 구성: ID / PW / 이름 / 적립금

### 2. 관리자 패널
- txt 파일 데이터를 `BufferedReader`, `FileReader`로 읽어옴
- 읽어온 데이터는 `StringBuilder`에 저장 후 관리자 화면에 출력
- 기능: 회원 정보 조회 / 수정 / 삭제 / 포인트 적립

### 3. 키오스크 UI
- Java Swing 기반 GUI
- 메뉴 배열을 기준으로 동적 버튼 생성
- 주문 내역은 `TextArea`에 표시
- 포인트 사용 여부에 따라 결제 금액 계산
- `ActionListener`로 이벤트 처리

### 4. 멤버쉽 기능
- 결제 금액의 10%를 포인트로 적립
- 회원 ID와 일치하는 줄을 찾아 포인트 업데이트
- `BufferedReader`로 파일 읽은 뒤 적립 포인트 저장

---

## 기능 우선순위

1. kioskmain  
2. join  
3. management  
4. membership  
5. UI  

## 기술 스택

- Java  
- Swing (JFrame)  
- txt 파일 저장방식  

---

## 개발 일정

- 2024-11-01 ~ 2024-12-09  
- 설계: 1주  
- 개발: 3주  
- 테스트 및 보완: 2주  

---

## 개발 환경

- IDE: Eclipse  
- OS: Windows 10  

---

## 주요 코드 흐름

### kioskmain

#### 관리자 로그인
```java
if (id.equals("admin") && pw.equals("1234")) {
    new message("관리자 로그인", "로그인 성공");
    new management();
    dispose();
    return;
}

#### 관리자 로그인
sign_read loginCheck = new sign_read();
if (loginCheck.login(id, pw)) {
    new message("회원 로그인", "로그인");
    dispose();
    runKiosk(id);
} else {
    new message("아이디 또는 비밀번호가 일치하지 않습니다.", "로그인 실패");
}

#### 회원가입 버튼
else if (e.getSource() == signUp_b) {
    new Sign_Up();
}


#### 키오스크 UI실행
UI kiosk = new UI(loggedInUserId);
kiosk.addWindowListener(new java.awt.event.WindowAdapter() {
    @Override
    public void windowClosing(java.awt.event.WindowEvent e) {
        runLogin();
    }
});


참고 자료

https://hyecoding.tistory.com/45


리스크 관리
1. 요구사항 변경 가능성

초기 요구사항 명확화

변경 발생 시 우선순위 재조정 및 일정 수정

2. 의사소통 부족

매주 진행 상황 공유 및 역할 조정

3. txt 파일 기반 회원 관리

장기적으로 빅데이터 기반 회원 관리 및 이벤트 자동화 목표