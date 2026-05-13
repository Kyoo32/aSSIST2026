# Starbucks Online App ERD

이 문서는 `Starbucks Online App 분석 통합 프로젝트`의 기준 스키마를 정리한 ERD입니다.
분석 대상은 내부 운영 분석가이며, 핵심 질문은 `노출 -> 클릭 -> 주문` 퍼널과 메뉴/카테고리별 매출 성과입니다.

## Mermaid ERD

```mermaid
erDiagram
    USERS ||--o{ VIEW_IMP_LOGS : sees
    USERS ||--o{ CLICK_LOGS : clicks
    USERS ||--o{ ORDERS : places
    MENUS ||--o{ VIEW_IMP_LOGS : appears_in
    MENUS ||--o{ CLICK_LOGS : clicked_for
    MENUS ||--o{ ORDER_ITEMS : ordered_as
    ORDERS ||--|{ ORDER_ITEMS : contains

    USERS {
        int user_id PK
        string user_name
        string age_band
        string gender
        string membership_tier
        string preferred_channel
        string signup_month
        timestamp created_at
    }

    MENUS {
        int menu_id PK
        string menu_name
        string category
        string subcategory
        string temperature
        numeric price
        boolean is_seasonal
        boolean is_limited
    }

    VIEW_IMP_LOGS {
        bigint view_id PK
        int user_id FK
        int menu_id FK
        string session_id
        timestamp event_ts
        string surface
        string device_type
        int position_rank
    }

    CLICK_LOGS {
        bigint click_id PK
        int user_id FK
        int menu_id FK
        string session_id
        timestamp event_ts
        string surface
        string device_type
        string action_type
    }

    ORDERS {
        bigint order_id PK
        int user_id FK
        string session_id
        timestamp order_ts
        string order_status
        string channel
        string store_type
        numeric total_amount
    }

    ORDER_ITEMS {
        bigint order_item_id PK
        bigint order_id FK
        int menu_id FK
        int quantity
        numeric unit_price
        numeric line_amount
    }
```

## 테이블 역할

- `users`: 사용자 프로필과 세그먼트 분석의 기준 테이블
- `menus`: 메뉴 마스터. 카테고리, 가격, 시즌성 같은 속성을 보관
- `view_imp_logs`: 앱 화면에서 메뉴가 노출된 로그
- `click_logs`: 메뉴 카드/배너/추천 영역에서 클릭한 로그
- `orders`: 주문 단위 헤더. 한 주문의 총액과 상태를 담음
- `order_items`: 주문 상세 라인. 어떤 메뉴가 몇 개 팔렸는지 담음

## 핵심 KPI 연결

- `노출 수`: `view_imp_logs`
- `클릭 수`: `click_logs`
- `CTR`: `clicks / impressions`
- `주문 전환`: `orders / clicks`
- `매출`: `orders.total_amount`, `order_items.line_amount`
- `재주문 패턴`: `orders`를 사용자 기준으로 시계열 집계

## 설계 메모

- `orders`와 `order_items`를 분리해 한 주문에 여러 메뉴가 들어가는 현실적인 구조를 유지합니다.
- `session_id`를 `view_imp_logs`, `click_logs`, `orders`에 같이 넣어 퍼널을 교육용으로 추적하기 쉽게 만듭니다.
- 모든 테이블/컬럼은 노트북에서 `COMMENT ON`으로 설명을 붙여 Text-to-SQL 정확도를 높입니다.
