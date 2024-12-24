<h2 id="캐릭터-애니메이션-적용">캐릭터 애니메이션 적용</h2>
<hr />
<h3 id="애니메이션-블루-프린트">애니메이션 블루 프린트</h3>
<blockquote>
<p>☝애니메이션 블루프린트란?
시불레이션 또는 게임 플레이 도중  스켈레탈 메시의 애니메이션을 제어하는 툿그 블루피린트이다
그래프는 애니메이션 블루프린트 에디터 안에서 편집되며, 애니메이션 블렌딩을 하거나 스켈레톤의 본을 제거하거나, 사용할 스켈레탈 메시의 최종 애니메이션 포즈를 정의할 로직을 생성할 수 있다</p>
</blockquote>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a60753c9-dcd2-44f1-9426-d2c1e1089606/image.png" />

<p>애니메이션을 추가하기 위해 애니메이션 블루프린트로 생성을 한다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/00bec44b-2d6d-4dfa-819a-bb4498c40f81/image.png" />

<p>이때 스켈레톤을 설정하여 어떤 뼈에 대한 애니메이션을 설정할 것인지를 선택하는 것이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7ed09bd9-d1e3-4af9-b044-fb26684f3ff2/image.png" />

<p>애니메이션을 블루프린트로 끌어와 Output Pose에 연결해준 뒤 컴파일을 누르게 되면 애니메이션이 적용이 된다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ef37a7e1-f5d0-4812-b984-5323f871a757/image.png" /></p>
<p>이제 적용할 블루프린트 클래스에 매쉬 설정에 들어가 애님 클래스에 애니메이션 블루프린트를 넣어주면 그 클래스에 적용이 될 것이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/29835ee2-a64e-40fb-ad4c-c50859335138/image.png" />


<p>적용이 된 모습니다</p>
<h3 id="블렌드-스페이스">블렌드 스페이스</h3>
<blockquote>
<p>☝블렌드 스페이스란?</p>
<ul>
<li>애님 크래프에서 샘플링 할 수 있는 특수 에셋</li>
<li>입력되는 값에 따라 다수의 애니메이션을 블렌딩 하는 복잡한 작업 가능 
블렌드 스페이스 1D</li>
<li>하나의 입력값에 따라 애니메이션을 블렌딩 시켜주는 것
블렌드 스페이스</li>
<li>두 입력 값에 따라 애니메이션 블렌딩을 시켜주는 것</li>
</ul>
</blockquote>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/75dcc580-cbb4-4044-8d1e-748729e3a26a/image.png" />

<p>우리는 하나의 값으로 멈춰있거나 달리는 기능을 만들 것이므로 블렌드 스페이스 1D를 사용하여 애셋을 만들어준다</p>
<p>값을 받을 이름을 지정해 주고 값의 최소 최대 값을 지정해 준 뒤 분할 될 그리드 수까지 설정해준다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/604f10cc-a466-4581-a875-6b8260305385/image.png" /></p>
<p>그렇게 하면 사진처럼 그리드에 들어온 값에 따라 애니메이션을 설정할 수 있게 된다</p>
<p>애니메이션을 원하는 위치에 넣어주면 값에 따라 애니메이션이 나오며 중간 값에는 애니메이션이 잘 섞여 중간 애니메이션을 그릴 수 있게 해준다 </p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/8205321f-62ba-40f3-a64e-5a3f5dc8360d/image.png" />


<p>다시 애니메이션 블루프린트로 돌아와 애님 그래프에서 블렌드 스페이스를 연결시켜 준 뒤 Speed라는 float 형 변수를 연결해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/90d46035-a3ba-4bb8-8c46-d697ed0f0ab1/image.png" />

<p>위의 사진처럼 노드를 연결하면 애니메이션 블루프린트를 가진 Pawn에게서 현재 속도를 가져오고 그를 float형 변수 Speed에 저장해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/61b3d94a-3ad4-4d53-b4de-b3c8cff822c5/image.png" />



