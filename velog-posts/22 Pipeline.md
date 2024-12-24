<ul>
<li><p>Rasterizer</p>
  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7e8999a8-ae15-4772-9766-da2b7294e9f4/image.png" />
</li>
<li><p>SamplerState</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/82ef3995-8af5-4aa7-8e1b-f54ffa010e21/image.png" /></li>
<li><p>BlendState</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a81cdc8e-fbf6-4aee-b889-7b926931dd0f/image.png" style="margin-bottom: 0;" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a0659add-b297-4871-9a4f-b525f898564d/image.png" style="margin-top: 0;" /></li>
<li><p>Game</p>
<pre><code class="language-cpp">void Game::Init(HWND hWnd)
{
  ...
  sampler = make_shared&lt;SamplerState&gt;(graphics-&gt;GetDevice());
  ...
  rs = make_shared&lt;Rasterizer&gt;(graphics-&gt;GetDevice());
  ...
  blend = make_shared&lt;BlendState&gt;(graphics-&gt;GetDevice());

  rs-&gt;Create();
  ...
  sampler-&gt;Create();
  ...
  //CreateBlendState
  blend-&gt;Create();
  ...
}
...
void Game::Render()
{
  ...
  //RS
  deviceContext-&gt;RSSetState(rs-&gt;GetComPtr().Get());

  //PS
  ...
  deviceContext-&gt;PSSetSamplers(0, 1, sampler-&gt;GetComPtr().GetAddressOf());

  //OM
  deviceContext-&gt;OMSetBlendState(blend-&gt;GetComPtr().Get(), blend-&gt;GetBlendFactor(),  blend-&gt;GetSampleMask());
  ...
}
</code></pre>
</li>
</ul>
<p>```</p>
<ul>
<li>Class로 나눈 Rasterizer, SamplerState, BlendState를 Game클래스에 객체로 만들어 적용시킨다</li>
<li>Pipeline<ul>
<li>지금까지 class 별로 나눈 것들은 새로운 리소스를 만들 때 사용되었지만 지금 만드는 Pipeline 클래스는 DeviceContext가 렌더링 파이프 라인과 나머지 리소스들을 묶어주는 자원을 맵핑해주는 역할을 할 것이다</li>
<li>Game의 Render함수에서 하는 것을 Pipeline에 묶어 더 알아보기 쉽고 사용하기 편하게 클래스로 묶어서 사용하게 될 것이다.<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/edcb754e-5bc2-470c-923e-71541b07670f/image.png" /></li>
<li>Update 함수에서는 Pipeline에서 필수적인 리소스들을 DeviceContext에 셋팅해줄 것이다</li>
<li>부가적으로 필요한 것들은 각각의 함수들을 통해 콜할 수 있게 만들어 주었다</li>
<li>이때 ConstantBuffer는 어떤 값이 들어올지 모르기 때문에 Templayte로 만들어 범용적으로 사용 가능하게 하였고, scope를 통해 enum으로 만들었던 값들과 비트연산을 통해 Vs인지 Ps인지 판단하여 ConstantBuffer를 설정할 수 있게 해주었다<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/e7cb2ae8-35a9-4a44-b38d-726fa93faac3/image.png" /></li>
<li>Render에 있던 내용을 각각에 알맞은 부분에 넣어주었다</li>
<li>이때 Draw와 DrawIndexed를 이용해 IndexBuffer가 있고 없을때 그리는 방법이 다르기 때문에 각각 알맞은 함수를 콜하여 그림을 그릴 수 있게 해주었다</li>
</ul>
</li>
</ul>