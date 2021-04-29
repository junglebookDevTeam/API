# 상품조회 API

## Request (GET) ##
<p>URL: https://api.junglebook.co.kr/goods/{라우트파라미터}[/{페이지번호}]?{조건파라미터}={값}</p>
<p><p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p></p>

{라우트파라미터}
<ul>
	<li>특정상품 조회시 {라우트파라미터} = "{상품번호}" ex) https://api.junglebook.co.kr/goods/3754</li>
	<li>전체상품 조회시 {라우트파라미터} = "all" ex) https://api.junglebook.co.kr/goods/all/2</li>
	<li>미진열상품 조회시 {라우트파라미터} = "close" ex) https://api.junglebook.co.kr/goods/close/3</li>
	<li>
		상품명 검색시 {라우트파라미터} = "goodsNm" ex) https://api.junglebook.co.kr/goods/goodsNm/1?query=뉴트리오큐브<br>
		- 검색어에 대한 형태소 분리 및 (일반, 고유)명사를 추출하여 상품명 필드 대상 LIKE 조건 검색 합니다.
	</li>
	<li>상품 조회시 상품수가 100개 이상인 경우, 페이징 처리가 되며 한 페이지당 100개의 상품이 조회됩니다.</li>
</ul>

[/{페이지번호}] (optional)
<ul>
	<li>페이징 처리된 경우 페이지번호 파라미터를 이용하여 특정 페이지의 데이터를 조회 합니다. ex) https://api.junglebook.co.kr/goods/all/7</li>
</ul>

{조건파라미터}
<ul>
	<li><code>updateAfter</code> (optional): 특정일 포함 이후 업데이트 상품 조회 (값 형식: yyyy-mm-dd)<br>ex) https://api.junglebook.co.kr/goods/all?updateAfter=2019-09-01</li>
	<li><code>query</code> (Conditional Required): 특정 라우트파라미터(goodsNm) 사용시 필수 파라미터 입니다.<br>ex) https://api.junglebook.co.kr/goods/goodsNm/1?query=뉴트리오큐브</li>
</ul>

