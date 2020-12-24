# 주문접수 API

## Request (POST) ##
<p>주문 요청 URL: https://api.junglebook.co.kr/order</p>
<p>테스트 주문 요청URL: https://api.junglebook.co.kr/order/test</p>
<p>Require header: Authorization {api_key} (api_key는 정글북 개발팀에 발급요청 하시기바랍니다. dev@junglebook.co.kr)</p>

## Response parameters ##

<ul>
	<li>data: 주문정보 (JSON 형식)</li>
</ul>

``` js
{
	"oaType": null, //[default: "api", string]
	//제휴처: storefarm(스토어팜), emp(EMP), talkstore(톡스토어), mall(자사몰), opo(자사상품발주)
	//제휴처별 주문관리를 위한 항목입니다. 제휴처 주문값이 없을경우 해당 파라미터 값을 null 또는 "api" 로 요청 합니다.
	
	"oaOrderNo": "123456", //[default: null, string]
	//제휴처 주문번호: null 인경우 자동으로 생성되며, 중복주문 확인 또는 주문조회시 사용 됩니다.
	//고객사에서 관리하고 있는 주문번호를 뜻합니다.
	
	"nameReceiver": "정글북", //[Required, string]
	//수령자: 2글자 이상의 수령자 이름
	
	"phoneReceiver": "010-1234-5678", //[Required, string]
	//수령자 전화번호1
	
	"mobileReceiver": "010-1234-5678", //[Required, string]
	//수령자 전화번호2
	
	"zipCode": "12345", //[Required, string]
	//(구/신)우편번호: 5자리 이상의 구 우편번호 또는 신 우편번호
	
	"address": "경기도 화성시 팔탄면 버들로 1362번길 10-12", //[Required, string]
	//(지번/도로명)주소: 주소정재 API를 이용하기 때문에 가급적 신주소로 요청하시기 바랍니다.
	
	"address2": "정글북", //[Required, string]
	//나머지 주소: 아파트명, 동, 호수 등 나머지 주소
	
	"settleKind": "a", //[default: "a", string]
	//결제방식: "a" => (무통장), "s" => (캐쉬결제)
	//무통장 결제인 경우, 주문접수만 처리 하고 캐쉬결제인 경우 주문접수후 캐쉬결제까지 처리합니다.
	
	"bankSender": "정글북", //[Conditional Required, string]
	//입금자명: settleKind 파라미터가 "a" (무통장)인경우 필수
	
	"doubleCheck": "1", //[Required, int]
	//구매동의: 구매하는 상품의 결제정보를 확인 하였으며, 구매진행의 동의여부 (1 => 동의, 0 => 동의하지 않음)
	//*동의하지 않을경우 주문접수 불가 합니다.
	
	"memo": "부재시 경비실에 맡겨주세요!", //[default: null, string]
	//배송메세지: 최대 100글자
	
	"orderItem": [ //[Required, array]
	// 주문상품 정보
		{
			"goodsNo": 7373, //[Required, int]
			//주문 상품번호: 정글북 상품번호
			
			"ea": 1 //[Required, int]
			//주문수량: 1 이상의 양수
		},
		{
			"goodsNo": 10437,
			"ea": 2
		},
		{
			"goodsNo": 10438,
			"ea": 3
		}
	]
}
```

## Response (JSON) ##

### 주문접수 성공시 ###

