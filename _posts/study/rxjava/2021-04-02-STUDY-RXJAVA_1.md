---
title: RxJava 프로그래밍, 1강 RxJava 소개
date: 2021-04-02 14:00:00 +0900
categories: [Study, RxJava]
tags: [study, reactive, rxjava, java]
comments: true
---

***한빛 미디어에서 출간한 RxJava 프로그래밍 책을 보고 공부한 내용을 정리한 페이지입니다.***<br>
[RxJava 프로그래밍](https://www.hanbit.co.kr/store/books/look.php?p_code=B3448548347)

---

### <span style="color: #aa88aa;">RxJava란?</span>
*   오픈소스 라이브러리
*   자바와 안드로이드를 위한 리액티브 프로그래밍 구현체
*   함수형 프로그래밍의 영향을 받음
*   함수 구성을 선호
*   전역 상태나 부수 효과를 피함
*   비동기나 이벤트 기반 프로그램을 작성할 때 스트림 방식으로 생각 
*   생산자/소비자 콜백을 사용한 옵저버 패턴
*   스케줄링, 스로틀링, 오류처리, 생명 주기 관리를 할 수 있는 많은 연산자 지원
   <br><br>
    
### <span style="color: #aa88aa;">리액티브 프로그래밍이란??</span>
데이터나 이벤트 변화의 반응에 초점을 맞춘 프로그래밍을 뜻하는 일반적인 용어
<br><br>

### <span style="color: #aa88aa;">RxJava vs 함수형 리액티브 프로그래밍</span>
*   FRP(리액티브 프로그래밍)는 리액티브 프로그래밍의 매우 특별한 형태로, 연속적인 시간의 흐름을 포함한다.
*   RxJava(리액티브 익스텐션)은 시간에 대해 불연속적인 이벤트만 다룬다.
<br><br>
    
### <span style="color: #aa88aa;">리액티브 함수형 프로그래밍이란?<span>
*   프로그래밍에 대해 하나의 접근 방식, 즉 명령형 시스템상의 추상화이다.<br>
    (컴퓨터 자체는 명령형으로 동작해야하나, 사람의 사고는 추상화를 거쳐야하므로 )
*   비동기 방식이나 이벤트 기반 요구사항을 구현할 때 컴퓨터처럼 생각하지 않아도 되며 상태들의 복잡한 상호작용을 명령형으로 정의하지 않아도 된다.
*   즉 동시성과 병렬성 해결을 위한 방식이다.
*   리액티브나 비동기 요구사항을 명령형 방식으로 만들었을 때 나타나는 결과물인 콜백 지옥 문제를 해결하기 위한 방법
<br><br>
    
### <span style="color: #aa88aa;">리액티브 프로그래밍이 필요한 환경</span>
1.  본질적으로 비동기성을 띠는 디스크나 네트워크 등 지연 바인딩 I/O 이벤트 응답
2.  서버의 시스템, 이벤트나 앞서 나온 사용자 이벤트 등등 통제 불가능한 어플리케이션에서 발생하는 이벤트나 데이터를 다룰 때
<br><br>
    
### <span style="color: #aa88aa;">단 하나의 이벤트 스트림만 처리하는 경우, 복잡하지 않은 경우</span>
*   명령형 접근 방법이 OS와 언어, 컴파일러 최적화 방식에 훨씬 가깝기 때문에 추상화 단계가 덧붙은 리액티브 프로그래밍 방식보다 효율적이다.
<br><br>
    
### <span style="color: #aa88aa;">RxJava는 어떻게 동작하는가?</span>
*   데이터나 이벤트 스트림을 나타내는 Observable 타입
*   밀어내기(reactive) 방식을 지향하지만 끌어오기(interactive) 방식으로도 사용가능
*   지연 실행되며, 비동기, 동기방식 모두 사용가능
<br><br>
    
### <span style="color: #aa88aa;">밀어내기(reactive)를 통한 이벤트 수신 방식(간략)</span>
*   Observable(데이터 스트림)/Observer를 사용하여 구독할 수 있다.
*   구독을 통해 3가지 종류의 이벤트를 받는다. ( Observer 인터페이스 기본형 )
    1.  onNext
        *   데이터 자체 전혀 호출 안되거나, 한번, 무한대로 호출 가능
    2.  onError
        *   오류(Exception, Throwable)
        *   단 한번만 호출
    3.  onComleted
        *   스트림 완료 통보
        *   단 한번만 호출
<br><br>
            
### <span style="color: #aa88aa;">확장형</span>
*   Producer 끌어오기 타입
*   Subscriber Observer에서 좀더 발전된 인터페이스( Observer 상속중 )
*   unsubscribe: Observable 스트림 구독을 끊을때 사용
*   setProducer: 생산자와 소비자 간의 양방향 소통 채널을 구성할 떄 사용
<br><br>
    
### <span style="color: #aa88aa;">비동기와 동기</span>
*   Observable은 동기 방식으로도 사용이 가능하고, 기본값은 동기 방식
*   명시적 요청이 없다면 RxJava는 동시성 처리를 하지 않는다.
*   동기 방식의 Observable를 구독하면 모든 데이터를 구독자 스레드에서 방출하고 종료
<br><br>
    
### <span style="color: #aa88aa;">메모리 내부 데이터</span>
*   메모리 캐시에 있는 데이터를 비동기로 처리하기 위해 스케줄링 비용을 소모하는 것은 좋은 생각이 아니다.
*   Observable은 단순히 동기 방식으로 값을 가져와 구독 스레드에 값을 방출한다.
<br><br>
    
### <span style="color: #aa88aa;">동시성과 병렬성</span>
*   단일 Observable 스트림은 동시성이나 병렬성 둘 다 허용하지 않는다.
*   대신 여러 비동기 Observable의 조합을 통해 이를 수행한다.
*   병렬성, 동시에 수행하는 작업들
*   동시성, 여러 작업들을 합성하거나 번갈아 수행한다는 뜻
*   하나의 CPU가 여러작업을 실행한다면 동시 실행은 맞지만, 병렬 실행은 아니다.
<br><br>
    
### <span style="color: #aa88aa;">Observable 특징</span>     
1.  Observable 타입은 느긋하다 ( lazy)
2.  다른 곳에서 subscribe 하지않으면 아무것도 하지 않는다
3.  Future와 같이 일단 생성되면 즉시 동작하는 조급한 유형과 다르다
4.  lazy한 방식은 경쟁 조건(race condition)으로 인한 데이터 유실 염려 없이 Observable을 모아 구성할 수 있게 해준다.
5.  Observable은 재사용할 수 있다.<br>
    Future는 재사용 불가, Future 참조 자체가 이미 시작된 일이 있다는 뜻
<br><br>
    
### <span style="color: #aa88aa;">Future대신 Observable을 쓰는 이유</span>
*   이벤트 스트림 또는 다중값 응답을 다룰 수 있기 때문
*   데이터의 종류와 상관없이 Observable로 대신할 수 있다.
<br><br>
    
### <span style="color: #aa88aa;">반환자가 다중이든 단일이든 Observable<Data>인 이유</span>
*   컬렉션 전체가 도착할 때까지 기다리지 않고 항목을 받는 대로 처리할 수 있기 때문
*   롱테일 지연이나 공유 데이터 저장소 때문에 일반적으로 컬렉션 전체를 기다린다면 소비자는 컬렉션에 수집이 끝나는 최대 지연 시간까지 대기해야한다.
*   이것이 가능하려면 서버에서 값을 받는 대로 방출해야 해서 스트림의 순서는 포기해야한다.
*   소비자 입장에서 순서가 중요하다면 랭킹이나 위치 값을 포함해야한다.
<br><br>
    
### <span style="color: #aa88aa;">Single형</span>
*   Observable 대신 Single형을 사용하여 ‘값 하나짜리 스트림’을 나타낼 수 있다.
*   이는 사용자가 오류 응답, 응답 없음, 정상 응답 3가지의 관심사만 고려하면 된다는 심플함을 가져다 준다.
*   기존 Observable에서 고려해야할 점
    1.  오류 응답
    2.  응답 없음
    3.  값이 없는 정상 응답 후 종료
    4.  단일 값 정상 응답 후 종료
    5.  다중 값 정상 응답 후 종료
    6.  하나 이상의 정상 응답 후 종료하지 않음(추가적인 값을 기다리며 대기)
*   따라서 API 사용 측면에서 Single형을 썼을 때 사고 체계가 단순해지며, 개발자가 추가 상태를 고려해야 하는 Observable 구성 과정이 단 한 번만 발생한다.
<br><br>
    
### <span style="color: #aa88aa;">Completable</span>
*   반환형이 없을 때 사용하는 타입
*   그저 처리 결과가 성공인지 실패인지를 나타내는데 사용할 수 있다.
*   Observable<void>, Single<void>의 대체제이다.
*   완료와 실패, 두 개의 콜백 추상화를 가지고 있다.
<br><br>
    
### <span style="color: #aa88aa;">카디널리티 정리</span>
*   Observable = 0부터 무한대
*   Single = 단일 요소 Observable
*   Completable = 구성 요소 없는 Observable
    <br><br>
    
### <span style="color: #aa88aa;">개선을 해야하는 이유</span>
1.  지연 시간과 처리량의 개선은 사용자 경험도 개선하고 인프라 스트럭처 비용을 낮춘다.
2.  이벤트 루프 아키텍처가 부하에 대한 탄력성이 더 좋다.<br>
    부하가 증가할 때 다운되지 않으며 시스템을 한계까지 밀어 붙이면서도 제대로 다룰 수 있다.
3.  이벤트 루프 아키텍처가 더 운영하기 쉽다.<br>
    요청별 스레드 아키텍처는 종종 스레드 풀 크기의 세밀한 조정이 필요한 반면 이벤트 루프 아키텍처는 최적의 성능을 얻기 위해 부하에 따라 조정할 필요가 없다.
4.  위 3가지 그리고 그외의 이유등으로 리액티브 아키텍처를 논블로킹 I/O와 이벤트 루프 형태로 만들어야하는지 이유를 알 수 있다.
    <br><br>
    
### <span style="color: #aa88aa;">RxJava의 타입과 연산자는 명령형 콜백 위에 쌓아올린 추상화이다.</span>
이 추상화는 코딩 스타일을 완전히 바꿔놓으며, 비동기 혹은 논블러킹 프로그래밍을 위한 강력한 도구를 제공한다.
<br><br>

### <span style="color: #aa88aa;">기타</span>
*   Observable 이벤트 생성의 중요한 기준은 블로킹/논블로킹 여부이지 동기/비동기 여부가 아니다
*   RxJava의 Observable은 의도적으로 동기/비동기를 구분하지 않으며, 동시성 여부뿐 아니라 어디서 비롯되었는지도 따지지 않는다.<br>
    의도적으로 설계한 동작으로서 무엇이 최선일지 Observable에서 선택한다.
*   동기 방식 계산<br>
    동기 방식을 유지하는 일반적인 이유는 스트림 조합과 연산자를 통한 변환 때문이다.
*   효율적인 동기 방식 이벤트 연산<br>
    비동기 파이프라인(Observable 구독 방식 )을 선언하고 동기적으로 이벤트를 처리하는 방식 ( 연산자 조합.. map, filter등등 )
*   하나의 Observable 스트림은 항상 직렬화되어 있지만, 각각의 Observable 스트림은 서로 독립적으로 조작할 수 있기 떄문에 동시에 병렬 수행할 수 있다.<br>
    RxJava에서 비동기 스트림을 모아 동시에 수행하기 위해 merge, flatMap을 보편적으로 사용하는 이유이다.
*   new Thread를 통해 Observable 구독 방식을 정하고 두개의 Observable을 따로 호출시키면 순차적으로 두개의 스레드에서 실행<br>
    merge를 통한 구독시키면 한 쓰레드에서 섞여서 실행
*   매우 잘게 나눈 병렬 처리는 가끔 더 느리다. 일반적으로 병렬 처리는 스레드 전환, 쓰레줄링, 재합성 오버헤드를 만회하기 위해 일괄 작업처럼 굵직한 단위로 구행할 필요가 있다.
*   이벤트 스트림에 병렬 연산을 추가할 때마다 거의 항상 추론해 보고 테스트해야한다.
*   명백하게 서로 관련 없는 네트워크 요청을 순차적으로 처리하기보다는 동시에 처리하여 지연 체감을 줄이는 것, 이것이 비동기를 채택하고 구성을 필요로 하는 이유이다.
*   톰캣 vs 네티   
    *   톰캣은 요청별 스레드, 네티는 이벤트 루프방식<br>
        Java8, 일반적으로 사용 중인, 수정하지 않은 톰캣과 네티 ( 비즈니스 로직 영향 제로 )
    *   톰캣은 스레드 풀 구조 때문에 부하가 크면 지연 시간이 늘어나며, 스레드 풀 잠김(잠김 경합) 스레드 마이그레이션이 부하를 가중시킨다.<br>
        ( 요청별로 스레드를 생성하여, 스케줄링을 하기때문에 스레드 마이그레이션 수치가  높다 )
    *   네티의 이벤트 루프 방식은 부하가 걸린 상태에서 스레드 마이그레이션을 줄여주며, CPU 캐시 효율성, 메모리 로컬리티 CPU 명령 사이클 개선 효과, 요청당 CPU 사이클 소비량이 적었다 ( 톰캣에 비해 )<br>
        부하가 낮을때는 두개의 성능은 비슷하다.
        => 부하가 높아지면 성능차이는 엄청나다
