# 송장번호 조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/invoice/{주문번호}[/{OA타입}]</p>
<p>Require header: pd_key (해당키는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* {주문번호}: 정글북 주문번호 또는 OA주문번호</p>
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
  <li>orderNo: 주문번호</li>
  <li>oaType: OA타입</li>
  <li>oaOrderNo: OA주문번호</li>
  <li>deliveryType: 배송타입</li>
  <li>deliveryCharge: 배송비</li>
  <li>invoiceCompanySno: 배송사코드</li>
	<ul>
		<li>12: 한진택배</li>
		<li>15: CJ대한통운</li>
		<li>21: KG로지스</li>
	</ul>
  <li>invoiceCompanyNm: 배송사명</li>
  <li>invoiceNo: 송장번호 (송장번호가 2개 이상인경우, 구분자 콤마(,) ex: 123456789000,123456789001)</li>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		http://api.junglebook.co.kr/invoice/{주문번호}[/{OA타입}]
		-H 'cache-control: no-cache'
		-H 'pd_key: {발급받은 API key}'
	</code>
</pre>