``` js
{
    "orderResult": { //주문접수 결과
        "success": "1", //성공여부 (1 => 성공, 0 => 실패)
        "ordNo": "1525145229154", //정글북 주문번호
        "oaType": "api", //제휴처 (api => oAPI를 이용한 일반 정글북 주문을 뜻함)
        "oaApiOrdno": "123456", //제휴처 주문번호 (주문접수시 입력하신 고객사 주문번호)
        "nameReceiver": "정글북", //수령자
        "zipCode": "12345", //우편번호
        "address": "경기도 화성시 팔탄면 버들로 1362번길 10-12 정글북", //주소
        "orderGoods": "[테스트] 일반상품 외 2건", //주문상품내용 요약
        "settleKind": "a", //결제방법
        "settlePrice": "7600", //총 결제금액
        "totalGoodsPrice": "5100", //총 상품금액
        "delivery": "2500", //배송비
        "memo": "부재시 경비실에 맡겨주세요!" //배송 메세지 (주문 테스트인경우 요청 파라미터가 삽입되어 리턴 됩니다.)
    },
    "payResult": { //결제결과
        "successs": 0, //성공여부 (1 => 성공, 0 => 실패)
        "payResultMsg": "order test :)", //결제결과 메세지
        "cashBalance": "0", //현재 캐쉬 잔액 (결제성공시에는 결제후 잔액)
        "payAmount": "7600" //결제요청 금액
    }
}
```

### 주문접수 실패시 (parameters error) ###

``` js
{
    "orderResult": { //주문접수 결과
        "success": 0, //성공여부 (1 => 성공, 0 => 실패)
        "errCode": "001", //에러코드
        "parameter": "nameReceiver", //에러 파라미터
        "errMsg": "parameter required" //에러 메세지
    },
    "payResult": {
        "successs": 0,
        "payResultMsg": "did not even try because order failed",
        "cashBalance": "0",
        "payAmount": 0
    }
}
```

### 주문접수 실패시 (중복주문) ###

``` js
{
    "orderResult": {
        "success": 0,
        "errCode": "105",
        "parameter": {
            "oaOrderNo": "123456",
            "dupOrderData": {
                "ordNo": "1525150381173",
                "oaOrderNo": "123456",
                "nameReceiver": "정글북"
            }
        },
        "errMsg": "duplicate order"
    },
    "payResult": {
        "successs": 0,
        "payResultMsg": "did not even try because order failed",
        "cashBalance": "0",
        "payAmount": 0
    }
}
```

### 주문접수 실패시 (주문상품 오류: 주문상품 품절) ###

``` js
{
    "payResult": {
        "successs": 0,
        "payResultMsg": "did not even try because order failed",
        "cashBalance": "0",
        "payAmount": 0,
        "bankAccount": "1",
        "bankSender": null
    },
    "orderResult": {
        "success": "0",
        "goodsData": {
            "goodsNo": "7373", //상품번호
            "goodsNm": "[테스트] 일반상품", //상품명
            "categoryCode": "001", //카테고리 코드 (SEPERATOR: "|")
            "categoryNm": "미분류(삭제X)", //카테고리 명 (SEPERATOR: "|")
            "origin": "국산", //원산지
            "maker": "테스트메이커", //제조사
            "brand": "굿프랜드", //브랜드
            "goodsPrice": "850", //상품가격
            "suggestionSalesPrice": "1070", //제안 상품가격
            "goodsDetail": "<img src=\"http://img.junglebook.co.kr/pettob/desc/D170311007373_0.png\">", //상세정보
            "goodsImage": "http://img.junglebook.co.kr/pettob/goods/G170221007373_l.png", //상품이미지 (SEPERATOR: "|")
            "goodsStock": "23", //재고
            "runout": "1", //품절여부
            "open": "1", //진열여부
            "EAD": "", //입고예정일자
            "inPackageEA": "100", //패키지 단위
            "tags": "" //상품TAG
        },
        "errCode": "206", //에러코드
        "errMsg": "runout" //에러 메세지
    }
}
```

### 결제 성공시 ###

``` js
{
    "orderResult": {
        "success": "1",
        "ordNo": "1525145229154",
        "oaType": "api",
        "oaApiOrdno": "123456",
        "nameReceiver": "정글북",
        "zipCode": "12345",
        "address": "경기도 화성시 팔탄면 버들로 1362번길 10-12 정글북",
        "orderGoods": "[테스트] 일반상품 외 2건",
        "settleKind": "a",
        "settlePrice": "7600",
        "totalGoodsPrice": "5100",
        "delivery": "2500",
        "memo": "부재시 경비실에 맡겨주세요!" 
    },
    "payResult": {
        "successs": 1,
        "payResultMsg": "success",
        "cashBalance": "10564",
        "payAmount": "7600" 
    }
}
```

