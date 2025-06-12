---
description: 커넥션 사이즈가 적절하지 않을 경우, 적절한 풀 사이즈
---

# DB 개선 ③ - 커넥션 사이즈 조절

## 커넥션 사이즈가 적절하지 않을 경우

↓ 커넥션 풀의 사이즈가 너무 <mark style="background-color:blue;">**작을**</mark> 경우 **→** 부족한 연결로 인해 대기 시간 증가

↑ 커넥션 풀의 사이즈가 너무 <mark style="background-color:blue;">**클**</mark> 경우 **→** 과부하로 인해 성능 저하 가능성

## 적절한 풀 사이즈

1. CPU 코어 개수와 디스크 I/O 성능을 고려한 HikariCP 공식

* Optimal Pool Size = ((Core Count \* 2) + Effective Spindle Count)
  * Core Count : 애플리케이션 서버의 CPU 코어 수
  * Effective Spindle Count: 데이터베이스 스토리지의 디스크(또는 SSD) 개수



2. TPS를 고려한 계산 방식

*   Optimal Pool Size = ![](https://latex.codecogs.com/svg.image?\frac{\text{Target%20TPS}%20\times%20\text{Average%20DB%20Response%20Time%20\(s\)\}}{1%20-%20\text{DB%20Server%20Utilization\}})

    * Target TPS : 목표하는 초당 트랜잭션 수
    * Average DB Response Time : 데이터베이스 응답 시간(초 단위)
    * DB Server Utilization : 현재 DB 서버의 활용률(0\~1 사이의 값, 예 : 0.7 **→** 70% 활용 중)



> 📚 참고: 『개발자 기술 면접 노트』 – 이남희 지음
