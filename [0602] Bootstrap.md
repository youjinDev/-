###6/2 수요일 수업

[프론트엔드 실무 팁]
- font 스타일링은 초반보다는 나중에 하는 것이 좋음
- <br>과 &nbsp 사용은 지양하고 <div>나 margin 속성으로 구현하는 것이 좋음

[이미지]
- img-fluid 
- img-thumbnail : 테두리에 박스 쳐주기
- rounded : 모서리 살짝 둥글게

[테이블]
- 부트스트랩에서 table class를 주면 부모 가로 길이 100% 점유 =>윈도우창에 꽉 차게 하지 않으려면 table 위에 부모 태그 필요
- thead, tbody가 웹표준이므로 꼭 쓰기 => 향후 버그를 줄일 수 있음
- table-hover : 마우스 올리면 특정 효과 발생
- table-responsive : 테이블 부모에 선언,  더 넘어가지 않게 wrapping 해주는 역할

[컴포넌트]
- Carousel 사용시 그 안에 있는 이미지 사이즈 동일하게 제작할 것
- form-control 클래스 사용시 너비 강제로 100% 점유 => 사이즈를 따로 지정시 이슈 발생 => 이 form이 속해있는 부모 컨테이너를 조작하기 (부모에 form-inline)