# 추가 배송료 조회 API

## Request (POST) ##
<p>URL: https://api.junglebook.co.kr/shipping/extraFare</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

## Request parameters ##

<ul>
	<li>(JSON 형식)</li>
</ul>

``` js
{
	"zipCode": "63503", //[Required, string]
	//우편번호
  
	"roadAddress": "제주특별자치도 서귀포시 대정읍 대한로 632", //[Conditional required, string]
	//도로명주소 (구주소 또는 도로명주소 중 1개 값은 필수 입니다.)
	
	"address": "제주특별자치도 서귀포시 대정읍 무릉리 310", //[Conditional required, string]
	//구주소 (구주소 또는 도로명주소 중 1개 값은 필수 입니다.)
}
```

## Response (JSON) ##

### 조회 성공시 (추가 배송료가 있는 경우) ###
``` js
{
    "extraShippingFare": 3000
}
```

### 조회 성공시 (추가 배송료가 없는 경우) ###
``` js
{
    "extraShippingFare": 0
}
```

### 조회 실패시 ###

``` js
{}
```


## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
curl -X POST \
  https://api.junglebook.co.kr/shipping/extraFare \
  -H 'cache-control: no-cache' \
  -H 'Authorization: {api_key}' \
  -F '{"zipCode": "06546", "roadAddress": "제주특별자치도 서귀포시 대정읍 대한로 632"}'
	</code>
</pre>
