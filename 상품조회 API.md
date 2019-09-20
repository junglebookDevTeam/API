# 상품조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/goods/{상품번호} OR !{태그}[/{페이지번호}]</p>
<p>Require header: pd_key (해당키는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* {상품번호} OR !{태그}: 정글북 상품번호 또는 !태그명</p>
<p>* 전체상품 조회시 {상품번호} = "all" ex) http://api.junglebook.co.kr/goods/all[/{페이지번호}]</p>
<p>* 전체상품 조회시 페이징 처리가 되며, 한 페이지당 50개의 상품이 조회됩니다.</p>

## Response (JSON) ##
<ul>
  <li>total: 조회된 상품수</li>
  <li>totalPageCnt: 전체 페이지수</li>
  <li>currentPage: 현재 페이지번호</li>
  <li>data: 상품정보(array)</li>
  <ul>
    <li>goodsNo: 상품번호</li>
    <li>goodsNm: 상품명</li>
    <li>categoryCode: 카테고리코드(SEPERATOR "|")</li>
    <li>categoryNm: 카테고리명(SEPERATOR "|")</li>
    <li>origin: 원산지</li>
    <li>maker: 제조사</li>
    <li>brand: 브렌드</li>
    <li>goodsPrice: 상품판매가(파트너사의 매입가)</li>
    <li>suggestionSalesPrice: 제안 판매가</li>
    <li>goodsDetail: 상품상세정보</li>
    <li>goodsImage: 상품이미지</li>
    <li>goodsStock: 상품재고수</li>
    <li>runout: 품절여부</li>
    <li>open: 진열여부</li>
    <li>EAD: 재입고일</li>
    <li>inPackageEA: 패키지 입수량</li>
	<li>tags: 상품 특이사항(SEPERATOR ",")</li>
  </ul>
</ul>

## 상품Tag 검색 ##

http://api.junglebook.co.kr/goods/!{태그}[/페이지번호]
* 태그로 상품조회시 태그명 앞에 "!" 삽입

태그 리스트
<ul>
	<li><code>!긴급소진</code>: 유통기한 임박 또는 악성재고 상품으로 분류되어 빠르게 소진 해야 할 상품 입니다.</li>
	<li><code>!본사품절</code>: 유통본사 재고가 없는 상품으로 분류되어 발주 및 입고예정일을 확인 할 수 없는 상품 입니다.</li>
	<li><code>!롱-리드</code>: 재입고까지 최소 2주 이상 걸리는 리드타임이 긴 상품 입니다.</li>
	<li><code>!단종</code>: 단종된 상품 입니다.</li>
	<li><code>!오프전용</code>: 오프라인에서만 판매/유통 할 수 있는 상품입니다.</li>
	<li><code>!단가인상</code>: 단가인상 예정인 상품 입니다.</li>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		http://api.junglebook.co.kr/goods/{상품번호} OR all OR !{태그}[/{페이지번호}]
		-H 'cache-control: no-cache'
		-H 'pd_key: {발급받은 API key}'
	</code>
</pre>
