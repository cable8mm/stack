- [서비스와 스토어 중복 회원](#서비스와-스토어-중복-회원)
  - [지능형 위젯](#지능형-위젯)
- [서비스만 회원](#서비스만-회원)

## 서비스와 스토어 중복 회원

서비스와 스토어 시퀀스 다이어그램:

```mermaid
sequenceDiagram
    participant C as 서비스
    participant User as 서비스 회원
    participant S as 스토어
    User->>+C: 회원가입
    Note left of C: 전화번호 and 이메일 저장
    C->>-User: 제품&카트 서비스 제공
    User->>+S: 회원가입
    Note right of S: 전화번호 and 이메일 저장
    S->>+C: 전화번호 & 이메일 전송
    Note left of C: 회원간 매칭
    C->>-User: 지능형 위젯 노출
    Note over C,S: 상품 분류 기준으로 주기적 소비 파악
    loop Every day
        S-->C: 동기화 후 지능형 위젯 스케쥴링
        C->>User: 지능형 위젯 갱신
    end
```

### 지능형 위젯

- 정기적인 소비가 일어나는 상품이나 소비가 일어날 필요가 있는 상품을 미리 연산 후 추천.
- 특정 고객에게 확실한 소비가 일어날 가능성이 있는 상품의 프로모션 쿠폰을 전달.

| 채널       | 설명                                     | 단점                          |
| ---------- | ---------------------------------------- | ----------------------------- |
| 아웃바운드 | 리모트 노티피케이션, 이메일, SMS, 알림톡 | 수신 여부를 확실히 알 수 없음 |
| 인바운드   | 서비스 1탭 두번째 혹은 세번째 섹션       | 위젯 공간을 놓칠 수 있음      |

미래 소비 상품**군** 예측:

```mermaid
sequenceDiagram
    participant C as 서비스
    participant User as 서비스 회원
    C->>User: 대중소형견 사료&간식 추천
    C->>User: 견종 패드 추천
```

미래 소비 상품**군** 프로모션:

```mermaid
sequenceDiagram
    participant C as 서비스
    participant User as 서비스 회원
    C->>User: 대중소형견 사료 할인전(예상 소비 기간 대부 2~3분기 지점)
    C->>User: 견종 패드 할인전(예상 소비 기간 대부 2~3분기 지점)
```

## 서비스만 회원

서비스 시퀀스 다이어그램:

```mermaid
sequenceDiagram
    participant C as 서비스
    participant User as 서비스 회원
    participant S as 스토어
    User->>+C: 회원가입
    Note left of C: 전화번호 and 이메일 저장
    C-->>+S: 프로모션 요청
    S->>-User: 견종 데이터 수집용 프로모션 3가지
    User->>+C: 응모
    Note left of C: 회원간 매칭
    C->>-User: 지능형 위젯 노출
    Note over C,S: 사료, 간식, 패드 등으로 주기적 소비 파악
    loop Every day
        S-->C: 동기화 후 지능형 위젯 스케쥴링
        C->>User: 지능형 위젯 갱신
    end
```

아후 프로세스는 `서비스와 스토어 중복 회원`과 같음