<p>이렇게 하면 속도에 따라 뛰거나 멈춰있는 애니메이션이 섞여 잘 나오는 것을 볼 수 있다</p>
<blockquote>
<p>☝
IsValid 함수
이 함수는 들어온 값이 Null인지 아닌지를 판단하여 결과에 맞는 노드를 연결할 수 있게 해주는 노드이다</p>
</blockquote>
<h2 id="액터-이동">액터 이동</h2>
<hr />
<h3 id="회전하는-액터">회전하는 액터</h3>
<p>먼저 블루프린트 클래스로 액터를 만든다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ca663a8a-663b-4e23-b8d1-012dc7d8a73a/image.png" />
Tick 변수를 통해 매 틱에 float형 변수를 곱해주고 그 값을 AddActorLocalRotation에 Z 값에 넣어준다

<p>이렇게 하면 물체가 Z축에 + 방향으로 float 변수에 설정한 값을 속도로 회전을 하게된다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cc73e11d-c86c-4b21-b7aa-a99225221f61/image.png" /></p>
<p>회전하는 방향을 바꾸기 위해서 Float형 변수에 -값을 곱해 저장해주면 - Z 축으로 회전시킬 수 있다</p>
<blockquote>
<p>☝Add Actor Local Rotation
Add Actor Local Rotation 함수는 액터의 회전을 변경 시켜주는 함수이다
이때 Add Actor World Rotation 함수도 존재하는데 이는 World를 기준으로 회전을 변경하는 함수이다
Local은 자기 자신이 가진 축을 말하며 두 함수 중 의도한 대로 알맞게 잘 사용해야 된다 </p>
</blockquote>
<h3 id="이동하는-액터">이동하는 액터</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/8b6f8852-966a-4ad4-b572-1a72a01e15b9/image.png" />

<p>새로운 블루프린트 액터를 만들어 준 뒤 3개의 변수를 만들어 준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/558fd2cc-7574-4a6d-850f-721958d35e40/image.png" />

<p>Event Begin Play 함수를 사용하여 게임 시작 시 액터의 위치를 가져와 Start Location 변수에 저장해 준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cc4584bd-a0ba-40ba-a102-ea27afb0b3d5/image.png" />
Tick 함수에서 매 시간 일정한 속도만큼 변하기 위해 Platfrom Velocity 변수와 곱해준다

<p>이 값을 다시 Gat Actor Locaton 함수와 더해주면서 액터의 현재 위치에서 Platfrom Velocity 값 만큼 매 시간 변하게 된다</p>
<p>이를 Set Actor Location 함수에 넣어주면 액터의 위치가 실시간 변하게 된다</p>
<blockquote>
<p>☝
Set Actor Location</p>
<ul>
<li>이 함수는 현재 액터의 위치를 변화시켜주는 함수이다
Event Tick</li>
<li>이 함수는 매 프레임마다 호출이 되는 함수로 실시간으로 변화하는 기능을 만들 때 사용한다</li>
<li>너무 남발하여 사용하면 게임의 성능 저하를 일으킬 수 있으므로 잘 사용해야 한다</li>
</ul>
</blockquote>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/98c7a0a5-af08-4b45-b216-9e01844617d1/image.png" />


<p>이번엔 특정 위치에 도달하면 반대로 이동하는 기능을 만들기 위해 if 문을 사용해 줄 것이다</p>
<p>현 위치와 시작 지점을 저장한 Start Location 변수 사이의 거리를 반환해주는 Distance 함수를 사용하여 Move Distance와 비교해 그 값보다 크거나 같은지 판단해 true라면 Platfrom Velocity에 Negate Vector를 Platfrom Velocity에 저장하여 반대 방향으로 이동할 수 있게 만들 수 있다</p>
<blockquote>
<p>☝
Distance To</p>
<ul>
<li>이 함수는 두 벡터간에 거리를 float형 변수로 리턴해주는 함수이다
Negate Vector</li>
<li>이 함수는 들어온 벡터에  -1을 곱한 값을 리턴하는 것으로 벡터의 방향을 반대로 바꾸는 함수이다</li>
</ul>
</blockquote>
<h2 id="overlap">Overlap</h2>
<h3 id="ice-발판-만들기">Ice 발판 만들기</h3>
<hr />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/5d9c8d7b-b6f0-4de3-8d88-32bee9f0d6d3/image.png" />

