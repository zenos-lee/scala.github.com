---
layout: overview-large
title: 들어가며..

disqus: true

partof: collections
num: 1
language: ko
---

**Martin Odersky, and Lex Spoon**

많은 사람들이 보기에, 스칼라 2.8의 가장 눈에 띄는 변화는 바로 새로운 컬렉션 프레임워크이다. 사실, 이전에도 스칼라에 컬렉션이 있었지만 2.8 버전부터 컬렉션을 일관되고 통일성 있게 제공하는 프레임워크로 자리매김하게 되었다. (이전 버전과 대부분 호환됨)

비록 처음에 컬렉션에 추가된 변화가 미미해보일지라도, 프로그래밍 스타일에 큰 변화를 가져올 수 있다. 컬렉션 각각의 요소를 이용한 것이 아닌 컬렉션 전체를 이용함으로써, 마치 더 고차원적인 프로그램을 작성하는 것처럼 느낄 것이다. 이 새로운 스타일에 익숙해지기 위한 시간이 필요하지만, 다행히 새로운 컬렉션의 특징 덕분에 쉽게 적응할 수 있다. 새로운 컬렉션은 쉽게 사용할 수 있고, 짧게 사용할 수 있으며, 안전하고, 빠르고, 통일성이 있다.  

**편리함:** 20-50개의 메소드로 구성된 몇가지 간단한 작업만으로 대부분의 컬렉션 문제를 풀기에 충분하다. 복잡한 루프 구조나 재귀적인 방법을 사용할 필요가 없다. 영속적인(persistent) 컬렉션들과 부작용없는 연산들(operations)은 새로운 데이터로 인한 컬렉션의 갑작스러운 손상을 걱정하지 않게 해준다. 이터레이터와 컬렉션 사이의 간섭은 사라지게 되었다. 

**간결함:** 단어 하나만으로 하나 이상의 루프를 표현할 수 있다. 또한, 큰 노력 없이도 간단한 구문과 연산들의 조합을 통해서 대수학을 커스터마이징하듯이 함수 연산들을 작성할 수 있다.   

**안전함:** 이는 실제로 경험해보지 않으면 알기 어렵다. 스칼라 컬렉션의 정적타입과 함수형이라는 특성은 대부분의 에러가 컴파일 시점에 잡힐 수 있음을 의미한다. 이러한 주장에 대해 다음과 같은 근거를 들 수 있다. 

(1) 프로그램은 대량의 컬렉션 연산을 통해서 충분히 테스트된다. <br>
(2) 컬렉션 연산은 입력과 출력을 함수 파라미터와 연산 결과에 대응시킨다. <br>
(3) 입력과 출력값들은 모두 정적 타입 검사를 수행한다. 

결론적으로, 대다수의 잘못된 사용은 타입 에러를 내게 한다. 한 번에 몇 백줄의 코드를 실행시킬 수 있는 것은 더이상 특이한 경우가 아니다. 

**빠름:** 컬렉션 연산들은 라이브러리들 안에서 튜닝되고 최적화된다. 그렇기 때문에 컬렉션을 사용하는 것은 꽤 효율적이다. 신중하게 직접 수정한 자료구조와 연산을 통해서 좀 더 나아질 수도 있지만 이를 구현하는 과정에서 최적화된 방법으로 구현되지 않은 몇몇 코드들이 더 나아지지 못하게하는 걸림돌이 될 수 있다. 게다가 컬렉션은 최근에 멀티 코어에서의 병렬처리 기능을 적용했다. 병렬처리를 지원하는 컬렉션은 일반적인 컬렉션과 같은 연산(operation)을 사용하기 때문에 새로운 연산을 배울 필요도 없고, 코드를 새로 작성할 필요도 없다. 그저 `par` 메소드를 사용하는 것만으로 병렬처리 기능을 사용할 수 있다. 

**통일성:** 컬렉션은 어떤 타입에 대해서도 같은 연산을 제공한다. 이를 통해 적은 어휘로 표현된 연산으로 많은 기능을 구현할 수 있다. 예를 들어, string은 개념적으로 문자들의 시퀀스이다. 따라서, 스칼라에서의 string은 모든 시퀀스 연산을 제공한다. 이는 배열에도 똑같이 적용된다.  

**예시:** 다음은 스칼리 컬렉션의 많은 장점을 한줄로 표현한 코드이다. 

    val (minors, adults) = people partition (_.age < 18)

보자마자 이 연산이 어떤 기능을 하는지 단번에 알 수 있다. 이 연산은 `people` 컬렉션을 그들의 age에 따라서 `minor`와 `adults`로 나눈다. `partition` 메소드가 루트 컬렉션 타입인 `TraversableLike`에 정의되어 있기 때문에, 이 코드는 배열을 포함한 어떤 종류의 컬렉션에서도 작동할 수 있다. 결과값인 `minor`와 `adults`도 `people` 컬렉션과 같은 타입을 갖는다. 

이 코드는 기존에 3개의 루프를 필요로 하는 기존의 컬렉션 프로세싱보다 훨씬 더 간결하다. (기존의 컬렉션 프로세싱은 중간 결과를 임시 저장하기 위해 3개의 루프를 사용하게 된다.) 기본적인 컬렉션 어휘들을 한번 배운 적이 있다면, 이 코드가 기존의 루프를 사용한 방법보다 훨씬 더 쉽고 안전하다는 것을 알 수 있다. 게다가 `partition` 연산은 꽤 빠르고 멀티코어와 병렬 컬렉션에서는 더 빠른 결과를 제공할 수 있다. (병렬 컬렉션은 스칼리 2.9의 한 부분으로 릴리즈되었다.)  

이 문서는 사용자 관점에서 스칼라 컬렉션 라이브러리 API에 대해 자세하게 설명한다. 모든 기본적인 클래스와 메소드들을 알아보자.   