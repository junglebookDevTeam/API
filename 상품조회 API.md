# 상품조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/goods/{라우트파라미터}[/{페이지번호}]?{조건파라미터}={값}</p>
<p><p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p></p>

{라우트파라미터}
<ul>
	<li>특정상품 조회시 {라우트파라미터} = "{상품번호}" ex) http://api.junglebook.co.kr/goods/3754</li>
	<li>전체상품 조회시 {라우트파라미터} = "all" ex) http://api.junglebook.co.kr/goods/all/2</li>
	<li>미진열상품 조회시 {라우트파라미터} = "close" ex) http://api.junglebook.co.kr/goods/close/3</li>
	<li>전체 또는 미진열 상품 조회시 페이징 처리가 되며, 한 페이지당 100개의 상품이 조회됩니다.</li>
</ul>

[/{페이지번호}] (optional)
<ul>
	<li>전체 또는 미진열 상품 조회시 사용하는 파라미터 입니다 ex) http://api.junglebook.co.kr/goods/all/7</li>
</ul>

{조건파라미터}
<ul>
	<li><code>updateAfter</code>: 특정일 포함 이후 업데이트 상품 조회 (값 형식: yyyy-mm-dd)<br>ex) http://api.junglebook.co.kr/goods/all?updateAfter=2019-09-01</li>
</ul>

## Response (JSON) ##
<ul>
  <li>total: 조회된 상품수</li>
  <li>totalPageCnt: 전체 페이지수</li>
  <li>currentPage: 현재 페이지번호</li>
  <li>data: 상품정보(array)</li>
  <ul>
    <li>goodsNo: 상품번호</li>
	<li>open: 진열여부 (* open 값이 "0" 인 경우(미진열 상품) 이하 상품정보값은 표시 하지 않습니다.)</li>
    <li>goodsNm: 상품명</li>
    <li>categoryCode: 카테고리코드(SEPERATOR "|")</li>
    <li>categoryNm: 카테고리명(SEPERATOR "|")</li>
    <li>origin: 원산지</li>
    <li>maker: 제조사</li>
    <li>brand: 브렌드</li>
    <li>goodsPrice: 상품판매가(파트너사의 매입가)</li>
    <li>suggestionSalesPrice: 제안 판매가</li>
    <li>goodsDetail: 상품상세정보</li>
	<li>goodsRepImage: 상품대표 이미지</li>
    <li>goodsImage: 상품 추가 이미지(array)</li>
    <li>goodsStock: 상품재고수</li>
    <li>runout: 품절여부</li>
    <li>EAD: 재입고일</li>
    <li>inPackageEA: 패키지 입수량</li>
	<li>tags: 상품 특이사항(SEPERATOR ",")</li>
  </ul>
</ul>

## 상품Tag 검색 ##

http://api.junglebook.co.kr/goods/tag[/페이지번호]?q={태그}

태그 리스트
<ul>
	<li><code>긴급소진</code>: 유통기한 임박 또는 악성재고 상품으로 분류되어 빠르게 소진 해야 할 상품 입니다.</li>
	<li><code>본사품절</code>: 유통본사 재고가 없는 상품으로 분류되어 발주 및 입고예정일을 확인 할 수 없는 상품 입니다.</li>
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
		http://api.junglebook.co.kr/goods/3754
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// 전체상품 조회
		curl -X GET
		http://api.junglebook.co.kr/goods/all
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// 미진열 상품 조회
		curl -X GET
		http://api.junglebook.co.kr/goods/close
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
	<code>
		// Tag검색
		curl -X GET
		http://api.junglebook.co.kr/goods/tag/1?query=단종
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>