<p>액터의 움직임을 보간하기 위해 무브먼트 컴포넌트에 보간을 추가한다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f306c126-5b84-4533-a542-0dec77b78413/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/04f71c50-a751-40e7-9eb7-ce9904b2f979/image.png" />
무브먼트 컴포넌트에 보간 속성을 보면 컨트롤러 포인트에서 X,Y,Z를 셋팅해 움직임을 제어할 수 있다

<p>또한 비헤이비어 타입을 변경하여 동작 방식을 변경할 수 있다</p>
<blockquote>
<p>☝비헤이비어 타입 종류
One Shot : 목표 지점까지 가면 정지
One Shot Reverse : 목표 지점까지 가면 돌아가서 정지
Loop Reset : 끝까지 가면 처음으로 돌아감
Ping Pong : 반복적으로 시작과 끝을 왔다 갔다 하며 선형보간함</p>
</blockquote>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/e1242607-38dc-4548-9327-64c21a2f6331/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/49f67226-8cba-4c3b-be3a-e7ced717e629/image.png" />
액터에 Box Collision을 추가한 뒤 원하는 크기로 맞춰준다

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7d9e403d-f3af-4ad1-bfad-f66843eaac48/image.png" />

<p>추가한 Collision을 이용해 OnComponentBeginOverlap을 사용하면 액터와 다른 액터가 충돌 시 이 함수가 호출된다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cc18baf3-c99f-40b0-8d44-884eb19b1dfd/image.png" />

<p>Other Actor는 충돌된 액터로 Other Actor와 현재 액터와 같은지 판단한 뒤 같지 않다면 Other Actor를  BP_Player로 캐스팅한다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7a7c695e-ddf1-4918-80f7-54265fb304dd/image.png" />

<p>캐스팅이 된다면 Character Movement 컴포넌트를 가져와 지면 마찰과 감속 걷기 제동의 값을 변경하여 플레이어가 이 액터와 충돌한다면 얼음처럼 미끄러운 액터를 만들 수 있다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b4533948-1b82-4ca8-b470-9742a22e4c98/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/94111d43-695d-4f84-90b6-2476b4be02d4/image.png" />
하지만 상태가 변화하면 충돌하지 않아도 계속해서 미끄러지듯 움직임을 가져가게 된다

<p>이를 방지하기 위해  OnComponentEndOverlap을 이용하여 BP_Player의 Movement 상태를 원래대로 돌려줘야 한다</p>
<h2 id="이벤트">이벤트</h2>
<p>Overlap이란 ‘겹쳤을 때 발생’ 하는 이벤트이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1a58b722-14b6-49c2-af6c-14f2cdce3f8f/image.png" />

<p>이를 사용하기 위해 트리거 볼륨을 사용해 볼 것이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/2a136e15-c4c4-4b51-b6fc-6353a755cbe6/image.png" />

<p>트리거 볼륨을 월드에 배치해보자</p>
<p>게임 실행 시 액터가 트리거 볼륨 영역에 들어오게 되면 이벤트를 발생 시킬 것이다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/0cd47109-6f17-49e6-8112-a8630f613a34/image.png" />

<p>이 트리거 볼륨의 충돌을 사용하기 위해 레벨에서 트리거 볼륨을 선택 후 레벨 블루프린트에서 Add Actor Begin Overlap 함수를 호출해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d49a8a77-1690-4783-a2bd-f109c57b635f/image.png" />

