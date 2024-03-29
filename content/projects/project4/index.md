---
title: "네이버 SENS API와 Node.js로 휴대전화 SMS 인증하기"
date: 2020-05-16
draft: false
project_tags: ["SENS API"]
status: "evergreen"
weight: 1
summary: "애플리케이션 내 휴대전화 인증을 위한 SENS API 사용법"
---

이게 엄청 옛날에 쓴 글인데 ㅠㅡㅠ 당시 조회수도 좀 있었구,,, 누가 필요하실까봐 남겨놓아요! 근데 제 원래 블로그에 어떤 분이 뭐 deprecated 됐다구 올리셔서.... 그 점은 참고하셔야 할 것 같아요!

#### 인트로

안드로이드에서 받아온 유저의 휴대폰 번호를 Node.js 서버로 넘겨 네이버 SENS API로 인증 문자를 보내려고 합니다.

먼저 제가 현재 졸업작품으로 개발 중인 프로젝트는 이더리움 블록체인을 이용한 신뢰성 있는 중고 전자기기 거래 플랫폼이에요. 모바일 애플리케이션으로 구현 중이고, IDE는 안드로이드 스튜디오를 사용 중입니다. 일단 제가 포스팅할 부분 전에, 안드로이드에서 사용자의 휴대폰 번호(수신 번호)와 인증 번호(내용)를 서버로 보낸 상태라고 가정하고 시작하도록 하겠습니다. 저는 서버로 Node.js를 사용했어요.

저는 일단 학생이라, 우리가 흔히 모바일 애플리케이션에서 사용하는 휴대폰 인증은 사용할 수가 없었어요. 그건 사업자 번호가 필요하거든요. 그래서 원래는 FCM을 이용해서 사람들이 회원가입을 하려고 할 때마다, 저한테 { 휴대폰 번호 : 인증번호 } 이런 식으로 푸시 메시지를 보내서 제가 다시 사용자들에게 문자 해주는 방식으로 인증을 하려고 했어요. 그런데 FCM 라이브러리가 얼마 전에(?) 업데이트되면서 사용법을 잘 모르겠어서 포기했습니다... 분명 사용법이 편해졌을텐데 기존에 있던 라이브러리 하나가 없어지고 통합되는 바람에, 토큰 받아오는 방법을 모르겠더라구요... 시간이 남으면 FCM도 다시 진행해서 포스트 하겠습니다.

