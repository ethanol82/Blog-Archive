![](https://velog.velcdn.com/images/macncheeeese/post/9e8056d6-ae8f-4e5f-90ec-e7bf07b1d2b3/image.png)

## 오늘 할 것 ^

![](https://velog.velcdn.com/images/macncheeeese/post/c6402151-b719-4eba-abe1-5afc0dc762d6/image.png)

## Default value

처음부터 나타난 중요한것

> 초기값을 선언하냐 안하냐는 인스턴스 관리에 매우 중요함. 
초기값을 선언하게 되면 인스턴스에 프로퍼티값을 굳이 선언하지 않아도 됨. (자동으로 초기값으로 설정됨)

>var 와 let의 차이: let은 인스턴스 생성 시 값을 줬을 때 변경이 불가능함. var은 변경이 가능함. 변수와 상수의 차이라고 보면 될 듯.

- let 프로퍼티: 초기값이 없으면 인스턴스 생성 시 반드시 값을 줘야 하고, 한 번 정해지면 이후 못 바꿈.
- var 프로퍼티: 초기값이 없으면 마찬가지로 인스턴스 생성 시 값을 줘야 하지만, 이후에 다시 값을 바꿀 수 있음.
- var + 초기값: 인스턴스 생성 시 값을 생략 가능 (기본값 사용), 나중에도 바꿀 수 있음.


## .resizable()

이미지의 크기를 조정하고 싶을 때 사용하는 modifier
이미지를 넣었을 때는 .frame을 써도 수정이 불가능함. 그럴 때 .resizable 을 쓰면 수정 가능. 

```
Image(systemName: "die.face.3")
    .resizable()
    .frame(width: 100, height: 100)
```

### 주의할 점
- .resizable을 쓰면 이미지 비율을 하나도 안맞게 찌그러질 수도 있음.
- 비율 유지하려면 **.aspectRatio(contentMode: .fit)** 같이 써줌

```
Image(systemName: "die.face.3")
    .resizable()
    .aspectRatio(contentMode: .fit)
    .frame(width: 100, height: 100)
```

## @State

tutorial 을 따라하는데 문제가 생겼다. 버튼을 누를때마다 numberOfPips 라는 프로퍼티의 값이 랜덤하게 바뀌고, 그 값에 따라 주사위 사진이 뜨도록 해놨는데, 오류가 떴다. 

이 문제를 **@State** 라는 문법으로 해결하라고 한다.

>@State는 SwiftUI에서 **"이 값이 바뀌면 화면을 다시 그려라"** 라고 알려주는 특별한 표시(property wrapper)예요.

var property의 값이 바뀌어도 SwiftUI는 그걸 감시하고있지 않기 때문에 변화에 맞춰 body가 바뀌지 않는다. 그렇기 때문에 @State를 붙여서 프로퍼티 값이 바뀌는 순간 body를 다시 그려내게 한다.

```
@State private var numberOfPips: Int = 1
```

### 주의할 점

- @State는 그 View가 직접 소유하는 값에만 써야 해요 (그래서 **private** 을 붙임).

### private
지역변수 정도의 느낌으로 볼 수도 있지만 엄연히 다르다. 
프로퍼티에 붙는다는 점부터 다름.
private으로 프로퍼티를 선언하게 되면, 해당 프로퍼티가 포함된 구조체 바깥에서는 아예 접근이 불가해짐. 

>@State는 "이 View 혼자 관리하는 비밀 상태"라는 전제로 설계된 도구라서, 그 전제를 깨고 남이 건드릴 수 있게 두면 SwiftUI의 데이터 흐름 원칙(단방향 데이터 흐름) 자체가 무너지기 때문에, private으로 반드시 잠가두는 거예요.

## ForEach

![](https://velog.velcdn.com/images/macncheeeese/post/68bc46de-42e4-4f93-87b2-84d5c4b860dc/image.png)

이런걸 만드는데

```
HStack {
   ForEach(1...3, id: \.description) {_ in
   	   DiceView()
}
```
뭐 무슨 이상한 문법을 가져다쓰는거임;;

> ForEach: 	컬렉션에 있는 각 요소마다 View를 반복해서 하나씩 만들어라

1...3 이니까 3번 클로저 안에 있는 View를 만들어라 이거임

### id 어쩌고는 뭐임?
각 view를 구분해야하니까 고유한 식별자(identifier)를 만들어야하는데 \.description 을 써서 그냥 문자열 1, 2, 3을 identifier로 쓴다는 소리

### 클로저 안에 이상한 소리는 뭐임?
ForEach는 각 반복에서의 값을 파라미터로 받음. 근데 지금을 파라미터가 필요가 없으니까
> 받기는 받는데 안쓸게요 ㅅㄱ

라는 뜻에서 **_** 를 쓴다고 함(언더바)

숫자로 받는 예시를 들면 
{number in ...} 라고 하고 number가 1,2,3순서대로 들어옴 
약간 for문 같은느낌

## .disabled

![](https://velog.velcdn.com/images/macncheeeese/post/b543d871-4ff1-46b6-83a9-e5be7210d6d6/image.png)

버튼을 추가해서 주사위 갯수를 늘리고 줄이려고 했는데 점점 줄이다 0개가 되니까 이렇게 말을 안들음 crash 발생

왜냐하면 아까 그 ForEach 문에서 레인지다 **1...0** 이 된거임
그래서 
>갯수가 1일때는 버튼을 비활성화 하자!

그래서 .disabled modifier를 사용함

```
Button("Remove Dice") {
   withAnimation {
       numberOfDice -= 1
   }
}                
.disabled(numberOfDice == 1)
```

이렇게 쓰시면됩니다.

## Label

```
Button("Add Dice", systemImage: "plus.circle.fill") { ... }
```

이렇게 버튼에는 이니셜라이저로 텍스트와 이미지를 받아놨다.
가독성때문에 이미지만 보이고 싶다.
텍스트를 지우면 된다. 

>텍스트는 VoiceOver(스크린 리더) 같은 접근성 기능을 위해 항상 존재해야 해요. 시각장애인 사용자는 아이콘 모양을 못 보니까, "Add Dice"라는 텍스트를 음성으로 읽어줘야 하거든요.

그래서 이니셜라이저로는 다 받아두고
.labelStyle(.iconOlny) modifier으로 스크린에는 아이콘만 띄워둔다.

![](https://velog.velcdn.com/images/macncheeeese/post/47c1fff2-e62f-4485-8922-ba1de15efcb0/image.png)

### 오늘은 이런거 만들어봤습니다

**클로드가 정리해줌**
오늘 배운 것 (DiceView 만들기)

1. 커스텀 View 분리

반복되는 UI를 재사용 가능한 DiceView 구조체로 분리

2. 프로퍼티 기본값

var x = 1 처럼 기본값을 주면 initializer에서 생략 가능 (let/var 여부와 무관)
var는 "나중에 재할당 가능"하다는 뜻이지, 초기값 필수 여부와는 별개 개념

3. .resizable()

이미지가 .frame() 크기에 맞춰 늘어나도록 허용하는 modifier

4. 클로저(closure)

이름 없이 코드를 변수처럼 담아 나중에 실행하는 코드 블록
Button("Roll") { ... }의 { } 부분이 클로저 (trailing closure syntax)

5. @State

SwiftUI에게 "이 값 바뀌면 화면 다시 그려라"고 알려주는 property wrapper
struct는 원래 자기 프로퍼티를 클로저 안에서 못 바꾸는데(self is immutable), @State가 이를 가능하게 해줌
private을 붙여 View가 자기 상태를 직접 소유·관리하도록 캡슐화

6. modifier 체이닝 위치

Swift는 들여쓰기가 아니라 {}, ., () 구조로 문법을 판단
.buttonStyle()은 Button(...) { } 전체(완성된 View)에 붙는 것이지 클로저 내부나 부모 스택에 붙는 게 아님

7. ForEach

for문과 비슷하게 반복하지만, 동작을 실행하는 게 아니라 View들을 생성하는 것이 목적
ForEach(1...3, id: \.description) { _ in DiceView() } → 숫자 값은 안 쓰고 _로 무시, DiceView 3개 생성

8. .labelStyle(.iconOnly)

텍스트+아이콘이 있는 Label에서 화면엔 아이콘만 보여주고, 텍스트는 VoiceOver 접근성용으로 남겨둠
