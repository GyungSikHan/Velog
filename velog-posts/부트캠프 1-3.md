<h2 id="레벨-디자인이란">레벨 디자인이란?</h2>
<hr />
<p>게임 내에 플레이어가 경험할 수 있는 환경 구조를 만드는 과정</p>
<p>시각적 요소의 배치를 넘어 플레이어 경험의 핵심을 설계하는 역할</p>
<h2 id="플레이어-캐릭터-만들기">플레이어 캐릭터 만들기</h2>
<hr />
<blockquote>
<p>💡플레이어 캐릭터는 게임 내에 사용자가 조종을 하는 핵심 오브젝트</p>
</blockquote>
<h3 id="캐릭터-클래스-만들기">캐릭터 클래스 만들기</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d199208f-e9c7-4953-bc76-341f6c788691/image.png" />

<p>블루프린트에서 캐릭터를 누르면 캐릭터를 누르게 되면 자동으로 캐릭터가 생성이 된다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/aa1a1230-1682-4f1d-b834-8be61205d3b2/image.png" />
그 안을 들어가 살펴보면 현재 아무런 메쉬가 없이 캡슐 컴포넌트 하나만 존재하게 될 것이다</p>
<h3 id="매시-추가">매시 추가</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3fbc3fff-0eaf-41fe-bb18-d6a3c2a6deab/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/80dc7870-1d02-4c94-a535-8b2f9153d5b1/image.png" />


<p>스켈레탈 메시에서 메시를 선택하면 캐릭터를 원하는 형태로 만들 수 있다</p>
<p>이때 캡슐 컴포넌트의 위치에 맞춰 캐릭터 메시를 맞춰줄 수 있다</p>
<h3 id="카메라-및-spring-arm">카메라 및 Spring Arm</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1f1e55de-88b8-4bda-804e-12b4ea8afe45/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ec0be3df-7420-4902-9990-a0d427e3c08f/image.png" />


<p>SpringArm과 Camera를 추가하게 되면 플레이어 뒤에 카메라가 생기며 게임 실행 시 우리가 아는 그 화면으로 보일 수 있게 된다</p>
<blockquote>
<p>💡SpringArm
카메라를 제어하는데 사용하는 컴포넌트로 캐릭터와 캐릭터 사이의 거리를 일정하게 유지 시켜준다
또한 카메라가 벽이나 장애물에 충돌할 때 자동으로 카메라의 위치를 조정할 수 있게 해줌으로 카메라가 벽이나 장애물을 통과하지 않고 캐릭터를 보여주게 해준다
플레이어가 회전하거나 빠르게 움직일 때 카메라가 자연스럽고 부드럽게 캐릭터를 따라 움직이게 해준다
bUsePawnControlRotation 옵션을 통해 플레이어 입력애 따라 카메라 회저을 제어할 수 있게 해준다
Socket Offset과 Target Ofsset을 통해 카메라의 정확한 위치를 미세 조정이 가능하다</p>
</blockquote>
<h3 id="입력---move-look">입력 - Move, Look</h3>
<blockquote>
<p>💡Enhanced Input System
Unreal Engine 5 버전으로 바뀌면서 입력을 맵핑하는 방법이 바뀌었다</p>
</blockquote>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/fb15c748-9445-46d2-90ba-b88bd7a755aa/image.png" />
향상된 입력 방법은 입력매핑 컨텍스트와 입력 액션 추가하여 커스텀하여 입력을 할 수 있게 해준다