우선 네이버 클라우드 플랫폼에 가입되어 있어야 합니다. 네이버 클라우드 플랫폼 [링크](https://www.ncloud.com)를 걸어 놓을게요.

저희가 사용할 서비스는 Simple & Easy Notification Service, 줄여서 SENS입니다. 홈페이지에서 SENS 서비스를 검색하시면 API 특징이나 상세 기능, 요금 등을 볼 수 있어요. 저는 SMS 기능을 사용할 것이고, 한 달에 50건 무료예요. 그럼 저희는 콘솔에서 SENS 프로젝트를 만들어 보겠습니다. 로그인한 뒤, 콘솔로 이동해 SENS 서비스를 눌러주세요.

#### 파라미터 확인

코드를 설명하기 전에, 저희는 SENS API 참조서에서 필요한 파라미터는 어떤 것인지 확인할 거예요. 링크를 걸어 놓을게요. SENS 서비스는 버전 1과 2가 있는데, 1이 얼마 지나지 않아 서비스를 종료한다고 하니 버전 2로 구현하겠습니다. 해당 [URL](https://apidocs.ncloud.com/ko/ai-application-service/sens/sms_v2/)로 들어가시면, 어떤 속성이 mandatory 인지, optional 인지 보실 수 있어요.

API 참조서를 잠깐 볼게요. 아래는 API URL과 요청 헤더에 담을 것들이에요. 아래 사진을 보면서 설명하겠습니다. 우선 아래 사진에 나온 x-ncp-iam-access-key는 포털(콘솔 X)에서의 제가 빨갛게 칠해 놓은 게 액세스 키에요. 바로 아래 사진인데요. 마이페이지 - 인증키 관리에 들어가시면 보이는 access key를 말합니다. 옆에 있는 secret key 도 필요해요.

메시지를 보내는 부분을 보겠습니다. 여기서 API에 접근하기 위한 주소로 쓸 서비스의 ID가 필요해요. 해당 아이디는 그 밑 사진에서 빨갛게 칠해 놓았어요. 해당 키는 콘솔 - SENS 서비스를 누르면, 사용하고자 하는 프로젝트 우측에 서비스 ID가 있을 겁니다. 이걸 사용할 거예요.

이제 헤더는 준비가 끝났어요. 다음으로 요청 바디를 보겠습니다. 바디에 from이라는 속성이 존재합니다. 해당 속성은 문자를 보낼 전화번호를 적는 공간인데요, 이때 전화번호는 SENS에서 인증을 먼저 해주셔야 합니다. 해당 전화번호만 from으로 사용할 수 있어요! 전화번호는 콘솔-SENS-SMS-Calling Number에서 인증할 수 있습니다. 실제 자신의 휴대폰 번호로 인증을 진행하게 됩니다. 이렇게 처리상태가 승인이 되면, 이 번호를 요청 바디에 from으로 사용 가능합니다.

거의 모든 준비가 끝났으니, 코드를 보겠습니다. 위에 API 헤더에서 x-ncp-apigw-signature-v2 요런 속성이 있었어요. 이건 시그니처인데요. API 설명서를 보면 시그니처를 생성하는 방법도 나와있는데 저는 좀 헷갈렸어서 같이 올립니다. 우선 Crypto라는 모듈을 npm 명령어를 통해 설치해 주세요. ★이 들어가 있는 부분에서, uri는 프로젝트의 서비스 ID, secret key와 accress key는 포털에서 얻을 수 있는 계정 key입니다. 시그니처는 Crypto의 SHA256과 Base64를 이용해 만듭니다. 코드에 쓰지 않는 모듈을 변수로 만들어놨는데 저런 건 무시하셔도 됩니다. 저 순서대로 시그니처를 생성하면 되겠습니다.

```
var express = require('express');
var http = require('http');;
var bodyParser = require('body-parser');
var mysql = require('mysql');
var crypto = require('crypto');
var request = require('request');

//create signature2
var CryptoJS = require('crypto-js');
var SHA256 = require('crypto-js/sha256');
var Base64 = require('crypto-js/enc-base64');

//file module
var multer = require('multer');

exports.send = function (req, res) {

	var user_phone_number = req.body.user_phone_number;
	var user_auth_number = req.body.user_auth_number;
	var resultCode = 404;

	const date = Date.now().toString();
	const uri = '본인의 service ID★';
	const secretKey = '본인의 secret key★';
	const accessKey = '본인의 access key★';
	const method = 'POST';
	const space = " ";
	const newLine = "\n";
	const url = `https://sens.apigw.ntruss.com/sms/v2/services/${uri}/messages`;
	const url2 = `/sms/v2/services/${uri}/messages`;

	const  hmac = CryptoJS.algo.HMAC.create(CryptoJS.algo.SHA256, secretKey);

	hmac.update(method);
	hmac.update(space);
	hmac.update(url2);
	hmac.update(newLine);
	hmac.update(date);
	hmac.update(newLine);
	hmac.update(accessKey);

	const hash = hmac.finalize();
	const signature = hash.toString(CryptoJS.enc.Base64);

```

다음 코드부터는 API 헤더와 바디를 만들어 요청을 보낼 거예요. ★에는 아까 콘솔에서 인증한 자신의 휴대폰 번호가 들어가야 해요. 저는 안드로이드에서 유저의 휴대폰 번호와 인증 번호를 보내어 body parser로 파싱 한 뒤 변수에 넣고 content와 to에 적은 것입니다. 헤더와 바디에 아까 생성한 시그니처, key 등을 적절히 삽입하고 보내면 휴대폰으로 문자를 받아볼 수 있습니다.


```
request({
		method : method,
		json : true,
		uri : url,
		headers : {
			'Contenc-type': 'application/json; charset=utf-8',
			'x-ncp-iam-access-key': accessKey,
			'x-ncp-apigw-timestamp': date,
			'x-ncp-apigw-signature-v2': signature
		},
		body : {
			'type' : 'SMS',
			'countryCode' : '82',
			'from' : '인증된 휴대폰 번호★',
			'content' : `WEIVER 인증번호 ${user_auth_number} 입니다.`,
			'messages' : [
				{
					'to' : `${user_phone_number}`
				}
			]
		}
	}, function(err, res, html) {
		if(err) console.log(err);
		else {
			resultCode = 200;
			console.log(html);
		}
	});

	res.json({

		'code' : resultCode
	});

```
---

{{< figure src="jessica-weiller-GAw5wFLVWVo-unsplash.jpg" title="Just chilling on my favorite tree in San Diego Zoo" width="100%" attr="https://unsplash.com/@jweiller?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">}}


For more image processing methods, you can create your own shortcode. Check this [link](https://gohugo.io/content-management/image-processing/) to see what you can do.

--- 

