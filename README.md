# java-convenience-store-precourse

## 🏪기능 요구 사항
구매자의 할인 혜택과 재고 상황을 고려하여 최종 결제 금액을 계산하고 안내하는 결제 시스템을 구현한다.
<ul>
<li>사용자가 입력한 상품의 가격과 수량을 기반으로 최종 결제 금액을 계산한다.
<ul><li>총구매액은 상품별 가격과 수량을 곱하여 계산하며, 프로모션 및 멤버십 할인 정책을 반영하여 최종 결제 금액을 산출한다.</li></ul></li>
<li>구매 내역과 산출한 금액 정보를 영수증으로 출력한다.</li>
<li>영수증 출력 후 추가 구매를 진행할지 또는 종료할지를 선택할 수 있다.</li>
<li>사용자가 잘못된 값을 입력할 경우 IllegalArgumentException를 발생시키고, "[ERROR]"로 시작하는 에러 메시지를 출력 후 그 부분부터 입력을 다시 받는다.
<ul><li>Exception이 아닌 IllegalArgumentException, IllegalStateException 등과 같은 명확한 유형을 처리한다.</li></ul></li>
</ul>

### 🥫재고 관리
<ul>
<li>각 상품의 재고 수량을 고려하여 결제 가능 여부를 확인한다.</li>
<li>고객이 상품을 구매할 때마다, 결제된 수량만큼 해당 상품의 재고에서 차감하여 수량을 관리한다.</li>
<li>재고를 차감함으로써 시스템은 최신 재고 상태를 유지하며, 다음 고객이 구매할 때 정확한 재고 정보를 제공한다.</li>
</ul>

### 🛍️프로모션 할인
<ul>
<li>오늘 날짜가 프로모션 기간 내에 포함된 경우에만 할인을 적용한다.</li>
<li>프로모션은 N개 구매 시 1개 무료 증정(Buy N Get 1 Free)의 형태로 진행된다.</li>
<li>1+1 또는 2+1 프로모션이 각각 지정된 상품에 적용되며, 동일 상품에 여러 프로모션이 적용되지 않는다.</li>
<li>프로모션 혜택은 프로모션 재고 내에서만 적용할 수 있다.</li>
<li>프로모션 기간 중이라면 프로모션 재고를 우선적으로 차감하며, 프로모션 재고가 부족할 경우에는 일반 재고를 사용한다.</li>
<li>프로모션 적용이 가능한 상품에 대해 고객이 해당 수량보다 적게 가져온 경우, 필요한 수량을 추가로 가져오면 혜택을 받을 수 있음을 안내한다.</li>
<li>프로모션 재고가 부족하여 일부 수량을 프로모션 혜택 없이 결제해야 하는 경우, 일부 수량에 대해 정가로 결제하게 됨을 안내한다.</li>
</ul>

### 🪪멤버십 할인
<ul>
<li>멤버십 회원은 프로모션 미적용 금액의 30%를 할인받는다.</li>
<li>프로모션 적용 후 남은 금액에 대해 멤버십 할인을 적용한다.</li>
<li>멤버십 할인의 최대 한도는 8,000원이다.</li>
</ul>

### 🧾영수증 출력
<ul>
<li>영수증은 고객의 구매 내역과 할인을 요약하여 출력한다.</li>
<li>영수증 항목은 아래와 같다.
<ul>
<li>구매 상품 내역: 구매한 상품명, 수량, 가격</li>
<li>증정 상품 내역: 프로모션에 따라 무료로 제공된 증정 상품의 목록</li>
<li>금액 정보
<ul>
<li>총구매액: 구매한 상품의 총 수량과 총 금액</li>
<li>행사할인: 프로모션에 의해 할인된 금액</li>
<li>멤버십할인: 멤버십에 의해 추가로 할인된 금액</li>
<li>내실돈: 최종 결제 금액</li>
</ul></li></ul></li>
<li>영수증의 구성 요소를 보기 좋게 정렬하여 고객이 쉽게 금액과 수량을 확인할 수 있게 한다.</li>
</ul>

## 🏪기능 목록 정리
<ol>
<li>환영 인사와 함께 상품명, 가격, 프로모션 이름, 재고 안내 출력
<ul><li>만약 재고가 0개라면 재고 없음을 출력한다.</li></ul></li><br>
<li>사용자로부터 구매할 상품과 수량 입력
<ul><li>상품명, 수량은 하이픈(-)으로, 개별 상품은 대괄호([])로 묶어 쉼표(,)로 구분한다.</li></ul></li><br>
<li>재고 수량을 고려하여 결제 가능 여부 확인 및 업데이트</li><br>
<li>최종 결제 금액을 계산하고 구매 내역을 영수증으로 출력</li><br>
<li>프로모션 기간, 재고를 고려하여 프로모션 적용</li><br>
<li>프로모션 상품 수량을 적게 가져온 경우, 추가 여부 및 처리</li><br>
<li>프로모션 재고 부족의 경우 처리</li><br>
<li>멤버십 할인</li><br>
<li>추가 구매 진행 여부 선택</li>
</ol>

## 🏪예외 처리
<ul>
<li>구매할 상품과 수량 형식이 올바르지 않은 경우<br>"[ERROR] 올바르지 않은 형식으로 입력했습니다. 다시 입력해 주세요."<br>를 출력하고 재입력받는다.</li><br>
<li>존재하지 않는 상품을 입력한 경우<br>"[ERROR] 존재하지 않는 상품입니다. 다시 입력해 주세요."<br>를 출력하고 재입력받는다.</li><br>
<li>구매 수량이 재고 수량을 초과한 경우<br>"[ERROR] 재고 수량을 초과하여 구매할 수 없습니다. 다시 입력해 주세요."<br>를 출력하고 재입력받는다.</li><br>
<li>기타 잘못된 입력의 경우<br>"[ERROR] 잘못된 입력입니다. 다시 입력해 주세요."<br>를 출력하고 재입력받는다.</li><br>
</ul>