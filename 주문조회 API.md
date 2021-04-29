# 주문조회 API

## Request (GET) ##
<p>URL: https://api.junglebook.co.kr/order/{주문번호}[/{OA타입}]</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* {주문번호}: 정글북 주문번호 또는 OA주문번호(고객사에서 관리하고 있는 주문번호)</p>
<p>* {OA타입} (optional): OA주문번호로 조회시 OA타입을 지정해주면 찾고자 하는 주문정보를 보다 정확히 리턴 받을수 있습니다.</p>
<p>
	{OA타입} = 
	<ul>
		<li>pettob: 정글북 주문서</li>
		<li>storefarm: 스토어팜 주문서</li>
		<li>emp: EMP(Playauto) 주문서</li>
		<li>talkstore: 톡스토어 주문서</li>
		<li>mall: 자체운영몰 주문서</li>
	</ul>
</p>

## Response (JSON) ##
<ul>
  <li><code><strong>orderNo</strong></code>(bigint): 주문번호</li>
  <li><code><strong>oaType</strong></code>(string) : OA타입</li>
  <li><code><strong>oaOrderNo</strong></code>(string): OA주문번호</li>
  <li><code><strong>orderName</strong></code>(string): 주문자명</li>
  <li><code><strong>orderPhone</strong></code>(string) : 주문자 전화번호</li>
  <li><code><strong>orderCellPhone</strong></code>(string): 주문자 휴대폰번호</li>
  <li><code><strong>receiverName</strong></code>(string): 수취인명</li>
  <li><code><strong>receiverPhone</strong></code>(string): 수취인 전화번호</li>
  <li><code><strong>receiverCellPhone</strong></code>(string): 수취인 휴대폰번호</li>
  <li><code><strong>receiverZonecode</strong></code>(string): 수취인 우편번호(신)</li>
  <li><code><strong>receiverRoadAddress</strong></code>(string): 수취인 도로명주소(전체)</li>
  <li><code><strong>receiverZipcode</strong></code>(string): 수취인 우편번호(구)</li>
  <li><code><strong>receiverAddress</strong></code>(string): 수취인 주소(전체)</li>
  <li><code><strong>orderMemo</strong></code>(string): 배송메세지</li>
  <li><code><strong>settlePrice</strong></code>(int): 결제금액</li>
  <li><code><strong>deliveryType</strong></code>(string): 배송타입</li>
  <li><code><strong>deliveryCharge</strong></code>(int): 배송비</li>
  <li><code><strong>invoiceCompanySno</strong></code>(int): 배송사코드</li>
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
  <li><code><strong>invoiceCompanyNm</strong></code>(string): 배송사명</li>
  <li><code><strong>invoiceNo</strong></code>(string): 송장번호 (송장번호가 2개 이상인경우, 구분자 콤마(,) ex: 123456789000,123456789001)</li>
  <li><code><strong>orderStatus</strong></code>(int): 주문상태</li>
	<ul>
		<li>0: 주문접수</li>
		<li>1: 결제완료</li>
		<li>2: 상품준비중</li>
		<li>3: 출고완료</li>
	</ul>
  <li><code><strong>orderClaimStatus</strong></code>(int): 주문클레임상태</li>
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
  <li><code><strong>insStatus</strong></code>(int): 검수상태</li>
	<ul>
		<li>0: null</li>
		<li>1: 검수중</li>
		<li>2: Boxing</li>
		<li>3: 검수완료</li>
		<li>10: 검수불가</li>
		<li>11: 입고대기</li>
	</ul>
  <li><code><strong>insEprDt</strong></code>(date): 출고가능날짜</li>
  <li><code><strong>regDt</strong></code>(datetime): 주문접수일</li>
  <li><code><strong>paymentDt</strong></code>(datetime): 결제완료일</li>
  <li><code><strong>deliveryDt</strong></code>(datetime): 출고일</li>
  <li><code><strong>modDt</strong></code>(datetime): 최근수정일</li>
  
  <li><code><strong>item</strong></code>(array, object): 주문상품</li>
	<ul>
		<li><code><strong>goodsNo</strong></code>(int): 상품고유번호</li>
		<li><code><strong>goodsNm</strong></code>(string): 상품명</li>
		<li><code><strong>makerNm</strong></code>(string): 제조사</li> #Deprecated
		<li><code><strong>brandNm</strong></code>(string): 브랜드</li> #Deprecated
		<li><code><strong>goodsPrice</strong></code>(int): 판매가격</li>
		<li><code><strong>claimStatus</strong></code>(int): 클레임상태</li>
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
		<li><code><strong>orderCnt</strong></code>(int): 주문수량</li>
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
		https://api.junglebook.co.kr/order/1567382399000
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// OA주문번호로 주문조회
		curl -X GET
		https://api.junglebook.co.kr/order/190901001/api
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>