<p>* 테스트 주문 또는 무통장으로 주문접수 할 경우 결제수단을 무통장 결제로 주문접수 처리 하기때문에 payResult 의 successs 값은 0 으로 리턴됩니다.</p>

### 결제 실패시 (캐쉬결제 실패: 캐쉬부족) ###

``` js
{
    "orderResult": {
        "success": "1",
        "ordNo": "1525154725763",
        "oaType": "api",
        "oaApiOrdno": "123456",
        "nameReceiver": "정글북",
        "zipCode": "12345",
        "address": "경기도 화성시 팔탄면 버들로 1362번길 10-12 정글북",
        "orderGoods": "[테스트] 일반상품4 외 2건",
        "settleKind": "s",
        "settlePrice": "10006750",
        "totalGoodsPrice": "10004250",
        "delivery": "2500",
        "memo": "부재시 경비실에 맡겨주세요!"
    },
    "payResult": {
        "successs": 0,
        "payResultMsg": "not enough cash",
        "cashBalance": "0",
        "payAmount": "10006750"
    }
}
```

## 자사상품 발주 ##

* 자사상품 발주시 __oaType__ 파라미터의 값은 __opo__ 입니다.
* 자사상품 발주시 아래 파라미터 값은 고정으로 요청처리 합니다.

| Parameter  | 값 |
| ------------- | ------------- |
| nameReceiver  | 주문자명  |
| zipCode  | 물류센터 우편번호  |
| address  | 물류센터 주소  |
| address2  | 물류센터 주소2 |

<p>* 자사상품 발주시 상품의 품절여부 및 재고여부와 상관없이 요청한 수량으로 주문접수 됩니다.</p>


## Error codes ##

#### 주문접수 Error codes ####
| Code  | Error message | 내용 |
| ------------- | ------------- | ------------- |
| 001  | parameter required  | 필수 파라미터 오류   |
| 002  | invalid argument   | 파라미터 형식 오류  |
| 101  | must be "1" for checking your purchase  | 구매 및 결제확인 동의하지 않음 으로인한 주문접수 불가  |
| 102  | duplicate items are ordered   | 주문상품중 중복으로 주문한 상품이 있음  |
| 103  | items that can not be ordered  | 구매 불가 상품 주문  |
| 104  | request order items are not matched  | 주문 상품 없음  |
| 105  | duplicate order  | 중복주문 오류  |
| 201  | can not found matched goods  | 주문상품 찾을수 없음  |
| 202  | invalid option  | 상품옵션 오류  |
| 203  | invalid bundle order quantity  | 묶음주문 수량 오류  |
| 204  | invalid min order quantity  | 최소 구매 수량 오류  |
| 205  | invalid max order quantity  | 최대 구매 수량 오류  |
| 206  | runout  | 주문상품 품절  |
| 207  | not enough stock  | 주문상품 재고부족  |
| 208  | items that can not be ordered by request of supplier  | 공급사 요청으로 인한 구매제한 상품 주문  |



## Code sample ##
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
curl -X POST \
  https://api.junglebook.co.kr/order \
  -H 'cache-control: no-cache' \
  -H 'Authorization: {api_key}' \
  -F 'data={
	"oaType": null,
	"oaOrderNo": "123456",
	"nameReceiver": "정글북",
	"phoneReceiver": "010-1234-5678",
	"mobileReceiver": "010-1234-5678",
	"zipCode": "12345",
	"address": "경기도 화성시 팔탄면 버들로 1362번길 10-12",
	"address2": "정글북",
	"settleKind": "a",
	"bankSender": "정글북",
	"doubleCheck": "1",
	"memo": "부재시 경비실에 맡겨주세요!",
	"orderItem":[
		{
			"goodsNo": 7373,
			"ea": 1
		},
		{
			"goodsNo": 10437,
			"ea": 2
		},
		{
			"goodsNo": 10438,
			"ea": 3
		}
	]
}'
	</code>
</pre>
