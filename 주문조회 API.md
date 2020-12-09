# 주문조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/order/{라우트파라미터}[/{OA타입}]</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

{라우트파라미터}
<ul>
	<li>주문번호로 송장번호 조회시 {라우트파라미터} = "{주문번호}" ex) http://api.junglebook.co.kr/invoice/1567382399000</li>
	<li>OA주문번호로 송장번호 조회시 {라우트파라미터} = "{OA주문번호}" ex) http://api.junglebook.co.kr/invoice/190901001</li>
	<li>{OA타입} (optional): OA주문번호로 조회시 OA타입을 지정해주면 찾고자 하는 주문정보를 보다 정확히 리턴 받을수 있습니다.
		<ul>
			<li>api: 정글북 주문서</li>
			<li>storefarm: 스토어팜 주문서</li>
			<li>emp: EMP(Playauto) 주문서</li>
			<li>talkstore: 톡스토어 주문서</li>
			<li>mall: 자체운영몰 주문서</li>
			<li>opo: 자사상품 주문서</li>
		</ul>
	</li>
</ul>

[/{OA타입}] (optional)
<ul>
	<li>OA주문번호로 송장번호 조회시 사용하는 파라미터 입니다 ex) http://api.junglebook.co.kr/invoice/190901001/mall</li>
</ul>

## Response (JSON) ##
<ul>
  <li>orderNo (bigint 20): 주문번호</li>
  <li>oaType (varchar 50) : OA타입</li>
  <li>oaOrderNo (varchar 100): OA주문번호</li>
  <li>orderName (varchar 20): 주문자명</li>
  <li>orderPhone (varchar 15) : 주문자 전화번호</li>
  <li>orderCellPhone (varchar 15): 주문자 휴대폰번호</li>
  <li>receiverName (varchar 20): 수취인명</li>
  <li>receiverPhone (varchar 15): 수취인 전화번호</li>
  <li>receiverCellPhone (varchar 15): 수취인 휴대폰번호</li>
  <li>receiverZonecode (varchar 5): 수취인 우편번호(신)</li>
  <li>receiverRoadAddress (varchar 100): 수취인 도로명주소(전체)</li>
  <li>receiverZipcode (varchar 7): 수취인 우편번호(구)</li>
  <li>receiverAddress (varchar 100): 수취인 주소(전체)</li>
  <li>orderMemo (varchar 100): 배송메세지</li>
  <li>settlePrice (int 10): 결제금액</li>
  <li>deliveryType (varchar 10): 배송타입</li>
  <li>deliveryCharge (int 10): 배송비</li>
  <li>invoiceCompanySno (int 3): 배송사코드</li>
	<ul>
		<li>15: CJ대한통운</li>
		<li>1: KGB택배</li>
		<li>39: 경동택배</li>
		<li>21: 드림택배</li>
		<li>5: 로젠택배</li>
		<li>13: 롯데택배</li>
		<li>19: 천일택배</li>
		<li>12: 한진택배</li>
	</ul>
  <li>invoiceCompanyNm (varchar 20): 배송사명</li>
  <li>invoiceNo (varchar 500): 송장번호 (송장번호가 2개 이상인경우, 구분자 콤마(,) ex: 123456789000,123456789001)</li>
  <li>orderStatus (int 4): 주문상태</li>
	<ul>
		<li>0: 주문접수</li>
		<li>1: 결제완료</li>
		<li>2: 상품준비중</li>
		<li>3: 출고완료</li>
	</ul>
  <li>orderClaimStatus (int 4): 주문클레임상태</li>
	<ul>
		<li>0: null</li>
		<li>40: 취소요청</li>
		<li>41: 취소접수</li>
		<li>42: 취소진행</li>
		<li>44: 취소완료</li>
		<li>50: 결제시도</li>
		<li>51: PG에러</li>
		<li>54: 결제실패</li>
	</ul>
  <li>insStatus (int 4): 검수상태</li>
	<ul>
		<li>0: null</li>
		<li>1: 검수중</li>
		<li>2: Boxing</li>
		<li>3: 검수완료</li>
		<li>10: 검수불가</li>
		<li>11: 입고대기</li>
	</ul>
  <li>insEprDt (date): 출고가능날짜</li>
  <li>regDt (date): 주문접수일</li>
  <li>paymentDt (date): 결제완료일</li>
  <li>deliveryDt (date): 출고일</li>
  <li>modDt (date): 최근수정일</li>
  
  <li>item (array): 주문상품</li>
	<ul>
		<li>goodsNo (int 10): 상품고유번호</li>
		<li>goodsNm (varchar 255): 상품명</li>
		<li>makerNm (varchar 50): 제조사</li> #Deprecated
		<li>brandNm (varchar 20): 브랜드</li> #Deprecated
		<li>goodsPrice (int 10): 판매가격</li>
		<li>claimStatus (int 4): 클레임상태</li>
			<ul>
				<li>0: null</li>
				<li>31: 추가발송</li>
				<li>41: 취소접수</li>
				<li>42: 취소진행</li>
				<li>44: 취소완료</li>
				<li>50: 결제시도</li>
				<li>51: PG에러</li>
				<li>54: 결제실패</li>
			</ul>
		<li>orderCnt (int): 주문수량</li>
	</ul>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		// 주문번호로 주문조회
		curl -X GET
		http://api.junglebook.co.kr/order/1567382399000
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// OA주문번호로 주문조회
		curl -X GET
		http://api.junglebook.co.kr/order/190901001/api
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>
