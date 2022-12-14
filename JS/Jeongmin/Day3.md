# JSDAY03

# 목차

### 꼬리 질문) 순수 함수가 뭔가요? 일반 함수와는 어떤 차이가 있죠?

### 실행 컨텍스트에 대해 말해보세요

### 동기와 비동기의 차이점에 대해서 설명해줄 수 있나요?

### 마이크로태스크 큐에 대해서 알고 있나요?

### 태스크 큐와 마이크로태스크 큐 중 어떤 것이 먼저 실행되나요?

---

## 꼬리 질문) 순수 함수가 뭔가요? 일반 함수와는 어떤 차이가 있죠?

순수함수란 외부의 상태를 변경하는 사이드 이펙트가 없고, 동일한 인자가 주어졌을때 항상 같은 값을 반환하는 함수를 뜻합니다  
일반함수일 경우 함수에서 외부의 변수값을 변경하거나 들어온 인자의 값을 변화시키는 부수적인 효과를 일으킵니다.  

## 실행 컨텍스트에 대해 말해보세요.

실행 컨텍스트는 코드를 실행하는데 필요한 환경을 제공하는 객체이자, 식별자 결정을 더욱 효율적으로 하기 위한 수단입니다.  
모든 소스코드는 실행에 앞서 평가 과정을 거치며 코드를 실행하기 위한 준비를 합니다.  
다시말해 자바스크립트 엔진은 소스코드를 2개의 과정 즉 ‘소스코드의 평가'와 ‘소스코드의 실행' 과정으로 나누어 처리하는거죠.  
소스코드 평가 과정에서는 실행 컨텍스트를 생성하고 변수, 함수 등 선언물을 실행하고, 생성된 변수나 함수 식별자를 키로 판단해서 이를 실행 컨텍스트의 스코프에 등록합니다.  
소스코드 평가 과정이 끝나면 런타임이 시작됩니다. 선언문을 제외하고 소스코드가 순차적으로 실행되는거죠.  
이 때 소스코드 평가 과정에서 등록했던 키를 바탕으로 변수나 함수의 참조 등 실행에 필요한 정보를 검색해서 취득합니다.  
이후에 변수 값이 변경되거나, 소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록합니다.  

이 모든 것을 관리하는 것이 바로 실행 컨텍스트입니다. 실행 컨텍스트의 역할엔 크게 세 가지가 있습니다.  
첫 번째로 선언에 의해 생성된 모든 식별자 즉 변수나 함수 등을 스코프로 구분해서 실행 컨텍스트의 스코프에 등록하고, 상태 변화를 지속적으로 관리합니다  
두 번째로 스코프는 스코프 체인을 통해 상위 스코프로 이동하며 식별자를 검색할 수 있습니다.  
세 번째로 현재 실행 중인 코드의 실행순서를 변경 할 수 있어야 하며 다시 되돌아갈 수도 있어야합니다.  

자바스크립트 코드가 실행되기 위해서는 스코프, 식별자, 코드 실행 순서 등의 관리가 필요합니다. 실행 컨텍스트는 소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역입니다.  
좀 더 구체적으로, 실행 컨텍스트는 식별자(변수, 함수, 클래스)등을 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 매커니즘으로, 모든 자바스크립트 코드는 실행 컨텍스트를 통해 실행되고 관리됩니다.  
식별자와 스코프는 실행 컨텍스트의 렉시컬 환경으로 관리하고, 코드 실행 순서는 실행 컨텍스트 스택으로 관리합니다.  

### 꼬리질문 -> 실행 컨텍스트 스택이란?