## Response (JSON) ##
<ul>
  <li><code><strong>total</strong></code>(int): 조회된 상품수</li>
  <li><code><strong>totalPageCnt</strong></code>(int): 전체 페이지수</li>
  <li><code><strong>currentPage</strong></code>(int): 현재 페이지번호</li>
  <li><code><strong>data</strong></code>(array): 상품정보</li>
  <ul>
    <li><code><strong>goodsNo</strong></code>(int): 상품번호</li>
	<li><code><strong>open</strong></code>(int): 진열여부 (* open 값이 "0" 인 경우(미진열 상품) 이하 상품정보값은 표시 하지 않습니다.)</li>
    <li><code><strong>goodsNm</strong></code>(string): 상품명</li>
    <li><code><strong>categoryCode</strong></code>(string): 카테고리코드(SEPERATOR "|")</li>
    <li><code><strong>categoryNm</strong></code>(string): 카테고리명(SEPERATOR "|")</li>
    <li><code><strong>origin</strong></code>(string): 원산지</li>
    <li><code><strong>maker</strong></code>(string): 제조사</li>
    <li><code><strong>brand</strong></code>(string): 브렌드</li>
    <li><code><strong>goodsPrice</strong></code>(int): 상품판매가(파트너사의 매입가)</li>
    <li><code><strong>suggestionSalesPrice</strong></code>(int): 파트너사의 권장 판매가</li>
	<ul>
		<li>권장 판매가의 경우 기본적으로 goodsPrice 값의 마진율 20% 계산한 금액을 리턴 합니다.</li>
		<li>상품공급 계약에 따라 파트너사가 고객에게 특정 판매가로 판매 하셔야 할 경우 goodsPrice 값 기준으로 계약 판매 마진율 N%가 계산된 상품 판매가를 리턴해 드립니다.</li>
		<li>별도 상품공급 계약을 하지 않은 파트너사는 리턴해 드리는 권장 판매가를 무시 하셔도 좋습니다.</li>
		<li>(단, 상품별로 온라인/오프라인 최소 판매가 준수 사항이 있으니 관련 문의는 정글북 MD팀으로 문의 부탁 드립니다!)</li>
		<li>계산공식: suggestionSalesPrice = goodsPrice / (1 - N%), N = 계약 판매 마진율, 10의 자리 올림 처리</li>
	</ul>
	<li><code><strong>sspProfitRate</strong></code>(int): 권장 판매가 마진율(%), (suggestionSalesPrice의 10의 자리 올림 처리로 계약 마진율 보다 같거나 높을 수 있습니다.)</li>
	<li><code><strong>suggestionRetailPrice</strong></code>(int): 권장 소비자가</li>
    <li><code><strong>goodsDetail</strong></code>(mediumtext): 상품상세정보</li>
	<li><code><strong>goodsRepImage</strong></code>(string): 상품대표 이미지</li>
    <li><code><strong>goodsImage</strong></code>(array): 상품 추가 이미지</li>
    <li><code><strong>goodsStock</strong></code>(int): 상품재고수</li>
    <li><code><strong>runout</strong></code>(int): 품절여부</li>
	<li><code><strong>barcode</strong></code>(string): 상품 바코드 (바코드 시작 값이 "A" 인 경우 정글북에서 임의 생성한 바코드 입니다. 경우에 따라 상품의 실제 바코드와 다를 수 있습니다.)</li>
    <li><code><strong>EAD</strong></code>(date): 재입고일</li>
    <li><code><strong>inPackageEA</strong></code>(int): 패키지 입수량</li>
	<li><code><strong>delivery</strong></code>(object): 상품 배송비 데이터</li>
	<ul>
		<li><code><strong>type</strong></code>(int): 배송비 설정</li>
		<ul>
			<li><code><strong>0</strong></code>: 기본</li>
			<li><code><strong>1</strong></code>: 무료 (해당 상품은 별도 배송비 없이 무료 배송)</li>
			<li><code><strong>3</strong></code>: 착불 (해당 상품 구매시 착불로 배송 됩니다.)</li>
			<li><code><strong>4</strong></code>: 고정 (구매 수량 상관없이 고정 배송비 부과 합니다.)</li>
			<li><code><strong>5</strong></code>: 수량별 (구매 수량별 배송비가 계산되어 부과 됩니다.)</li>
		</ul>
		<li><code><strong>title</strong></code>(string): 배송설정 타이틀</li>
		<li><code><strong>fee</strong></code>(int): 배송비</li>
	</ul>
	<li><code><strong>expData</strong></code>(object): 상품 유통기한 데이터</li>
	<ul>
		<li><code><strong>active</strong></code>(date): 현재 출고 중인 ACTIVE 유통기한 날짜</li>
		<li><code><strong>cActive</strong></code>(date): 선입선출 전제로 계산된 ACTIVE 유통기한 날짜</li>
		<li><code><strong>period</strong></code>(int): 유통기간 (제조일로 부터 N개월)</li>
		<li><code><strong>releasable</strong></code>(array): 출고 가능성 있는 유통기한 날짜 리스트</li>
	</ul>
	<li><code><strong>updateDt</strong></code>(date): 상품 업데이트 날짜</li>
	<li><code><strong>regDt</strong></code>(date): 상품 등록 날짜</li>
  </ul>
</ul>

## 상품Tag 검색 ##

https://api.junglebook.co.kr/goods/tag[/페이지번호]?q={태그}

태그 리스트
<ul>
	<li><code>긴급소진</code>: 유통기한 임박 또는 악성재고 상품으로 분류되어 빠르게 소진 해야 할 상품 입니다.</li>
	<li><code>본사품절</code>: 유통본사 재고가 없는 상품으로 분류되어 발주 및 입고예정일을 확인 할 수 없는 상품 입니다.</li>
	<li><code>단종예정</code>: 단종예정 상품 입니다.</li>
	<li><code>단종</code>: 단종된 상품 입니다.</li>
	<li><code>오프전용</code>: 오프라인에서만 판매/유통 할 수 있는 상품입니다.</li>
	<li><code>단가인상</code>: 단가인상 예정인 상품 입니다.</li>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		// 상품번호 조회
		curl -X GET
		https://api.junglebook.co.kr/goods/3754
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// 전체상품 조회
		curl -X GET
		https://api.junglebook.co.kr/goods/all
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// 미진열 상품 조회
		curl -X GET
		https://api.junglebook.co.kr/goods/close
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// Tag검색
		curl -X GET
		https://api.junglebook.co.kr/goods/tag/1?query=단종
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>