<p>그 후 BP_Player를 레퍼런스로 생성한 뒤 Other Actor와 같다면 Hello라는 문자열을 출력하게 만들어준다</p>
<p>이렇게 되면 BP_Player가 트리거 박스와 충돌하게 되면 Hello라는 문자열을 출력한다</p>
<h3 id="timer-이벤트">Timer 이벤트</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/17c2e6c3-ec96-47e9-bec1-869ec55c92ff/image.png" />
이제 액터에 float형 Time 변수를 만들어보자

<p>그 후 눈 모양을 누르게 되면 눈을 뜨는 표시로 바뀌는데 이는 전역에서 사용할 수 있는 public과 같은 의미이다</p>
<p>이걸 켜주게 되면 블루프린트에서 직접 값을 변경하지 않고 레벨에 배치된 액터 개개인의 값을 바꿀 수 있게 된다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1320ed55-5b09-474e-bde4-4dc2b32d5a1f/image.png" />

<p>먼저 Tick 함수를 통해 매 프레임 Time에 Delta Seconds를 뺀 값을 셋팅하여 0보다 작거나 같게 되면 액터를 지우는 노드를 만들었다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/50bd3ec4-31c0-452d-9535-f5c2861206a7/image.png" />

<p>이때 Time에 Delta Secons를 빼고 Time이 0보다 작거나 같은지를 판단하는 과정을 만들어 놓은 블루프린트 함수가 Delay 라는 함수이다</p>
<p>Delay 함수를 사용해 보기 위해 Event BeginPlay 함수에 Delay 함수를 연결해 Time 변수를 넘겨준다</p>
<p>그 후 Destory Actor 함수를 연결하면 Time의 시간이 지난 뒤 액터가 사라지는 것을 볼 수 있다</p>
<h3 id="축을-중심으로-회전--부딪힌-액터-튕겨내기">축을 중심으로 회전 + 부딪힌 액터 튕겨내기</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/6a2f4a4a-1869-41d0-bb0c-9cb3d2f33b60/image.png" />

<p>새로운 액터를 만들어 Mesh와 float형 Radius, Speed 변수를 만들어준다</p>
<p>Radius는 가상 축 까지의 거리(반지름) - 기본 값 700</p>
<p>Speed는 속도 - 기본 값 100</p>
<p>으로 설정해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/4184c5d1-b010-4737-b31f-f6a69f446437/image.png" />

<p>제자리에서 액터가 돌게 만들어 준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3f4545f9-55a8-4cfe-b569-aaf3a9497f17/image.png" />

<p>이때 지금까지와 다르게 Local 축에서 회전하는 것이 아닌 월드에 가상 축을 기준으로 회전을 하게 만들것이다</p>
<p>따라서 Set World Location 함수를 이용해 줄 것이다</p>
<p>가상의 축을 기준으로 만들기 위해 GetActorLocation을 가져와 X 축 값만 따로 빼 Radius와 더한 값을 벡터로 만들어준다</p>
<p>Event BeginPlay에 SetWorldLocation 함수를 연결해주고 조금 전 만든 벡터와 Mesh를 연결해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/94e57769-765d-4e02-965e-4e5ba4c2b091/image.png" />

<p>액터가 World의 가상 축을 기준으로 잘 회전을 한다</p>
<p>하지만 액터와 충돌시 밀어내지 못하고 통과하는 것을 볼 수 있다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3ba2cb22-998b-402e-a455-c2e58781c235/image.png" />

<p>다시 블루프린트로 돌아와 Mesh의 OnComponentHit를 호출해준다</p>
<p>이 이벤트는 액터와 다른 액터가 충돌시 호출된다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7fa1264f-f875-497a-a449-d540448e18ad/image.png" />

