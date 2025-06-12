# HTTP란 무엇인가?

**HTTP(HyperText Transfer Protocol)**&#xB294; 웹에서 **클라이언트(브라우저)**&#xC640; **서버** 간의 데이터를 주고받기 위한 <mark style="background-color:blue;">**애플리케이션 계층 프로토콜**</mark>입니다.

#### 🔹 특징

* **Stateless**: 요청과 응답이 각각 독립적으로 처리됨 (세션 유지 불가)
* **Request/Response 구조**: GET, POST, PUT, DELETE 등의 메서드 사용
* **Port 80 사용 (HTTPS는 443번)**

#### 🔹 HTTP와 HTTPS 차이

| 구분    | HTTP                 | HTTPS                 |
| ----- | -------------------- | --------------------- |
| 보안    | 없음                   | SSL/TLS 암호화 적용        |
| 포트    | 80                   | 443                   |
| 사용 예시 | `http://example.com` | `https://example.com` |
