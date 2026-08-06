![](https://velog.velcdn.com/images/macncheeeese/post/ea6be8ac-ecfa-4275-9f35-d95e0140e524/image.png)

## List
```
List {
   Text("Elisa")
   Text("Andre")
   Text("Jasmine")
   Text("Po-Chun")
}
```

![](https://velog.velcdn.com/images/macncheeeese/post/c8cb63ea-91e5-4aea-8298-9119926daa61/image.png)

>A List view adds other views to the content in its body, like separators between rows and visual elements such as rounded corners and backgrounds.

List View 는 포함된 다른 view를 이미지처럼 줄과 도형으로 구분하여 보여준다.

```
struct ContentView: View {
    @State private var names: [String] = ["Elisha", "Andre", "Jasmine", "Po-Chun"]
    
    var body: some View {
        VStack {
            List {
                ForEach(names, id: \.description) {name in
                    Text(name)
                }
            }
        }
        .padding()
    }
}

#Preview {
    ContentView()
}

```

이런 식으로 @state 를 사용해서 문자열 리스트를 생성하고, ForEach 문으로 리스트 뷰를 생성할 수 있다.

**@State 를 쓰는 이유는 저 이름 리스트를 동적으로 이용할 거기 때문. **

## TextField

```
TextField("Add Name", text: $nameToAdd)
```
list view 밑에 이런 코드를 추가햇음.
```
@State private var nameToAdd = ""
```
이런 프로퍼티도 선언함.

### 그게뭔데
>**TexField**:사용자가 텍스트를 입력할 수 있는 UI 컴포넌트 (한 줄짜리 입력창). 

>**text: $nameToAdd** :
- $ 기호는 Binding을 만드는 문법임. $nameToAdd는 nameToAdd라는 @State 변수에 대한 "양방향 연결 통로"를 의미함.
- 이 바인딩 덕분에 사용자가 텍스트필드에 타이핑하면 → 그 값이 실시간으로 nameToAdd 변수에 자동 반영된다. 반대로 코드에서 nameToAdd를 바꾸면 → 텍스트필드에 보이는 내용도 바뀜 ㅇㅇ.
- 만약 $ 없이 그냥 text: nameToAdd라고 썼다면, 그건 값을 한 번 읽어오기만 하는 것(one-way)이라 사용자가 입력해도 변수가 업데이트되지 않아요 — 컴파일 에러가 날 거예요, TextField는 바인딩을 요구하거든요.

### 외우자 TextField 는 binding($)을 요구함

![](https://velog.velcdn.com/images/macncheeeese/post/294374ae-0e1e-4199-8103-66cf6611274c/image.png)

이렇게 됨

## .onSubmit

```
TextField("Add Name", text: $nameToAdd)
    .onSubmit {
        names.append(nameToAdd)
        nameToAdd = ""
```

.onSubmit modifier 로 textField에서 받은 string을 names list 에 append 함.

## .autocorrextionDisabled

textfield 에서 문자열을 입력할때 자동완성 기능을 끄는 modifier

## ternary conditional operater (삼항연산자)

```
Text(pickedName.isEmpty ? " " : pickedName)
```

Vstack 에 이 코드를 추가함.
여기에는 삼항연산자 문법이 사용되었음. 간단히하면 조건문을 한 문장으로 줄이는 문법

![](https://velog.velcdn.com/images/macncheeeese/post/9c0ff71f-0716-4335-b266-141452f68099/image.png)


## Optional Binding

```
Button("Pick Random Name") {
    if let randomName = names.randomElement() {
        pickedName = randomName
    } else {
        pickedName = ""
    }
}
```

이런 코드를 추가했음. 

- ```names.randomElement``` : 배열 ``names``에서 무작위로 요소를 하나 뽑는 메서드. 근데, 반환타입이 ```String```이 아니라 ```string?```임. 왜냐면 배열이 비어있으면 ```nil```를 반활할수도 있기 때문임.
- ```if let randomName = names.randomElement() { ... }``` 이게 **optional binding** 이라는 문법.

- ```names.randomElement()```가 ```nil```이 아닌 실제 값을 반환하면 그 값을 ```randomName```이라는 상수에 "언래핑(unwrap)"해서 담고 ```{...}```안의 코드 실행

- ```nil```이 반환되면 ```if``` 문 건너뛰고 ```else```문 실행됨.

- ```randomName``` 은 ```if```문 내의 지역상수임.

### Swift에서는 옵셔널 값(String?) 을 안전하게 처리하지 않고 그냥 쓰면 컴파일 에러가 발생할 수 있음.


## Divider()

![](https://velog.velcdn.com/images/macncheeeese/post/5ebfd627-8768-4032-80d3-6151dcfeaca3/image.png)

사이에 선을 넣어서 구분을 해준다.

List뷰는 그걸 자동으로 해줌

## Binding22

```
Toggle("Remove when picked", isOn: $shouldRemovePickedName)
```

이런 코드를 추가함
근데 isOn 뒤에 왜 저 변수를 바인딩하는거임?
>클로드왈: **$shouldRemovePickedName은 단순히 값을 읽기만 하는 게 아니라, "이 변수를 읽고 쓸 수 있는 권한" 자체를 Toggle에게 통째로 넘겨주는 거예요.**

```
struct Binding<Value> {
    let get: () -> Value          // 값을 읽는 방법
    let set: (Value) -> Void      // 값을 쓰는 방법
}
```

이렇다고 함.
바인딩하면 저런 함수를 알아서 할당하는듯
신기한게 얘네는 함수타입 프로퍼티를 선언할수 있음 독특함

>**```isOn: $shouldRemovePickedName```: 스위치를 켜고 끄면 shouldRemovePickedName이라는 @State 변수가 실시간으로 true/false로 동기화돼요.**

그리고 또 코드를 추가했음
```
if shouldRemovePickedName {
    names.removeAll { name in
        return (name == randomName)
    }
}
```
**토글이 켜져 있으면(true), 뽑힌 이름을 리스트에서 삭제하는 로직이 실행됨**

### removeAll{}
이게 구라같긴한데 names 배열에서 하나씩 꺼내서 클로저에 보여준다고 함
진짜 구라였음 
클로저 안에 파라미터에 배열의 한 값씩 돌아가면서 넣어줌. 그리고 클로저 안에 조건에 맞는거는 지우는 메서드였음
함부로 AI믿지 맙시다 여러분들 팩트체크 해야함

return은 굳이 없어도됨 그래서 지움 나는

## 개선

![](https://velog.velcdn.com/images/macncheeeese/post/ef94425a-1525-4e57-9051-4058597d2736/image.png)

같은 이름을 적으면 리스트에 추가되지 않도록 만들었음.

```
if !nameToAdd.isEmpty && !names.contains(nameToAdd)
```

onSubmit 에 딸린 if문 조건에 조건을 더 추가해서 이름이 겹치는걸 1차로 걸러줬음.
근데 문제는 그러면 텍스트필드에 적힌 텍스트가 사라지지 않는다는거임.
그리고 나는 알림을 띄워주려고 했음.
위에 사진에 보이는것처럼

그래서 변수하나 만듬
```
@State private var showDuplicateAlert = false
```

```
else if names.contains(nameToAdd) {
	showDuplicateAlert = true
    nameToAdd = ""
                    }
```

이거를 if문 밑에 추가했음. 이러면 알림 띄울수있다. 그리고 nameToAdd를 비워서 텍스트필드도 깔끔하게 지웠음.

```
.alert("Alert", isPresented: $showDuplicateAlert) {		Button("Got it") {}
} message: {
	Text("This name is dulpicated.")
 }
```

알림은 이렇게 띄움


### \#오늘은 여기까지 