<p>Hit 정보를 펼쳐 HitNormal을 이용해 Character를 날릴 힘을 설정해 준 뒤 Launch Character에 연결해준다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/684ff9d7-ce05-4d40-bc4b-0d7620352d72/image.png" />

<p>이렇게 되면 회전하는 액터에 충돌시 캐럭터가 멀리 날아가는 것을 볼 수 있다</p>
<blockquote>
<p>☝
Launch Character
캐릭터를 특정 속도로 발사하게 만드는 함수이다
Character Movement Component의 틱에서 적용되며, 이후 falling으로 설정된다
OnLaunched 이벤트를 트리거 한다
XY/Z Override는 true인 경우 XY/Z 속도가 설정된 값으로 바뀌고, 반대의 경우 기존 XY/Z의 속도 값에 더해지게 된다</p>
</blockquote>
<h2 id="숙제">숙제</h2>
<hr />
<p>어제 오늘 배운 블루프린트를 통해 간단한 점프 맵 만들기</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f53c44bb-f818-45fb-8f35-350c9a0ea700/image.png" />

<p>일단 어제 만들어 놓은 맵에 기능을 조금 추가할 예정이다</p>
<h3 id="bridge">Bridge</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ddf3a244-2395-43ed-bd1c-f4a95e64e69d/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3e2f0fb1-6003-4c62-9e4b-179bbbc94dcb/image.png" />
이 액터는 Local 축을 기준으로 회전하는 액터이다

<p>캐릭터와 충돌시 캐릭터를 멀리 날려버리는 액터이다</p>
<p><img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/bca1b6b2-e8b6-4e5b-bb33-5a5987a84ab7/image.png" /><img align="rithg" src="https://velog.velcdn.com/images/gksrudtlr2/post/0942cc35-3fb9-4dc0-9204-abbcd15ec8f9/image.png" />
구현부는 위의 사진처럼 되어있다</p>
<p>Tick 함수에서 SetActorLocalRotation을 이용해 실시간으로 회전하게 만들었다</p>
<p>OnComponentHi를 사용해 Character와 부딪히면 LaunchCharacter 함수를 사용해 멀리 날려버린다</p>
<h3 id="사라지는-바닥">사라지는 바닥</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3be2bd4c-02df-454e-ae93-dcbdf92c07a5/image.png" />
!<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d00a3ce7-43a3-46ca-99e5-1a5f50693cfd/image.png" />

<p>이 액터와 캐릭터가 충돌하면 액터의 Mesh가 사라지고 충돌체도 꺼지면서 캐릭터가 땅으로 떨어지게 하였다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/6e1585d2-4741-4e67-89df-9855c54b71c1/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ad37a2c1-eb43-4ee1-8813-aaa0c469b517/image.png" />
Floor는 BP_Player와 충돌 시 Mesh와 충돌체를 끄면서 화면상에 보이지 않고 더이상 충돌을 하지 않게 구현했다

<p>충돌이 끝나면 다시 충돌과 Mesh를 보여지게 하기 위해 EndOverlap을 이용하여 구현했습니다</p>
<h3 id="미끌어지는-바닥">미끌어지는 바닥</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/20043a9a-e124-44f2-931b-b2d0593fcd1f/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/85cfb8ab-6e88-46a0-b713-6608a6146b28/image.png" />

<p>미끌어지는 바닥은 함정의 대부분을 차지한다</p>
<p>InterpToMovement 컴퍼넌트에 비헤이비어 타입에서 PingPong을 사용하여 계속해서 움직임이 보간하도록 했습니다</p>
<p>캐릭터가 땅을 밟으면 미끄러집니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/2643ae70-60b1-4370-9e53-54b46f83f442/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7db996d2-6d6b-4214-8902-8997a85ed07d/image.png" /></p>
<p>다른 함정들과 마찬가지로 캐릭터와 충돌 시 BP_Player에서 CharacterMovement 컴포넌트를 가져와 그 안에 지면 마찰과 감속 걷기 제동의 값을 변경하여 캐릭터가 미끄러지도록 구현했습니다</p>
<p>충돌이 끝나고 다른 바닥을 밟았을 땐 미끄러지면 안되므로 지면 마찰과 감속 걷기를 원래대로 되돌려 미끄러지지 않게 하였습니다</p>
<h3 id="wall">Wall</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ae5f9ae9-27f1-4aeb-82f7-1a34024f6682/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f0a87d2e-e139-464b-833f-9781b2517c42/image.png" />

