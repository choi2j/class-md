오늘 설명한 비동기 글로 읽기
=============

## 비동기란?

원래 JS 코드를 실행하면 처음에 있는 코드가 먼저 실행되고 다음 코드가 실행되는 방식입니다.

이를 "동기" 라고 하는데,

"비동기"는 "동기"가 아닌 방식으로 코드를 실행한다는 말입니다.

비동기 실행은 코드가 먼저 실행 되었냐 와 관계없이 동시에 실행된다고 생각하시면 됩니다.

이 방식은 비동기로 만든 코드만 해당하고 비동기 방식으로 만들지 않은 코드는 동기 방식으로 실행됩니다.

><br>간단한 예시를 들자면,<br><br>
>식당에 일반 손님과 VIP 손님이 있다고 합시다.<br><br>
>일반 손님은 앞의 손님이 주문을 완료하기 전에는 주문을 할 수 없습니다.<br><br>
>하지만 VIP 손님은 앞에 손님이 있든 없든 주문을 할 수 있습니다.<br><br>

일반 손님은 동기 방식, VIP 손님은 비동기 방식이라고 생각하시면 이해가 될거라고 생각합니다.

그렇다면 이를 코드로 어떻게 작성하는지 알아보겠습니다.

## 비동기 코드 작성

코드를 비동기적으로 실행하고 싶다면 이 코드들을 VIP 로 만들어야합니다.
그 방식은

><br>setTimeout / setInterval<br><br>
>Promise<br><br>
>async / await<br><br>

이 있습니다.

## setTimeout / setInterval

먼저 setTimeout / setInterval 을 보겠습니다.
요 친구들은 이름에 있는 Time 을 기능으로 갖습니다.
먼저 쓰는 방식부터 알아보자면,

```js
setTimeout(() => {코드}, 시간);
setInterval(() => {코드}, 시간);
```

로 그냥 똑같이 코드를 써주면 됩니다.
이 둘은 모두 정해진 시간이 지나면 코드를 실행하는 특징을 가지고 있습니다.
두 코드의 차이점은

setTimeout 은 코드를 1번 실행,
setInterval 은 코드를 무한히 실행 한다는 차이가 있습니다.
setInterval 은 while(1) 을 같은 코드를 가진 setTimeout 코드라고 생각하시면 됩니다.
 
## Promise

Promise 는 비동기로 실행한 코드의 결과를 저장해놓은 객체입니다.
위의 식당 예시를 이어서 하자면,
VIP 손님들이 코드라면, Promise 는 손님들이 한 주문, 즉 코드의 결과라고 생각하시면 됩니다.

그렇다면 이 식당의 주방에서는 주문을 받으면 그 주문에 맞춰 요리를 하겠죠?
이때 이 주문의 상태는

주문에 맞춰 요리를 완료하기 전, 주문에 맞춰 요리를 완료한 후, 주문에 맞춰 요리를 하지 못한 경우

라고 볼 수 있겠지요.
이는 Promise 에서도 똑같이 볼 수 있습니다.

코드 실행 대기, 코드 실행 완료, 코드 실행 실패 또는 오류

이들은 각각 

><br>Pending, Fulfilled, Rejected<br><br>

라고 부릅니다.

쓰는 방식을 알아보자면

```js
const promise = new Promise((resolve, reject) => {코드});
```

입니다.
여기서 resolve 랑 reject 는 각각 코드 실행 성공, 코드 실행 실패 또는 오류 상태를 가리킵니다.

만약 주어진 코드가 성공했다면 resolve 상태가 되어 resovle 결과를 return 하고, 실패했다면 rejecte 상태가 되어 rejecte 결과를 return 합니다.
 
아래는 그 결과를 return 하는 예시 코드입니다.

```js
const promise = new Promise((resolve, reject) => {
   if(resolve) return resolve(“success”);
   else return reject(new Error(“falied”));
})
```

여기서 return resolve, return reject 는 각각 상태를 return 하는 함수로, 괄호 안에는 리턴 값을 넣을 수 있습니다.

그러면 이 결과를 어떻게 확인하는지 보겠습니다.

```js
promise.then((val) => {
   console.log(val);
}).catch((err) => {
   console.log(err);
})
```

promise 를 실행했을 때, then은 성공한 상태, 즉 resolve 상태일 때의 return 값을 받아오고, catch 는 실패 또는 오류 상태, 즉 reject 상태일 때의 return 값을 받아옵니다. 이를 콘솔로 찍는 코드입니다.
 
## async / await

async 와 await 은 promise 를 조금 더 쉽게 쓰기 위해 사용합니다.
async 는 Promise 객체를 return 하는 함수 앞에 붙여줍니다.

* async 사용하기 전
```js
function asyncFunc(state) {
   return new Promise((res, rej) => {
       if(state == 1) return res("1");
       else return rej(new Error("0"));
   })
}
```

* async 사용한 후
```js
>async function asyncFunc(state) {
       if(state == 1) return "1";
       else return new Error("0");
}
```

훨씬 보기 편하다고 생각이 듭니다.

물론 얘도 then, catch 로 결과를 확인할 수 있습니다.

```js
const promise = asyncFunc(0);
promise.then((val) => {
    console.log(val);
}).catch((err) => {
    console.log(err);
})
```

그리고 아직 배우지 않았지만 await 을 쓰면 try, catch 라는 것도 사용할 수 있습니다.

```js
(async () => {
    try {
        const val = await asyncFunc(1);
        console.log(val);
    }
    catch (err) {
        console.log(err);
    }
})
```

각각 결과는 0과 1이 될 겁니다.

하지만 아직 우리는 await 이 뭔지 잘 모르죠.

await 의 기능은 주어진 Promise 객체가 Fulfilled 또는 Rejected 상태가 될 때까지 기다리는 겁니다.

너무 어려운 말이라고 생각되시면 그냥 async 함수의 결과를 받기 위해서는 await 을 써줘야 한다는 겁니다.

await 의 특징은 무조건 async 함수의 안에서 사용할 수 있다는 점입니다.

아래는 이해를 돕기 위한 3개의 함수입니다.

```js
async function settimeoutFunc(delay) {
    return setTimeout(() => {
        console.log("eeeeee");
    }, delay);
}

async function asyncJob(state) {
    if (state == 1) return "resolved";
    else return new Error("rejected");
}

async function asyncFunc() {
    await settimeoutFunc(1000);
    const pro3 = asyncJob(1);

    try {
        const value = await pro3;
        console.log(value);
    } catch (e) {
        console.error(e);
    }

    const pro4 = asyncJob(0);

    try {
        const value = await pro4;
        console.log(value);
    } catch (e) {
        console.error(e);
    }
}

asyncFunc();
```

위의 settimeoutFunc() 는 setTimeout 함수를 return 합니다.

asyncJob() 함수는 state 의 결과에 따라 성공, 실패 여부를 return 합니다.

마지막 asyncFunc() 함수는 안에서 settimeoutFunc() 의 결과를 실행하고,

asyncJob() 의 결과를 pro3 과 pro4 에 각각 담아서 결과를 확인합니다.

맨 위의 
```js
await settimeoutFunc(1000);
```
는
```js
const set = await settimeoutFunc(1000);
console.log(set);
```
과 같다고 보면 됩니다.

- - -

오늘 수업이 많이 부족한 것 같아서 이렇게 코드를 각각 작성해서 문서를 보내드립니다.

다음 수업은 js dom 이 될 예정입니다.