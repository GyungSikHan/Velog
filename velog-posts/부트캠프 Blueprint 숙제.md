<h2 id="숙제">숙제</h2>
<hr />
<p>(<a href="https://1drv.ms/u/c/9360c5bd5d7fe113/ERFhz8ALyAJIh-f69OhKOoQBbx_ygmBiei8Y_hqqPOBTgw?e=SJVUim">https://1drv.ms/u/c/9360c5bd5d7fe113/ERFhz8ALyAJIh-f69OhKOoQBbx_ygmBiei8Y_hqqPOBTgw?e=SJVUim</a> 숙제 링크)</p>
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