<blockquote>
<p>💡입력 액션과 입력 매핑 컨텍스트</p>
</blockquote>
<ul>
<li>입력 액션<ul>
<li>게임에서 수행할 수 있는 특정 동작을 정의하는 역할을 한다</li>
<li>설정<ul>
<li>Value Type: 입력 값의 타입을 지정한다</li>
<li>Triggers : 입력이 언제 발생할지 결정한다(누를 때, 때었을 때 등)</li>
<li>Modifiers : 입력 값을 변형 시킬 수 있다(반전, 스케일 조정 등)</li>
</ul>
</li>
</ul>
</li>
<li>입력 매핑 컨텍스트<ul>
<li>여러 입력 액션을 그룹화하고 특정 키나 버튼에 매핑하는 역할을 한다</li>
<li>기능<ul>
<li>입력 액션을 하나의 컨텍스트로 묶을 수 있다</li>
<li>런타임 중 컨텍스트를 추가하거나 제거할 수 있어 상황에 따른 입력 관리가 용이하다</li>
</ul>
</li>
</ul>
</li>
</ul>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3c433592-c3d3-4db1-9376-aef4cf523462/image.png" />
Move, Look 입력 액션은 모두 X, Y축을 사용하므로 Value Tyep에 Axis2D로 설정을 해준다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ca8a4059-0875-48f6-af00-455c3db55b56/image.png" />
입력 매핑 컨텍스트에서 입력 액션을 추가한 뒤 특정 키로 맵핑을 해줄 수 있다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f44c32a2-e91f-4015-84ea-3204303e24a7/image.png" />

<p>이동은 하나의 입력 액션을 사용해 4개의 버튼으로 사용하기 때문에 모디파이어를 변경해주어야 한다</p>
<p>W는 앞으로 가는 키로 기본 값으로 설정을 해주고 S는 W와 반대로 움직여야 하므로 모디파이어에 부정으로 설정하여 들어오는 값의 -를 곱해 뒤로 이동할 수 있게 해준다</p>
<p>A와 D는 좌우로 움직여야 하는데 이때 스위즐 입력 축 값을 사용하면 들어오는 입력의 축 값을 바꿀 수 있다</p>
<p>이때 Unreal은 왼손좌표계를 이용하므로 오른쪽으로 이동하는 것이 + 값이므로 A에 부정을 추가해준다</p>
<h3 id="캐릭터-회전">캐릭터 회전</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7f7f8082-3c89-44b7-8923-072be1b8dc9a/image.png" />


<p>캐릭터 블루프린트 클래스로 돌아와 만들어준 입력 액션중 Look을 콜하여 return해주는 벡터 값을 핀분할을 통해 분해해준다</p>
<p>이때 X 값은 Add Controller Yaw Input에 Y 값은 Add Contoller Pitch Input에 넘겨주는대 X 값을 Yaw인 Z 축에 넘겨주는 이유는 마우스가 X 축으로 이동할때 카메라의 Z축을 회전시켜 마우스가 이동하는 방향으로 카메라를 비추기 위해서이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/149bba73-b7ee-40ac-8b39-b0f8b983ef1f/image.png" />


<p>디테일 페널에서 컨트롤러 피치 및 요를 사용하는 것을 체크하여 움직여보자</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cdfccbb2-25ff-4343-89cd-15819051195d/image.png" />


<p>카메라가 회전할 때 그 방향으로 캐릭터도 같이 움직이면서 원하는 움직임이 나오지 않을 것이다</p>
<p>그 이유는 컨트롤러 회전 사용은 캐릭터 전체와 연결이 되어있기 때문이다</p>
<p>따라서 두개다 체크 해제를 해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/563dc440-456c-4b9a-ac38-fb9565ef5dc6/image.png" />

<p>다시 돌아와 캐릭터 무브먼트 컴포넌트를 선택 후 무브먼트 방향으로 회전 조정에 체크를 해보자</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b20875a3-0903-45aa-8803-ba2735ff3c99/image.png" />


<p>또한 SpringArm 컴포넌트의 폰 제어 회전 사용도 체크해준다</p>
<p>이렇게 되면 우리가 알고있는 게임의 카메라 회전과 비슷하게 나올것이다</p>
<p>하지만 Y 축 회전 시 애플의 스크롤 처럼 움직이게 되는 것을 볼 수 있다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/4f95e935-f66c-4625-a14c-34c9bc9bf38d/image.png" />

