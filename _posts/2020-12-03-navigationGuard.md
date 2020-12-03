---
title: "네비게이션 가드"

categories:
 - vuejs
tags:
 - vuejs
 - 네비게이션 가드
last_modified_at: 2020-12-02T08:06:00-05:00
---
### 네비게이션 가드
 : 뷰 라우터로 특정 url에 접근할 때 해당 url의 접근을 막는 방법.
 예를 들면 사용자의 인증정보가 없을시, 특정 페이지에 접근하지 못하도록 차단할 때 사용하는 기술
 * 전역 가드: 애플리케이션 전역에서 동작하는 Ex) beforeEach() 
 * 라우터 가드: 특정 url에서만 동작하는 Ex) beforeEnter, beforeRouteEnter, beforeRouteLeave
 * 컴포넌트가드 : 라우터 컴포넌트 안에 정의하는

#### 전역가드
```javascript
router.beforeEach(function(to, from, next)){

});
```
 * to: 이동할 url 정보가 담긴 라우터 객체.
 * from: 현재 url 정보가 담긴 라우터 객체.
 * next: to에서 지정한 url로 이동하기 위해 꼭 호출해야 할 함수.  

router.beforeEach()를 호출하고 나면 모든 라우팅은 대기상태.
원래 url이 변경되고 나면 url에 따라 화면 전환이 이루어저야 하는데 전역 가드를 설정해서 화면이 전환되지 않는다. 여기서 해당 url()로 라우팅 하기위해서는next()호출이 필요하다.

```javascript
router.beforeEach((to, from, next) => {
    next()
        if(to.matched.components!==undefined){
            if(to.matched.some( (item)=> item.components.meta.superAdmin)){
                if(myAuth===authType.SUPERADMIN){
                    next();
                }
                else{
                    alert("권한이 없습니다.");
                    next(-1);
                }
            }
            else{
                next()
            }
        }
        else{
            next()
        }
})
```
superadmin의 권한을 가지고 있는 유저만 해당 화면에 접근할 수 있다.  
.some()은 자바스크립트 내장 API. 저장된 배열의 모든 요소를 검사하여 조건을 만족시키면 true값을 반환하고 아니면 false값을 반환한다.  


#### 라우터 가드
```javascript
{
        path: '*',
        beforeEnter: (to, from, next) => {
            next('/login')
        }
    }
```
특정 라우팅에 대해서 가드를 설정하는 방법.  


#### 컴포넌트 가드
```javascript
const Login = {
	template: '<p>Login Component<p>'
	beforeRouteEnter (to, from, next){
		//Login컴포넌트가 화면에 표시되기 전에 수행될 로직.
		//Login컴포넌트는 아직 생성되지 않은 시점.
	},
	beforeRouteUpdate (to, from, next){
		//화면에 표시된 컴포넌트가 변경될 때 수행될 로직
		//this로 Login컴포넌트를 접근할 수 있다
	},
	beforeRouteLeave (to, from, next){
		//Login 컴포넌트를 화면에 표시한 url값이 변경되기 직전의 로직
		//'this'로 Login컴포넌트를 접근할 수 있다
	}
}
```
## reference
[https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/)