<p>이 벽은 위 아래로 왔다갔다 하는 캐릭터와 충돌 시 멀리 날려버리는 벽으로 구현하였습니다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b62d41cc-4c6a-4b13-8af2-f8095203be0a/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1c0e0b2c-f413-45e9-b057-b4b6d3a630c7/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/59ee8027-640b-4bee-b87d-cb3834432922/image.png" />
BeginPlay에 현재 위치를 저장해준다

<p>위아래로 움직이기 위해 특정 위치에 도달하면 움직이는 방향을 변경하도록 구현했습니다</p>
<p>Tick 함수에서 Arrive가 true고 현재 위치와 시작 위치를 저장해 준 Start를 Distance로 거리를 계산해줍니다</p>
<p>계산된 값과 특정 갑을 비교하여 Distancs가 그 값보다 작거나 같으면 아래로 이동시켰습니다</p>
<p>Arrive와 두 번째 값이 false면 위로 올라가게끔 구현하였고 이 때 start와 현재 위치가 같다면 Arrive를 true로 바꿔주면서 다시 아래로 이동하게 하였습니다 </p>
<h3 id="자동차">자동차</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/30045a48-e53c-4a3b-8a7c-da076c4754a4/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/da17a753-4836-4ffd-ac52-ee7dcc7d5756/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9958e5fa-c054-4be3-83b7-1095e42d2a28/image.png" />
이 게임의 핵심 함정으로 특정 위치를 계속해서 왔다갔다 하는 액터입니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/098165a1-7435-4c3c-bbe6-9328994f877f/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b8a47c29-6ff4-404c-b660-0e8ebe4a24f5/image.png" />
이 액터는 Arrive가 true일 때 X축 방향으로 이동하게 구현하였습니다

<p>fale면 Rotator가 true인지 판단하는데 true면 Data가 180과 같은지 판단하여 같지 않다면 액터가 회전하게 구현했습니다</p>
<p>이 때 Data 값에 회전시킬 때 넣은 값을 누적해 더해주면서 180도만 회전할 수 있도록 구현하였습니다</p>
<p>Data가 180과 같다면 Rotator를 false로, Data를 0으로 Arrive를 true로 바꿔주면서 다시 움직이게 해줍니다</p>
<p>이때 반대 방향으로 이동해야 하므로 Speed에 -1을 곱해주어 반대로 이동하게 해줍니다</p>
<p>Rot 함수는 Rotator를 true로 Arrive를 false로 변경해주는 함수입니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/4ff54df8-e81e-43a5-a550-d8f0c74ab831/image.png" /></p>
<p>이 함수를 호출하기 위해 BP_Overlap 클래스에서 BP_Car와 충돌시 BP_Car의 Rot 함수를 호출하여 구현하였습니다</p>
<h3 id="warp">Warp</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/c13718d7-e500-47c5-8c05-7f55d6089e8b/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f024a34c-7a27-4846-8730-bb717c1115d6/image.png" />

