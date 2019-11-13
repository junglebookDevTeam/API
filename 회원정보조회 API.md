# 회원정보 조회 API

## Request (GET) ##
<p>URL: http://api.junglebook.co.kr/member/{라우트파라미터}</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>


{라우트파라미터}
<ul>
	<li><code>cash</code>: 현재 캐쉬 및 포인트 잔액<br>ex) http://api.junglebook.co.kr/member/cash</li>
</ul>

## Response (JSON) ##
<ul>
  <li>name: 이름</li>
  <li>company: 회사명</li>
  <li>item: 요청 데이터</li>
	<ul>
		<li>요청 데이터 값</li>
	</ul>
</ul>

## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		//캐쉬 및 포인트 잔액 조회
		curl -X GET
		http://api.junglebook.co.kr/member/cash
		-H 'cache-control: no-cache'
		-H 'Authorization: {api_key}'
	</code>
</pre>
