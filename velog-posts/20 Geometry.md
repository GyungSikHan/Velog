<ul>
<li>스마트 포인터를 사용한 이유<ul>
<li>장점<ul>
<li>동적으로 만든 메모리 공간뿐만 아니라 reference count가 관리되는 블록까지한번에 만들어주기 때문에 강의에서 일반적인 new 동적할당이 아닌 스마트 포인터를 사용</li>
</ul>
</li>
<li>단점<ul>
<li>사이클 문제에 대해 자유롭지 않아 항상 염두하고 작업해야 함</li>
</ul>
</li>
</ul>
</li>
<li>Geometry  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1aabf220-c986-42eb-9037-d822f8f2f718/image.png" />


</li>
</ul>
<pre><code>- Geometry는 template로 만들어 Vertex에 대한 정보가 어떤것이 들어와도 호환이 될 수 있도록 만듦
- 이때 vertex의 정보들 뿐만 아니라 index의 정보들도 저장할 수 있게 하였다</code></pre><ul>
<li>VertexData<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9a611234-4f93-4040-bf66-e2c026c25f9a/image.png" />
  - VertexData는 Texture와 Color 값을 선택하여 도형을 만들 때 색을 입혀줄 수 있게 구조체로 만들었으며 추후 더 추가가 될 것이다
  - descs를 static으로 만들어 Shader에 넘어갈 정보를 알맞게 미리 초기화하여 어디서든 가져다 쓸 수 있게 만들어 주었다</li>
<li>GeometryHelper<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/0dc84dc3-027e-47c7-9585-48d987a202fe/image.png" />
  - GeometryHelper는 사각형을 그리는 함수를 만들었으며 각각 Color, uv를 통해 색을 채워줄 수 있게 Vertex와 Index에 설정해 주는 함수로 만들었다</li>
<li>Game<ul>
<li>geometry변수를 동적으로 만들어준 뒤 기존에 Vertex,Index를 만들던 방식이 아닌 GeometryHelper로 Rectangle을 그려주었으며, VertexBuffer, IndexBuffer에도 GeometryHelper를 사용해 geometry에 저장된 vertex, index 정보를 넘겨주었다<pre><code class="language-cpp">void Game::Init(HWND hWnd)
{
...
geometry = make_shared&lt;Geometry&lt;VertexTextureData&gt;&gt;();
...
}
</code></pre>
</li>
</ul>
</li>
</ul>
<p>...</p>
<p>void Game::Render()
{
    uint32 stride = sizeof(VertexTextureData);
    ...
    deviceContext-&gt;DrawIndexed(geometry-&gt;GetIndexCount(), 0, 0);
}</p>
<p>...</p>
<p>void Game::CreateGeometry()
{
    //VertexData - index
    {
        GeometryHelper::CreateRectangle(geometry);
    }
    //VertexBuffer
    {
        vertexBuffer-&gt;Create(geometry-&gt;GetVertices());
    }
    //IndexBuffer
    {
        indexBuffer-&gt;Create(geometry-&gt;GetIndices());
    }
}
...</p>
<p>```</p>
<ul>
<li>실행했을 때 문제가 없이 돌아가면 잘 분리가 된 것이다.</li>
</ul>