<ul>
<li><p>ConstantBuffer</p>
  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/bd7723af-58f1-47d9-b35e-370d6d818108/image.png" />
 - constant buffer는 vs서 가장 많이 사용하므로 사실상 shader에 만들어야하지만 vs에 만들어줬다
 - ConstantBuffer를 template로 만들어 어떤 종류의 Constant Buffer든 다 호환되어 만들 수 있게 하였다
 - Constant Buffer를 만들어주는 부분과 GPU에 있는 데이터를 CPU로 복사해주는 부분을 함수로 만들어 사용할 수 있게 해줬다
</li>
<li><p>Shader</p>
  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/c104cd03-1fa3-4461-b3e6-4db394d619fe/image.png" />
 - Shader에선 소멸자, Create는 상속받아 재정의 해줄 것이므로 가상화를 해주었다
 - Enum으로 ShaderScop를 만들어 Shader가 현재 있는지, 어떤 Shader가 있는지 등을 활용하기 위해 만들었으며 비트 연산자를 사용하여 어떤 Shader가 사용중인지 확인이 가능하다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7965d04c-b7d5-4f06-812b-19c6a294a888/image.png" />
 - LoadShaderFormFile 함수에서는 Shader 파일을 불러와 Shader 파일을 컴파일 해준다
 - VertexShader
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1e389163-21ac-4c71-b67b-18c5b97af324/image.png" />
  - Shader를 상속받아 Create함수를 재정의 해주었다
  - Create 함수에서 LoadShaderFormfile을 통해 Shader 파일을 컴파일하고 VertexShader를 만드는 과정이다

<ul>
<li>PixelShader<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/f8d11903-b260-45b5-9242-89bf998a0d86/image.png" />
- PixelShader역시 Shader를 상속받아 Create 함수를 재정의 해주었다
- Create 함수에서 LoadShaderFormfile을 통해 Shader 파일을 컴파일하고 PixelShader를 만드는 과정이다
</li>
</ul>
</li>
<li><p>Texture</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/df730cf4-9ba4-4a81-8b41-fcde9eb4ab72/image.png" />
  - Texture는 Shader resource View로 만들어 지는데 이는 Shader에서 Texture에 해당되는 부분이므로 Texture라고 Class이름을 지었다
  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9b7fcc71-9a10-459c-8b8f-6ffd529f13a9/image.png" />
  - Create 함수에서 texture를 읽어와 Shader Resource View를 만들어 Shader에 꽂아줄 수 있게한다
</li>
<li><p>Game</p>
<ul>
<li>Game 함수에서 VertexShader,PixelShader, ConstantBuffer, Texture(SRV)를 동적으로 메모리를 할당한 뒤 각각 Create 함수를 통해 만들어준다</li>
<li>ConstantBuffer는 Update에서 매 프레임 복사가 일어나야 하므로 CopyData를 통해 데이터를 복사할 수 있게 한다</li>
<li>Render 함수에선 만들어진 데이터를 토내로 Shader나 ConstantBuffer를 세팅해주면 된다</li>
</ul>
</li>
</ul>
<pre><code class="language-cpp">void Game::Init(HWND hWnd)
{
    vertexShader = make_shared&lt;VertexShader&gt;(graphics-&gt;GetDevice());
    pixeShader = make_shared&lt;PixelShader&gt;(graphics-&gt;GetDevice());
    constantBuffer = make_shared&lt;ConstantBuffer&lt;TransformData&gt;&gt;(graphics-&gt;GetDevice(), graphics-&gt;GetDeviceContext());
    srv = make_shared&lt;Texture&gt;(graphics-&gt;GetDevice());
...
    vertexShader-&gt;Create(L&quot;Default.hlsl&quot;, &quot;VS&quot;, &quot;vs_5_0&quot;);
    pixeShader-&gt;Create(L&quot;Default.hlsl&quot;, &quot;PS&quot;, &quot;ps_5_0&quot;);
    srv-&gt;Create(L&quot;IMG_0424.png&quot;);
...

    constantBuffer-&gt;Create();
}

void Game::Update()
{
...
    constantBuffer-&gt;CopyData(transformData);
}

void Game::Render()
{
...
    //VS
    deviceContext-&gt;VSSetShader(vertexShader-&gt;GetComPtr().Get(), nullptr, 0);
    deviceContext-&gt;VSSetConstantBuffers(0, 1, constantBuffer-&gt;GetComptr().GetAddressOf());
...
    //PS
    deviceContext-&gt;PSSetShader(pixeShader-&gt;GetComPtr().Get(), nullptr, 0);
    deviceContext-&gt;PSSetShaderResources(0, 1, srv-&gt;GetComPtr().GetAddressOf());
...
}
...</code></pre>