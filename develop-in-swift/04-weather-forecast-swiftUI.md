![](https://velog.velcdn.com/images/macncheeeese/post/755ab160-5991-48f8-9a76-1a93eb48f3f8/image.png)

SwiftUI 만지기 단계로 레전드 점프하고 시작하겠습니다..

그냥 배운 내용중에 생각나는거만 끄적이는 노트 정도로 쓰겠습니다
오늘은 코드 쓰는거라..

## View
part of the interface of an app
View 와 Data는 독립적임
EX. ```Text```(View)  ,```String```(Data)

### View Library
단축키: shift+command+L

## Modifier
.으로 연결함.
![](https://velog.velcdn.com/images/macncheeeese/post/befbbb10-791b-4a37-9782-1839bee77485/image.png)
![](https://velog.velcdn.com/images/macncheeeese/post/ead1741e-7b9c-4861-89c0-a3daa4f9d1ce/image.png)
![](https://velog.velcdn.com/images/macncheeeese/post/ea73aa85-8da1-4b6c-a1d6-ecd3a8ffda3e/image.png)
![](https://velog.velcdn.com/images/macncheeeese/post/cc575944-30c2-4fa4-8812-bfa434467d46/image.png)


>modifier 순서에 따라 view가 달라지더라~![](https://velog.velcdn.com/images/macncheeeese/post/02acb8b8-c485-466b-beaa-6d9f3434d514/image.png)

## Property

![](https://velog.velcdn.com/images/macncheeeese/post/09107889-5fd2-4156-af68-32c493d6d75a/image.png)

음.. 여기는 변수를 property라고 하는건가요..?
약간 의미가 다른거같긴한데
일단 property라고 알고 있겟습니다

![](https://velog.velcdn.com/images/macncheeeese/post/25b46fea-a03b-44f6-9be5-88220e2f3792/image.png)

구조체를 하나 만들고 그걸 불러서 쓸 때 반드시 property를 넣어줘야 합니다

![](https://velog.velcdn.com/images/macncheeeese/post/b341bed5-9cf4-42f7-9751-eaa42be24086/image.png)

```
struct DayForecast: View {
    let day: String
    let high: Int
    let low: Int
    
    var body: some View {
        VStack {
            Text(day)
            Image(systemName: "sun.max.fill")
                .foregroundStyle(Color.yellow)
            Text("High: \(high)º")
            Text("Low: \(low)º")
        }
        .padding()
    }
}
```

int 형을 text에 넣는다? text view는 string 을 내놓기 때문에 
>"\(int)" 로 넣어줘야한다~

>The order of parameters in the initializer matches the order of declaration of their matching properties, so you can’t add the new arguments at the end, as you did before. **파라미터 순서 맞출 것**

### computed vs stored protperty

stored property
는 let으로 선언함

computed propert
는 var로 선언함. 

>A computed property doesn’t store a value directly like the stored properties


핵심 개념

- **Structure(struct)**: 코드와 데이터를 하나의 재사용 가능한 단위로 묶는 도구. DayForecast 같은 커스텀 View도 사실 struct임
- **Initializer**: struct의 property에 값을 채워서 인스턴스를 만드는 과정 — DayForecast(day: "Mon", high: 75, low: 60) 처럼
- **Property**: 각 인스턴스를 서로 다르게 만드는 값 (같은 struct 틀이지만 property 값이 다르면 다른 결과)
- **Computed property**: 저장된 값이 아니라 조건에 따라 "계산해서" 반환하는 property — var temperatureColor: Color { high > 80 ? .red : .blue } 같은 형태

비유: struct는 쿠키 틀(cutter)과 같아요. 하나의 틀(struct 정의)로 여러 쿠키(인스턴스)를 찍어내지만, 각 쿠키마다 다른 토핑(property 값)을 올릴 수 있죠. Computed property는 쿠키를 굽고 난 뒤 "온도가 몇 도 이상이면 색이 변한다"는 규칙을 정해두는 것과 비슷합니다.

![](https://velog.velcdn.com/images/macncheeeese/post/e04d1df4-357a-4a89-8050-5cb0e0940538/image.png)

일단 ㅇ이걸 만들었고요

![](https://velog.velcdn.com/images/macncheeeese/post/f9bd7e78-64ef-431f-8f2e-65d1e32ab1fa/image.png)

이렇게 만들어봤슴다

### 깃헙에 올려놓고 있음. 오늘은 여기까지. 성한전 코드리뷰하고 좀 공부해놔야함