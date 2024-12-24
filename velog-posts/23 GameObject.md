<ul>
<li><p>GameObject</p>
<ul>
<li>모든 물체들을 묶어서 관리하기 위해 클래스로 묶은것이다</li>
<li>pipelineinfo 같은 경우 물체마다 각각 가지고 그려주는 것이지 Render에서 모든 부분을 할 필요가 없다</li>
<li>지금처럼 Render에 렌더링 파이프 라인을 모든 물체들을 하나의 렌더링 파이프 라인으로 그리는 것이 아닌 같은 애들끼리 묶어서 렌더링 파이프라인을 설정해 그리고 다른 물체들은 다른 설정을 통해 렌더링 파이프 라인을 그리는 식으로 하기위한 클래스이다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/861148a2-b800-4be8-ac1a-089c570ad8f7/image.png" /></li>
<li>GameObject 클래스에서는 오브젝트마다 자기 자신만의 정보를 가지고있고 그를 토대로 그림을 그리게 할 것이다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/51c01595-223e-496f-9ff9-71ee19030d74/image.png" /></li>
<li>생성자에서 객체들을 동적 할당을 해준 뒤 Create함수를 사용하여준다</li>
<li>이는 Game의 Init에서 한 것을 그대로 가져와주면 된다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d4086510-edb6-450c-b932-c1e454e2658e/image.png" /></li>
<li>Update함수에서는 scale, rotation, translation을 가지고 world 행렬을 만들어 transforData.World에 저장해주고 constantBuffer를 통해 GPU에서 CPU로 값을 복사해주어 변화가 일어나면 적용시킨다</li>
<li>Render 함수에서는 Game에 Render에 있는 부분을 그대로 가져와 오브젝트마다 자신이 가진 정보대로 렌더링 파이프라인에 적용하여 그림을 그리는 과정이다</li>
</ul>
</li>
<li><p>요약</p>
<ul>
<li>Graphics : Device, DeviceContext, RenderTargetView와 같이 핵심적이고 변하지 않는 것들이 배치됨</li>
<li>Pipeline : 렌더링 파이프라인 묘사, 실시간으로 렌더링 파이프라인에서 셋팅하는것을 맵핑해 관리하는 부분</li>
<li>GameObject : 오브젝트마다 자기만의 정보를 가지고 그를 토대로 어떤식으로 그림이 그려질것</li>
</ul>
</li>
</ul>