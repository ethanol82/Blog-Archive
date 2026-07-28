![](https://velog.velcdn.com/images/macncheeeese/post/2f65de4f-e6d8-4c2c-8d6a-7b9030ff5e07/image.png)

다시 왔습니다. 그냥 밥먹고 좀 더 공부할게요 어차피 이번챕터는
하나밖에 없어서..


![](https://velog.velcdn.com/images/macncheeeese/post/4d355811-3b29-4baf-bb49-1e453cfea02c/image.png)

![](https://velog.velcdn.com/images/macncheeeese/post/47af7a41-bf74-4d49-99b0-dc95314ee0c0/image.png)

이런거 만등어봤습니다

이번 챕터(Stacks & Layout)의 핵심 개념:

핵심 개념

- **VStack / HStack / ZStack**: 세로, 가로, 겹쳐서 배치하는 3가지 기본 스택
- **Spacer**: 스택 안에서 빈 공간을 밀어내는 역할 — 요소를 양 끝에 붙이거나 정렬할 때 사용
- **Frame**: .frame(width:height:)로 View의 크기를 직접 지정
- **Border**: .border(.red) 같은 걸로 View의 실제 경계를 눈에 보이게 해서 레이아웃 디버깅
- **Type inference**: Color.red 대신 .red처럼 타입을 생략해도 컴파일러가 추론
- **TabView(.page)**: 페이지 넘기듯 스와이프하는 온보딩 화면

비유: ZStack은 투명 필름 여러 장을 겹쳐놓는 것과 같아요 — 뒤에서부터 순서대로 쌓이고, 위에 있는 필름(View)이 아래를 가립니다. Spacer는 고무줄처럼 늘어나면서 남는 공간을 다 차지해, 다른 View들을 양 끝으로 밀어내는 역할을 해요.