# 회원정보 조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/member/{요청항목}</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

<p>* {요청항목}: 회원정보 항목중 요청할 항목</p>
<p>
	{요청항목} = 
	<ul>
		<li>cash: 캐쉬 및 포인트 잔액</li>
	</ul>
</p>

## Response (JSON) ##
<ul>
  <li>name: 이름</li>
  <li>company: 회사명</li>
  <li>item: 요청항목 데이터</li>
	<ul>
		<li>요청항목 데이터</li>
	</ul>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		http://api.junglebook.co.kr/member/{요청항목}
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>
