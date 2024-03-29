# 🌏  Spring boot와 Java를 활용하여 Account(계좌 관리) 시스템을 만드는 프로젝트 과제 
- Account(계좌) 시스템은 사용자와 계좌의 정보를 저장하고 있으며, 외부 시스템에서 거래를 요청할 경우 거래 정보를 받아서 계좌에서 잔액을 거래금액만큼 줄이거나(결제), 거래금액만큼 늘리는(결제 취소) 거래 관리 기능을 제공하는 시스템입니다.
- 구현의 편의를 위해 사용자 생성 등의 관리는 API로 제공하지 않고 프로젝트 시작 시 자동으로 데이터가 입력되도록 하며, 계좌 추가/해지/확인, 거래 생성/거래 취소/거래 확인의 6가지 API를 제공합니다.

# 📕 프로젝트 소개
### ✅ 계좌 관련 API
1) 계좌 생성
a. 파라미터 : 사용자 아이디, 초기 잔액
b. 결과
i. 실패 : 사용자 없는 경우, 계좌가 10개(사용자당 최대 보유 가능 계좌) 인 경우 실패 응답
ii. 성공
- 계좌번호는 10자리 랜덤 숫자
- 응답정보 : 사용자 아이디, 생성된 계좌 번호, 등록일시(LocalDateTime)

[ 계좌생성 시 주의사항 ]
- 계좌 생성 시 계좌 번호는 10자리의 정수로 구성되며, 기존에 동일 계좌 번호가 있는지 중복체크를 해야 한다.
- 기본적으로 계좌번호는 순차 증가 방식으로 생성한다. (응용하는 방식으로는 계좌 번호를 랜덤 숫자 10자리로 구성하는 것도 가능하며, 랜덤생성이 현업과 더욱 유사하니 참고해주세요.)

2) 계좌 해지
a. 파라미터 : 사용자 아이디, 계좌 번호
b. 결과
i. 실패 : 사용자 없는 경우, 사용자 아이디와 계좌 소유주가 다른 경우, 계좌가 이미 해지 상태인 경우, 잔액이 있는 경우 실패 응답
ii. 성공
- 응답 : 사용자 아이디, 계좌번호, 해지일시

3) 계좌 확인
a. 파라미터 : 사용자 아이디
b. 결과
i. 실패 : 사용자 없는 경우 실패 응답
ii. 성공
- 응답 : (계좌번호, 잔액) 정보를 Json list 형식으로 응답

### ✅ 거래(Transaction) 관련 API
1) 잔액 사용
a. 파라미터 : 사용자 아이디, 계좌 번호, 거래 금액
b. 결과
i. 실패 : 사용자 없는 경우, 사용자 아이디와 계좌 소유주가 다른 경우, 계좌가 이미 해지 상태인 경우, 거래금액이 잔액보다 큰 경우, 거래금액이 너무 작거나 큰 경우 실패 응답
ii. 성공
- 응답 : 계좌번호, transaction_result, transaction_id, 거래금액, 거래일시

2) 잔액 사용 취소
a. 파라미터 : transaction_id, 계좌번호, 거래금액
b. 결과
i. 실패 : 원거래 금액과 취소 금액이 다른 경우, 트랜잭션이 해당 계좌의 거래가 아닌경우 실패 응답
ii. 성공
- 응답 : 계좌번호, transaction_result, transaction_id, 취소 거래금액, 거래일시

3) 거래 확인
a. 파라미터 : transaction_id
b. 결과
i. 실패 : 해당 transaction_id 없는 경우 실패 응답
ii. 성공
- 응답 : 계좌번호, 거래종류(잔액 사용, 잔액 사용 취소), transaction_result, transaction_id, 거래금액, 거래일시
- 성공거래 뿐 아니라 실패한 거래도 거래 확인할 수 있도록 합니다.
  
# 📕 개발 기간
23.12.27 ~ 24.01.01

## 🖥️ 개발 환경
- 언어 : Java
- 프로그램 : IntelliJ IDEA(Ultimate)
- JDK 17

### 💪 아쉬운 점(느낀 점)
- 개인사정 때문에 시간이 너무 없어서 제대로 못한게 너무 아쉽다. 
  과제 요구사항이 내가 이해하고 만든게 맞나 살짝 헷갈린다.
  다음 과제가 끝나면 다시 제대로 해볼 예정이다.