자바스크립트 엔진은 먼저 전역 코드를 평가하여 전역 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시합니다. 이떄 전역 변수나 전역 함수는 실행 컨텍스트에 등록됩니다. 이후 전역 코드가 실행되기 시작하면서 전역변수에 값이 할당되고, 전역 함수가 호출됩니다.  
전역 함수가 호출되면 전역 코드의 실행은 일시 중단되고 코드의 제어권이 함수 내부로 이동합니다. 엔진은 또다시 함수 내부의 코드를 평가하고 함수 실행 컨텍스트를 생성하며 이를 실행 컨텍스트 스택에 푸시합니다. 이때 지역변수가 있다면 지역변수를 함수 실행 컨텍스트에 등록합니다. 이후 함수 코드가 실행되면서 지역변수에 값이 할당됩니다.  
만약 중접 함수가 있다면 동일한 과정을 반복합니다. 함수의 호출과 실행까지 모두 마무리 되었다면 더이상 실행할 코드가 없으므로 함수는 종료됩니다.  
이후 함수가 종료되면 코드의 제어권은 다시 전역 코드로 이동합니다. 자바스크립트 엔진은 실행이 종료된 함수 실행 컨텍스트를 스탭에서 팝하여 제거합니다.  
그리고 더이상 실행할 전역 코드가 남아있지 않으면 전역 실행 컨텍스트도 실행 컨텍스트 스택에서 팝되어 실행 컨텍스트는 아무것도 남아있지 않게 됩니다.  
이처럼 실행 컨텍스트 스택은 코드의 실행 순서를 관리합니다. 소스 코드가 평가되면 실행 컨텍스트가 생성되고, 실행 컨텍스트 스택의 최상위에 쌓입니다. 이때 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행 중인 코드의 실행 컨텍스트입니다.  
실행 컨텍스트 스택에서 함수 실행 컨텍스트가 제거되었다고 해서 렉시컬 환경까지 즉시 소멸 되는 것은 아닙니다. 렉시컬 환경은 실행 컨텍스트에의해 참조되긴 하지만 독립적인 객체입니다.  
객체를 포함한 모든 값은 누군가에 의해 참조되지 않을 때 비로소 가비지 컬렉터에 의해 메모리 공간의 확보가 해제되어 소멸합니다.  

## 동기와 비동기의 차이점에 대해서 설명해줄 수 있나요?

자바스크립트는 싱글 스레드 기반의 언어이고, 자바스크립트 엔진은 하나의 호출 스택만을 사용합니다.  
이는 요청이 동시다발적으로 오더라도 동기적으로 처리되며, 한 번에 한 가지 일만 처리할 수 있음을 의미합니다.  
즉 자바스크립트는 단일 스레드(싱글 스레드), 동기 언어입니다.  

메모리 힙과 콜스택은 자바스크립트 엔진의 주요 구성 요소입니다.  
메모리 힙이란 변수와 메모리 할당을 담당하는 곳을 뜻합니다. 콜스택이란 실행컨텍스트 스택이라고도 말합니다.  
자바스크립트에서 함수를 호출하면 이 콜스택이라는 곳에 호출 순서대로 차곡차곡 쌓이게 됩니다. 그리고 맨 마지막에 호출된 함수부터 먼저 반환됩니다. 먼저 들어온것이 먼저 나가는 List in First Out 방식으로 처리되는거죠.  
함수가 순서대로 푸시되서 쌓이고 팝되어 사라지는 과정을 동기라고 부릅니다.  

하지만 만약에 앞에서 실행중인 함수의 처리 시간이 오래 걸린다면 동기적 특성을 지니고 있는 자바스크립트로 작성된 웹 페이지는 이 동작이 끝날 때까지 화면에 제대로 렌더링 되지 않거나, 다음 동작을 수행하는데 지장을 주게 될것입니다.  
이러한 자바스크립트의 단일 스레드, 동기 방식을 보완하기 위해 구현된 처리 방식을 비동기라고 부릅니다.  
비동기는 어떠한 요청을 보내면 그 요청이 끝날 때까지 기다리는 것이 아니라, 응답에 관계없이 바로 다음 동작이 실행되는 방식을 뜻합니다.  

