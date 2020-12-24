# 카테고리 조회 API

## Intro ##
<p>카테고리 구조</p>
<ul>
	<li>카테고리 구조는 최대 4 depth 로 구성 되어 있으며, 각 depth의 카테고리코드(categoryCode)는 3자리 입니다.</li>
	<li>각 depth의 카테고리 코드는 이전 depth 각각의 카테고리 코드를 연결한 코드 입니다.</li>
	<li>
		예시)
		<ul>
			<li>1 depth: <code>032</code> (고양이)</li>
			<li>2 depth: <code>032</code><code>001</code> (사료)</li>
			<li>3 depth: <code>032</code><code>001</code><code>001</code> (브랜드사료)</li>
			<li>4 depth: <code>032</code><code>001</code><code>001</code></code><code>011</code> (로얄캐닌)</li>
			<li>032001001011 => (고양이 > 사료 > 브랜드사료 > 로얄캐닌)</li>
		</ul>
	</li>
</ul>

## Request (GET) ##
<p>URL: https://api.junglebook.co.kr/category[/{카테고리코드}]</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* 전체카테고리 조회시 => https://api.junglebook.co.kr/category</p>
<p>* 특정 카테고리 조회시 => https://api.junglebook.co.kr/category[/{카테고리코드}]</p>
<p>* 특정 카테고리 조회시 요청한 카테고리 포함한 하위 카테고리 데이터를 리턴합니다. </p>

## Response (JSON) ##
<ul>
  <li>categoryNm: 카테고리 이름</li>
  <li>categoryCode: 카테고리 코드</li>
  <li>parentCategory: 상위(부모) 카테고리 코드</li>
  <li>children: 하위 카테고리 정보(array)</li>
  <ul>
		<li>categoryNm: 카테고리 이름</li>
		<li>categoryCode: 카테고리 코드</li>
		<li>parentCategory: 상위(부모) 카테고리 코드</li>
		<li>children: 하위 카테고리 정보(array)</li>
			<ul>
				<li>... 최대 4 depth</li>
		  </ul>
  </ul>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		https://api.junglebook.co.kr/category
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>

# 카테고리별 상품 조회 API

## Request (GET) ##
<p>URL: https://api.junglebook.co.kr/category/{카테고리코드}/goods/[/{페이지번호}]?{조건파라미터}={값}</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

{카테고리코드}
<ul>
	<li>카테고리 조회 API에서 리턴받은 <code><strong>categoryCode</strong></code> 값</li>
</ul>

[/{페이지번호}] (optional)
<ul>
	<li>페이징 처리된 경우 페이지번호 파라미터를 이용하여 특정 페이지의 데이터를 조회 합니다. ex) https://api.junglebook.co.kr/category/031/goods/7</li>
</ul>

{조건파라미터}
<ul>
	<li><code>updateAfter</code>: 특정일 포함 이후 업데이트 상품 조회 (값 형식: yyyy-mm-dd)<br>ex) https://api.junglebook.co.kr/category/031/goods?updateAfter=2020-12-24</li>
</ul>

## Response (JSON) ##

상품조회 API > Response 참고
https://github.com/junglebookDevTeam/API/blob/master/%EC%83%81%ED%92%88%EC%A1%B0%ED%9A%8C%20API.md#response-json

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		https://api.junglebook.co.kr/category/031/goods/1
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>
