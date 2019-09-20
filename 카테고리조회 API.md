# 카테고리 조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/category[/{카테고리코드}]</p>
<p>Require header: pd_key (해당키는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* 전체카테고리 조회시 => http://api.junglebook.co.kr/category</p>
<p>* 특정 카테고리 조회시 => http://api.junglebook.co.kr/category[/{카테고리코드}]</p>
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
		http://api.junglebook.co.kr/category[/{카테고리코드}]
		-H 'cache-control: no-cache'
		-H 'pd_key: {발급받은 API key}'
	</code>
</pre>
