---
title: "동기 VS 비동기 , Promise 이해하기"

categories:
 - server
 - vuejs
tags:
 - rest api 
 - vuejs
 - promise
 - restful api
last_modified_at: 2020-10-14T08:06:00-05:00
---
**동기(Syncronous)**는 요청을 보낸 후 해당 요청의 응답을 받아야 다음 동작을 실행하는 방식.  
**비동기(Asuncronous)**는 요청을 보낸 후 응답과 관계없이 다음 동작을 실행 할 수 있는 방식을 의미한다.  



자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미한다.  


비동기 처리의 가장 흔한 사례는 제이쿼리의 Ajax이다. 제이쿼리로 실제 웹 서비스를 개발할 때 Ajax 통신으로 해당 데이터를 서버로부터 가져올 수 있다. 콜백함수로 비동기 처리 방식의 문제점 해결하기.



## Promise
'promise'는 자바스크립트 비동기 처리에 사용되는 객체이다. 프로미스를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 프로미스의 상태이다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미한다. new Promise()로 프로미스를 생성하고 종료될 떄까지의 3가지 상태를 갖는다.
1. *pending(대기)* : 비동기 처리 로직이 아직 완료되지 않은 상태.
2. *fulfilled(이행)* : 비동기 처리가 완료되어 프로미스가 결과값을 반환해준 상태.
3. *Rejected(실패)* : 비동기 처리가 실패하거나 오류가 발생한 상태

#### 1.1. pending(대기)
new promise() 메서드를 호출하면 대기(pending)상태가 된다. new promise() 메서드를 호출할 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자는 resolve, reject이다.  


#### 1.2. fulfilled(이행)
콜백 함수의 인자 resolve를 아래와 같이 실행하면 이행(fulfilled)상태가 된다. 이행 상태가 되면 then()을 이용하여 처리 결과 값을 받을 수 있다.  
*프로미스의 이행 상태를 좀 다르게 표현해보면 완료이다.*  


#### 1.3. rejected(실패)
reject를 호출하면 실패 상태가 된다. 실패 상태가 되면 실패한 이유 (실패 처리의 결과 값)을 catch()로 받을 수 있다.   


<br/>

## 프로미스의 에러 처리방법
실제 서비스를 구현하다 보면 네트워크 연결, 서버 문제 등으로 인해 오류가 발생할 수 있따. 따라서, 프로미스의 에러 처리 방법에 대해서도 알고 있어야 한다.
1. then()의 두번째 인자로 에러를 처리하는 방법
```
getData().then(
handleSuccess,
handleError
);
```
2. catch()를 이용하는 방법.
```
getData().then().catch()
```  


두가지 방법 모두 프로미스의 reject()메서드가 호출되어 실패 상태가 된 경우에 실행된다. 프로미스의 로직이 정상적으로 돌아가지 않는 경우 호출된다. 가급적 catch()로 체러 처리를 하는게 더 효과적이다.  



## promise vuejs 사용예시
로그인 api 요청시,
1. NetworkUtils.js
```javascript
LOGIN: function(params) {
        return new Promise(function(resolve, reject) {
            axios
                .post("http://localhost:3500/v1/signin", params, {
                    headers: { 'x-accept-type': 'operator' }
                })
                .then(res => {
                    console.log(res)
                    if (res.data.code === 0) {
                        resolve(res.data)
                    } else {
                        reject(res.data.msg)
                    }

                })
                .catch(err => {
                    //alert('이메일과 비밀번호를 확인하세요')
                    console.log(err)
                });
        })
    },
```
2. store actions
```javascript
actions: {
        //로그인 시도
        signin({ dispatch }, params) {
            return NetworkUtils.LOGIN(params).then((res) => {
                console.log(res)
                let token = res.data
                    //토큰을 로컬스토리지에 저장
                localStorage.setItem("x-auth-token", token)
                dispatch("getMemberInfo")
                alert("로그인이 되었습니다.")
            }).catch(res => {
                alert(res),
                    console.log(res)
            });
	}
```

예외처리 custom message를 서버에서 전달해주고 클라이언트에서 받아주기 위해서 필요한 기능이다.

#### Reference
[https://backback.tistory.com/395?category=704721](https://backback.tistory.com/395?category=704721)