<p>이것을 고치기 위해 입력 매핑 컨텍스트에 Look을 찾아 모디파이에 부정을 추가해준다</p>
<p>이때 인덱스를 펼치면 축에 따라 값을 적용할지 안할지 설정할 수 있는데 이때 Y축 값만 체크하여준다</p>
<p>이제 플레이를 하게되면 우리가 알고있는 게임의 카메라 회전과 동일하게 움직이는 것을 볼 수 있다</p>
<h3 id="캐릭터-움직이기">캐릭터 움직이기</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f5bc0bc3-504d-494c-827f-4c68d7474f5c/image.png" />


<p>입력 액션으로 만든 Move를 가져와 Value 값을 핀분할 해 각각 Add Movement Input 함수에 넣어준다</p>
<p>Add Movement Input은 엔진 내에서 제공하는 함수로 들어오는 Float 값과 Vector 값을 통해 움직임을 제공해준다</p>
<blockquote>
<p>💡
Controller Rotation을 이용하는 이유!!
캐릭터의 움직임은 카메라가 현재 바라보는 방향을 기준으로 움직인다
예를 들어 카메라가 플레이어의 오른쪽 방향을 바라보고 있을 때 캐릭터가 앞으로 움직인다 생각해보자
그러면 캐릭터는 카메라가 바라보는 방향을 기준으로 회전하여 움직일 것이다
이러한 기능을 위해 Controller Rotation을 가져와 사용하는 것이다</p>
</blockquote>
<blockquote>
<p>☝Forward Vector, Right Vector
Foward Vector
앞뒤 움직임에서 Controller의 회전 값 중 Z 값을 가져와 Forward Vector에 Z 값만 넣어 Vector 값으로 만들어주게 되는데 여기서 의문점이 생겼다
왜 Z 축 값이며 Forward Vector인가
Controller Rotation에서 설명한 내용을 가지고 생각해보자
일단 Forward Vector에 대해 알아야 한다
이는 X축이 1이고 나머지는 0인 Vector(1,0,0) 인 방향 벡터이다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/dad2272f-0f9a-48f5-86d1-0c5d5682d132/image.png" />
그림을 보고 생각을 해보자 각각의 축을 기준으로 Forward Vector를 구한 뒤 앞으로 움직이게 되면 이동하게 될 방향을 그린 그림이다
이처럼 Z 축이 아닌 다른 축으로 Forward Vector를 만들어 연산하면 카메라 회전에 따라 땅에 박히거나 하늘로 날라가는 등 잘못된 움직임을 보일 것이기 때문에 Z 축 값을 넣은 것이다
Right Vector
Right Vector는 Y축이 1인 Vector(0,1,0)인 방향 벡터이다
Forward Vector에서 설명한 것처럼 Z,X축을 기준으로 Right Vector를 만든 이유도 동일한 이유이다</p>
</blockquote>
<h2 id="배운-것을-토대로-jump-만들어보기">배운 것을 토대로 Jump 만들어보기</h2>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/5058c470-5866-48f9-ad8d-af56a6e949a0/image.png" />

<p>점프는 엔진 내에서 제공하는 Jump 함수를 사용하면 된다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/92807d87-7612-4f6f-ae03-714ec9544575/image.png" />

<p>입력 액션을 가지고 Jump를 만들어준 뒤</p>
<p>입력 매핑 컨텍스트에 Jump 를 추가해 준 뒤 스페이스 키로 맵핑해준다</p>
<p>그 뒤 캐릭터 블루프린트에서 입력 액션과 Jump 함수를 연결해주면 완성이 된다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7651b739-4ff4-419d-94ee-f2e72d492665/image.png" />

<h2 id="숙제--공책에-간단한-레벨-디자인하기">숙제 : 공책에 간단한 레벨 디자인하기</h2>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/dac82e8c-3d78-4141-9b95-ad99ebdbadec/image.png" />

<p>점프와 이동으로 도착지점까지 함정들을 피해 이동하는 느낌으로 그림</p>