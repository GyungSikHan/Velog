<h2 id="camera와-transform-나누기">Camera와 Transform 나누기</h2>
<hr />
<ul>
<li><p>Camera class</p>
<ul>
<li>지금 우리 구조를 보면 물체마다 World, View, Projection을 넘겨주게 되면서 카메라가 있던 없던 카메라까지 쉐이더에서 연산을 계속해서 하게된다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/827a5d11-4b64-4a4b-8b35-955bd00d18f9/image.png" />    </li>
<li>이를 방지하기 위해 Shader에서 TransformData에서 카메라에 해당하는 View와 Projection을 다로 빼내어 따로 값을 받아올 수 있게 만들어준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/ac14ced0-a7fa-429c-8e61-f6e22f338914/image.png" /></li>
<li>마찬가지로 Shader에 World, View, Projection 값을 넘겨주는 TransformData 구조체에서도 Camera와 Transform 정보를 따로 보낼 수 있게 나눠준다</li>
</ul>
</li>
<li><p>GameObject Class</p>
<ul>
<li>GameObject Class에서 Transform에 관련된 데이터를 상수 버퍼로 GPU에 복사해 넘겨줬던 것 처럼 CameraData역시 동일하게 GPU로 복사해줘야 한다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/6af93107-6311-4b10-85c0-5703da1f21a7/image.png" /></li>
<li>먼저 생성자에서 Camera의 ConstantBuffer를 만들어준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d73547a3-6503-4eef-b207-1128772a0244/image.png" /> </li>
<li>그 후 Update 함수에서 View와 Projection을 가져와 ConstantBuffer에 Copy해 GPU로 넘겨줄 수 있게 한다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/c0368e5a-defc-40ee-8ec2-e25a595db69e/image.png" /></li>
<li>Render 함수에서 ConstantBuffer를 Shader에 맞는 slot에 올바른 값을 넘겨주기 위해 Camer 버퍼와 Transform 버퍼를 Shader에 설정한 slot으로 넘겨주면 된다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a57756fc-eb5a-4dca-bafc-7f85d574a207/image.png" /></li>
<li>하지만 실행 결과에서는 아무것도 보이지 않을 것이다</li>
<li>그 이유는 Camera Class에서 UpdateMatrix 함수에서 설정한 Projection의 직교투영시 설정한 카메라의 뷰 포트가 너무 크기 때문에 보이지 않는 것이다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/bcde0c2c-f5f5-4bff-9c16-58588ac316af/image.png" /></li>
<li>해결 방법으로는 뷰 포트의 Width, Height 크기를 줄이거나<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/52f3d5c8-282b-4a86-a399-ddf6ea98c375/image.png" /></li>
<li>Game class에서 화면에 출력하는 객체의 크기를 키우는 식으로 해결하면 되는데 우리는 일단 위의 방법을 선택할 것이다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/52eb2128-d786-4f56-b719-ab5985781944/image.png" /> </li>
<li>그렇게 하면 결과가 잘 나오는 것을 볼 수 있다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b86dcbf1-f457-48d7-918f-bf1f86049683/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/55033fa0-4653-4e93-97e8-44f5c1b08a63/image.png" /></li>
<li>마지막으로 현재 Transform과 Camera의 데이터는 나눠서 GPU로 보내게 하였지만 나눈것과 의미없이 모든 물체들이 카메라 버퍼를 복사하는 일이 아직도 일어난다</li>
<li>그래서 GameObject Class에서 GetCamera 함수를 만들어 Camera가 존재하면 Component로부터 Camera를 가져오고 존재하지 않는다면 null을 반환하는 함수를 만들어준다</li>
<li>이 함수를 통해 Update 함수에서 Camera가 있는지 없는지 판단하여 임시적으로 존재한다면 굳이 상수 버퍼를 복사하지 않고 Update를 끝내도록 조건문을 추가해준다</li>
</ul>
</li>
<li><p>이런 과정을 통해 Transform과 Camera에 해당하는 View, Projection 정보를 나눠 GPU로 보낼 수 있게 한 것이다</p>
</li>
</ul>
<h2 id="meshrenderer">MeshRenderer</h2>
<hr />
<ul>
<li><p>GameObject에 렌더링 파이프라인을 거쳐 어떠한 물체를 그리는데 이를 MeshRenderer 클래스에 분리하여 이 객체를 가지고 있는 물체들만 파이프 라인을 거쳐 그림을 그릴 수 있게 만들어 줄 것이다</p>
</li>
<li><p>그래서 device와 deviceContext를 통해 데이터를 만드는 부분과 렌더링파이프에 데이터를 셋팅하고 Render를 하는 부분을 모두 MeshRenderer로 옮길 것이다</p>
</li>
<li><p>MeshRenderer Class</p>
<ul>
<li>MeshRenderer Class는 Component를 상속받아 만들었으며 생성자에서 Device와 DeviceContext를 가져오고 ComponentType중 MeshRenderer를 Component 생성자에 넘겨줄 것이다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/781d958a-bfda-43b6-a5d5-81768c1e860f/image.png" /> </li>
<li>GameObject의 생성자에 있는 코드를 전부 가져와 MeshRenderer의 생성자에 넣어주면서 렌더링을 하기위한 정보들을 만들어준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a1069858-ba2d-4e65-977e-37cce030d6bc/image.png" /> </li>
<li>Update 함수에서는 Camera Transform의 정보를 Constbuffer로 복사하는 부분을  GameObject의 Update에서 가져와준다</li>
<li>이때 transformData에 World에 값을 넣는 과정에서 GameObject에만 있는 함수를 통해 값을 넘겨주게 되어 오류가 생기므로 GetTransform 함수로 바꿔 오류를 해결해 준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/11f173f9-9213-4595-869f-1501b7af757e/image.png" /> </li>
<li>Rneder 함수 역시 GameObject의 Render 함수에서 모두 가져와준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/c8e0e4fe-bcf2-46e7-a262-4bd35c5ec306/image.png" /> </li>
<li>옮기는 작업이 끝이나면 GameObject Class에서 Component를 배열로 만든 객체안에 MeshRenderer를 가져와 return해주는 함수를 만들어준다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d6ce3da2-dec5-49b0-bdfa-f92d52cc16fd/image.png" /> </li>
<li>실행을 하게되면 오류가 뜰 것인데 그 이유는 Game Class 내에서 Rneder를 하게끔 함수 호출을 해주는 부분인 Render 함수에서 GameObject가 아닌 MeshRenderer안에 있는 Render 함수에서 하므로 GameObject 객체안에 조금전에 만든 GetMeshRenderer 함수를 호출하여 MeshRenderer 클래스의 Render 함수를 호출할 수 있게 만들어 줘야한다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/b021ac34-ac9e-43dc-8279-e93cbfb93cec/image.png" /> </li>
<li>또한 Game Class의  Init 함수에서 GameObject 객체의 AddComponent 함수를 호출하여 GameObject 내의 Component 배열에 MeshRenderer 타입을 추가해 Render 함수에서 GetMeshRenderer에 Render 함수를 호출할 때 null이 안뜨도록 미리 추가해줘야 한다</li>
</ul>
</li>
<li><p>결과</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/215d9897-26d4-47e6-abbd-5eab6fb837d8/image.png" /> 
- 이런 과정을 거치면 우리가 지금까지 출력했던 이미지가 잘 뜨게된다
- 이렇게 World, View, Projection를 넘겨주는 과정에서 Transform과 Camera를 나누어 GPU로 넘겨주게 하고 GameObject에서 Rneder하는 부분을 다른 곳으로 빼서 관리하도록 해주었다</li>
</ul>