자바스크립트는 어떻게 여러 이벤트를 동시에 동작하게 할 수 있는걸까요?  
사실 여러 동작이 한꺼번에 실행 되는 것이라 아니라 특정 함수가 종료되지 않았어도 대기 하지 않고 다음 코드를 실행하는 자바스크립트의 특성이기 때문에 가능한겁니다.  
자바스크립트 엔진 밖에서도 자바스크립트에 관여하는 요소들이 있습니다. 런타임은 특정 언어로 만든 프로그램들을 실행할 수 있는 환경입니다.  
Node.js나 크롬등의 브라우저들은 자바스크립트가 구동되는 환경이기 때문에, 이를 자바스크립트 런타임이라고 합니다. 런타임 환경에서는 자바스크립트 엔진 자체가 제공하지 않는 DOM 조작이나 AJAX같은 비동기 처리를 위한 web API를 제공하고 있습니다.  
또 이를 제어 하기 위해 이벤트 루프나 태스크 큐 등이 존재합니다.  

자바스크립트에서 비동기로 호출되는 함수들은 콜스택에 쌓이는 것이 아니라 태스크 큐로 보내집니다.  
기본적인 함수들은 호출시 자바스크립트의 콜스택에 푸시되며, 동작이 완료되면 팝되어 콜스택에서 사라집니다.  
하지만 비동기 함수는 자바스크립트 엔진이 처리하지 않고 Web API가 처리합니다. 예를들어 setTimeout이 있습니다. 콜스택에 쌓인 비동기 함수인 setTimeout은 Web API에게 콜백 함수를 전달하고, setTimeout 작업을 요청합니다.  
이후 성공적으로 Web API에 전달 이후엔 콜스택에서 팝되서 사라지게 됩니다. 콜스택 상의 작업이 마무리 되면 이때 Web API는 setTimeout 작업을 시작합니다. 설정한 시간이 지나면 태스크 큐로 콜백 함수를 전달합니다.  
해당 콜백 함수를 쌓이면 실행을 해야하는데, 자바스크립트 엔진은 언제나 콜스택을 바라보고 있습니다. 현재 태스크 큐로 전달된 콜백 함수는 콜스택에 없으므로 해당 함수를 실행 할 수 없습니다.  
이때 이벤트 루프가 동작하게 됩니다. 이벤트 루프는 콜스택이 비어있으면 태스크 큐에서 함수를 하나씩 꺼내 콜스택에 넣고 실행합니다.  
콜스택에 푸시되어 쌓인 콜백 함수는 실행을 마치면 팝되서 사라지게 되고 함수 실행은 종료됩니다.  

## 마이크로태스크 큐에 대해서 알고 있나요?

태스크 큐란 콜스택을 통해 비동기 함수를 호출 할 때 콜백 함수들이 대기하는 큐 형태의 배열입니다.  
태스크 큐에는 두 가지 종류가 있습니다.  
매크로 태스크 큐 통칭 태스크 큐와 마이크로 태스크 큐입니다. 이 둘은 서로 별도의 큐라고 볼 수 있습니다.  
마이크로 태스크 큐에는 프로미스의 후속 처리 메서드의 콜백 함수가 일시 저장됩니다.  
그 외의 비동기 함수의 콜백 함수나 이벤트 핸들러는 태스크 큐에 일시 저장됩니다.  

## 태스크 큐와 마이크로태스크 큐 중 어떤 것이 먼저 실행되나요?

콜백 함수나 이벤트 햄들러를 일시 저장하는 점에서 태스크 큐와 동일하지만 마이크로 태스크큐는 태스크 큐보다 우선순위가 높습니다.  
즉 이벤트 루프는 콜 스택이 비면 먼저 마이크로태스크 큐에서 대기하고 있는 함수를 가져와 실행합니다 렌더링 작업도 마치고 태스크 큐로 간다. 이후 마이크로 태스크 큐가 비면 태스크 큐에서 대기하고 있는 함수를 가져와 실행합니다.  