<p>플레이어가 맵을 벗어나면 시작 위치로 돌아갈 수 있도록 구현했습니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/be6615a6-e177-49c7-bc82-47f2e5765e16/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/e82c27a3-cca2-4c8e-b966-9fe2bac02f4e/image.png" />
Warp 클래스에서 BP_Player와 충돌 시 BP_Player의 Start Location 함수를 호출합니다</p>
<p>이 함수는 BeginPlay에서 시작 위치를 저장한 변수를 가지고 처음 위치로 돌려줍니다</p>
<h3 id="endgame">EndGame</h3>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d855bc14-b74b-49c0-a183-08d8e99963a1/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/8965cc10-505d-4fe4-a929-1be1e6687f40/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/42dcc94b-827b-4c72-a322-3d91d3c5f7fa/image.png" />

<p>도착 지점에 도착하면 UI를 띄우게 하였습니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cf514b76-a2d1-40a1-a175-e4bdb88c38c0/image.png" /></p>
<p>이 역시 Warp와 마찬가지로 충돌 시 BP_Player의 EndGame함수를 호출합니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/3913d3e5-c6ef-4062-a153-fc6075651362/image.png" /></p>
<p>EndGame 함수를 보기 전 BeginPlay에서 UI Widget을 생성하고 생성된 변수를 숨긴 뒤 뷰포트에 추가해줍니다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/4c8a84e7-f7dc-4f3b-be97-267771ddc417/image.png" />
EndGame 함수가 실행되면 Disable Input 함수로 입력이 들어오지 않게 하고 UI가 보이게 해줍니다</p>
<h2 id="수업-외-구현-부">수업 외 구현 부</h2>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/8fc1a4c0-0d33-4a5c-b1e2-481ed677e376/image.png" />
애니메이션 블루프린트에서 State Machine 안에서 기본 Jump와 달릴 때 Jump를 나눠 Jump Loop, Land를 구현했습니다

<p>Spee 값에 따라 점프 모션과 Land 모션이 달라집니다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/e3db1f40-c0d8-4c35-aa21-3d30d3c618d1/image.png" />

<p>기본 움직임과 Jump 사이에선 Falling 이 true고 Speed에 따라 Jump 모션이 다르게 구현하였습니다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ab8aaa53-0c78-483e-8cde-6ae7e64ae93f/image.png" />

<p>Jump에서 Jump Loop로 가는 것은 Jump 애니메이션의 Time remaining 값이 0.5보다 작거나 같을 때 변경되도록 구현하였습니다.</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9416c29d-3603-4244-a417-ff8bd56356e3/image.png" />

<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7e765d80-6024-4a9b-9dd7-f5612359d430/image.png" />

<p>점프가 끝나고 땅에 도착하는 모션은 Falling이 False일 때 변경되도록 하였고 이때 Speed 값에 따라 모션이 다르게 구현했습니다</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d05f88db-8004-4415-bb8e-24972852e95c/image.png" />

<p>마지막으로 원래 기본 움직이는 애니메이션으로 바뀌기 위해 Land 애니메이션의 Time Remaining 값이 0.8보다 작다면 바뀔 수 있게 하였습니다</p>
<h3 id="시연-영상-및-설명">시연 영상 및 설명</h3>
<p><a href="https://www.youtube.com/watch?v=1k22NfeBFZY&amp;t=1s">https://www.youtube.com/watch?v=1k22NfeBFZY&amp;t=1s</a></p>
<h2 id="느낀점">느낀점</h2>
<p>이번 프로젝트를 진행하면서 오랜만에 블루프린트를 사용해 생각한 시간보다 더 오래 걸렸던것 같다</p>
<p>수업 때 배운 내용을 복습하는 겸 여러 함정도 만들었고 원래 알고있던 것들도 조금씩 구현했습니다</p>
<p>하지만 오랜만에 하기도 하고 생각처럼 구현이 잘 안됐습니다</p>
<p>그래도 구글링을 하거나 질문을 하는 등으로 해결을 하였습니다</p>
<p>그러면서 간단한 것도 생각처럼 잘 나오지 않아도 끝까지 하면 어떻게든 구현할 수 있다는 자신감도 생겼고 이를 통해 더욱더 열심히 참여해야겠다는 생각이 들었습니다</p>