<h2 id="mesh-class">Mesh Class</h2>
<h3 id="mesh-class-1">Mesh Class</h3>
<pre><code class="language-C++">class Mesh : public ResourceBase
{
    using Super = ResourceBase;
public:
    Mesh(ComPtr&lt;ID3D11Device&gt; device);
    virtual ~Mesh();

    void CreateDefaultRectanble();

    shared_ptr&lt;VertexBuffer&gt; GetVertexBuffer() { return m_pVertexBuffer; }
    shared_ptr&lt;IndexBuffer&gt; GetIndexBuffer() { return m_pIndexBuffer; }

private:
    ComPtr&lt;ID3D11Device&gt; m_pDevice;
    //Mesh
    shared_ptr&lt;Geometry&lt;VertexTextureData&gt;&gt; m_pGeometry;
    shared_ptr&lt;VertexBuffer&gt; m_pVertexBuffer;
    shared_ptr&lt;IndexBuffer&gt; m_pIndexBuffer;
};

cpp
Mesh::Mesh(ComPtr&lt;ID3D11Device&gt; device)
    : Super(ResourceType::Mesh), m_pDevice(device)
{
}

Mesh::~Mesh()
{
}

void Mesh::CreateDefaultRectanble()
{
    //Create Geometry
    m_pGeometry = make_shared&lt;Geometry&lt;VertexTextureData&gt;&gt;();
    GeometryHelper::CreateRectangle(m_pGeometry);

    //VertexBuffer
    m_pVertexBuffer = make_shared&lt;VertexBuffer&gt;(m_pDevice);
    m_pVertexBuffer-&gt;Create&lt;VertexTextureData&gt;(m_pGeometry-&gt;GetVertices());

    //IndexBuffer
    m_pIndexBuffer = make_shared&lt;IndexBuffer&gt;(m_pDevice);
    m_pIndexBuffer-&gt;Create(m_pGeometry-&gt;GetIndices());
}</code></pre>
<ul>
<li><p>Mesh는 물체의 형태를 나타나는 것으로 Geometry하나와 VertexBuffer, IndexBuffer가 하나로 사용할 것이므로 MeshRenderer안에 이 객체들을 Mesh Class로 옮겨준다</p>
</li>
<li><p>ID3D11Device 또한 버퍼들을 만들때 필요하므로 생성자에서 받아와 저장할 수 있게 매개변수로 만들어준다</p>
</li>
<li><p>나중에 버퍼들을 다른곳에서 사용할수도 있으므로 VertexBuffer와 IndexBuffer를 return해주는 함수도 만들어 준다</p>
</li>
<li><p>CreateDefaultRectangle 함수를 통해 기본 사각형을 그릴수 있게 구현할것이므로 Geometry와 VertexBuffer, IndexBuffer를 동적할당하고 생성하는 구문을 MeshRenderer의 생성자에서 가져와준다</p>
</li>
<li><p>나중에는 현재 Geometry가 우리가 만든 Helper 클래스로 간단한 사각형을 그리는 것이 아닌 복잡한 3D같은 물체를 그릴땐 fbx 파일에 있는 Geometry를 만들어준 뒤 그에 맞는 Buffer를 연결해주는 식으로 만들어야 할것이다</p>
<h3 id="오류제거">오류제거</h3>
</li>
<li><p>빌드를 실행하면 RenderManager등에서 오류가 생기는 것을 볼 수 있다</p>
</li>
<li><p>이는 우리가 MeshRenderer에서 변수들을 Mesh로 가져오면서 생긴 문제들일 것이기 때문에 이를 고쳐줘야한다</p>
<pre><code class="language-C++">class MeshRenderer
{
...
public:
  void SetMesh(shared_ptr&lt;Mesh&gt; mesh) { m_pMesh = mesh; }
  shared_ptr&lt;Mesh&gt; GetMesh() { return m_pMesh; }
...
private:
  shared_ptr&lt;Mesh&gt; m_pMesh;
}</code></pre>
</li>
<li><p>Mesh를 통해 물체를 그려주는데 MeshRenderer가 존재하는 물체들만 그림을 그려줄 것이기 때문에 MeshRenderer에 Mesh 객체를 만들어준다</p>
</li>
<li><p>이때 Mesh는 외부에서 만들어 넘겨줄것이므로 Get,Set 함수를 만들어 Mesh를 설정해주고 다른곳으로 return해주는 함수를 만들어준다</p>
<pre><code class="language-C++">RenderMGR.cpp
...
void RenderMGR::RenderObjects()
{
  for (const shared_ptr&lt;GameObject&gt;&amp; gameObject :    m_vRenderObject)
  {
      ...
      m_pPipeline-&gt;SetVertexBuffer(meshRenderer-&gt;GetMesh()-&gt;GetVertexBuffer());
      m_pPipeline-&gt;SetIndexBuffer(meshRenderer-&gt;GetMesh()-&gt;GetIndexBuffer());

      m_pPipeline-&gt;ConstantBuffer(0, EVertexShader, m_pCameraBuffer);
      m_pPipeline-&gt;ConstantBuffer(1, EVertexShader, m_pTransformBuffer);

      m_pPipeline-&gt;SetTexture(0, EPixelShader, meshRenderer-&gt;GetTexture());
      m_pPipeline-&gt;SetSamplerState(0, EPixelShader, m_pSampler);

      m_pPipeline-&gt;DrawIndexed(meshRenderer-&gt;GetMesh()-&gt;GetIndexBuffer()-&gt;GetCount(), 0, 0);
  }
}</code></pre>
</li>
<li><p>기존에 Pipeline에 MeshRenderer로 만든 변수로 Buffer를 가져와 연결해주었던 부분은 이제 meshRenderer 변수에서 GetMesh를 호출해 mesh 안에있는 Buffer등을 꺼내서 사용해주면 오류가 사라질 것이다</p>
<pre><code class="language-C++">ResourceMGR.cpp
...
void ResourceMGR::CreateDefaultMesh()
{
  //Mesh
  shared_ptr&lt;Mesh&gt; mesh = make_shared&lt;Mesh&gt;(m_pDevice);
  mesh-&gt;SetName(L&quot;Rectangle&quot;);
  mesh-&gt;CreateDefaultRectanble();
  Add(mesh-&gt;GetName(), mesh);
}
...</code></pre>
</li>
<li><p>이때 빌드를 하면 오류가 없지만 실행을 하게되면 Mesh를 셋팅한적이 없기 때문에 크래쉬가 날것이므로 ResourceMGR에서 Texture처럼 생성을 해줘야 한다</p>
</li>
<li><p>이렇게 하면 기본적인 메쉬중 Rectangle이라는 것을 만들어 준것이고, 다른 메쉬를 사용하기 위해서는 SceneMGR에서 생성 및 추가를 해줬었다</p>
<pre><code class="language-C++">SceneManager.cpp
...
shared_ptr&lt;Scene&gt; SceneManager::LoadTestScene()
{
  ...
  //monster
  shared_ptr&lt;GameObject&gt; m_pMonster = make_shared&lt;GameObject&gt;(m_pGraphics-&gt;GetDevice(), m_pGraphics-&gt;GetDeviceContext());
  {
      m_pMonster-&gt;GetOrAddTransform();
      shared_ptr&lt;MeshRenderer&gt; meshRenderer = make_shared&lt;MeshRenderer&gt;(m_pGraphics-&gt;GetDevice(), m_pGraphics-&gt;GetDeviceContext());
      m_pMonster-&gt;AddComponent(meshRenderer);

      //TODO : Material

      //auto mesh = RESOURCES-&gt;Get&lt;Mesh&gt;(L&quot;Rectangle&quot;);
      //meshRenderer-&gt;SetMesh(mesh);
      scene-&gt;AddGameObject(m_pMonster);
  }

  return scene;
}</code></pre>
</li>
<li><p>SceneManager에서 LoadTestScene에서 monster를 meshRenderer에 추가해줬던 것처럼 Game 클래스에서 RecourceMGR를 타고 들어가 넘겨준 Key 값에대한 변수가 있는지 판단하여 mesh 변수에 저장해준다
그 후 meshRenderer에 SetMesh를 통해 mesh를 지정해주고 Scene에 Gameobject를 추가하게 되면 monster라는 물체가 Rectangle이라는 메쉬를 갖는 물체로 만들어 줄 수 있다</p>
<h3 id="결과">결과<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/1d9ad612-ed96-4272-aef2-b8b31608e67f/image.png" /></h3>
</li>
<li><p>이미지가 잘 나오는 것을 볼 수 있는데 이를 통해 상용화된 엔진에서는 메쉬라는 개념이 결국 어떠한 모형을 나타내는 것이고 이를 메쉬 렌더러에 전달해주면 된다는 것을 알 수 있다</p>
<h2 id="material">Material</h2>
<h3 id="material-1">Material</h3>
</li>
<li><p>Material은 물체의 재질을 의미한다</p>
</li>
<li><p>이놈은 우리가 봤을 때 Shader와 그와 관련된 애들로 이루어져 있을거란걸 알 수 있다</p>
</li>
<li><p>따라서 MeshRenderer에 Shader와 관련된 부분을 Material Class로 옮겨와야 할 것이다</p>
</li>
<li><p>하지만 아직 Shader에 관련된 리소스 클래스를 만들지 않았기 때문에 Shader class 먼저 작성해야한다</p>
<h3 id="shader-class">Shader class</h3>
<pre><code class="language-C++">class Shader : public ResourceBase
{
  using Super = ResourceBase;
public:
  Shader();
  virtual ~Shader();

  void SetInputLayout(shared_ptr&lt;InputLayout&gt; input);
  void SetVertexShader(shared_ptr&lt;VertexShader&gt; vertex);
  void SetPixelShader(shared_ptr&lt;PixelShader&gt; pixel);

  shared_ptr&lt;InputLayout&gt; GetInputLayout() { return m_pInputLayout; }
  shared_ptr&lt;VertexShader&gt; GetVertexShader() { return m_pVertexShader; }
  shared_ptr&lt;PixelShader&gt; GetPixelShader() { return m_pPixelShader; }
</code></pre>
</li>
</ul>
<p>private:
    //Material
    shared_ptr m_pInputLayout; // Vertex shader를 넘겨줄 때 어떤 모양인지 설정해주므로 같이 가져가야한다
    shared_ptr m_pVertexShader;
    shared_ptr m_pPixelShader;
};</p>
<p>cpp
Shader::Shader() : Super(ResourceType::Shader)
{
}</p>
<p>Shader::~Shader()
{
}</p>
<p>void Shader::SetInputLayout(shared_ptr input)
{
    m_pInputLayout = input;
}</p>
<p>void Shader::SetVertexShader(shared_ptr vertex)
{
    m_pVertexShader = vertex;
}</p>
<p>void Shader::SetPixelShader(shared_ptr pixel)
{
    m_pPixelShader = pixel;
}</p>
<pre><code>- ResourceMGR에서 Shader와 관련된 VertexShader, PixelShader를 가져와준다
- 마찬가지로 Vertex Shader를 GPU에 넘겨줄때 어떤 모양인지 설정해주는 InputLayout도 가져와야한다
- Mesh에서 했던것과 마찬가지로 외부에서 값을 전달받아 Shader나 Layout을 셋팅해주도록 각각 Set 함수를 만들고, 이를 외부에서 사용할 수 있게 Get 함수도 만들어준다
### Material Class
- Material Calss은 어떠한 Shader에 추가적으로 텍스처나 인자들이 들어가야 할 것이다
```C++
class Material : public ResourceBase
{
    using Super = ResourceBase;
public:
    Material();
    virtual ~Material();

    void SetShader(shared_ptr&lt;Shader&gt; shader);
    void SetTexture(shared_ptr&lt;Texture&gt; texture);

    shared_ptr&lt;Shader&gt; GetShader() { return m_pShader; }
    shared_ptr&lt;Texture&gt; GetTexture() { return m_pTexture; }

private:
    shared_ptr&lt;Shader&gt; m_pShader;
    //쉐이더에 넘기는 온갖 인자들
    shared_ptr&lt;Texture&gt; m_pTexture;
};

cpp
Material::Material() : Super(ResourceType::Material)
{
}

Material::~Material()
{
}

void Material::SetShader(shared_ptr&lt;Shader&gt; shader)
{
    m_pShader = shader;
}

void Material::SetTexture(shared_ptr&lt;Texture&gt; texture)
{
    m_pTexture = texture;
}</code></pre><ul>
<li><p>Material Class에서는 쉐이더에 넘겨주는 온갖 인자들을 객체로 추가해 줄 것이고, Shader Class역시 객체로 만들어주는데 현재는 Texture만 존재하므로 Texture Class만 객체로 넘겨준다</p>
</li>
<li><p>마찬가지로 외부에서 셋팅한 값을 받아와 사용할 수 있게 Set함수와 외부에서 사용가능하도록 Get 함수를 각각 만들어준다</p>
<h3 id="resource-setting">Resource Setting</h3>
</li>
<li><p>Material도 만들었으므로 이제 ResourceMGR에서 사용 가능하도록 작성해야한다</p>
<pre><code class="language-C++">ResourceMGR.cpp
...
void ResourceMGR::CreateDefaultShader()
{
  //Create VS
  shared_ptr&lt;VertexShader&gt; vertexShader = make_shared&lt;VertexShader&gt;(m_pDevice);
  vertexShader-&gt;Create(L&quot;Default.hlsl&quot;, &quot;VS&quot;, &quot;vs_5_0&quot;);

  //CreateInputLayout
  shared_ptr&lt;InputLayout&gt; inputLayout = make_shared&lt;InputLayout&gt;(m_pDevice);
  inputLayout-&gt;Create(VertexTextureData::descs, vertexShader-&gt;GetBlob());

  //CreatePS
  shared_ptr&lt;PixelShader&gt; pixelShader = make_shared&lt;PixelShader&gt;(m_pDevice);
  pixelShader-&gt;Create(L&quot;Default.hlsl&quot;, &quot;PS&quot;, &quot;ps_5_0&quot;);

  shared_ptr&lt;Shader&gt; shader = make_shared&lt;Shader&gt;();
  shader-&gt;SetName(L&quot;Default&quot;);
  shader-&gt;SetInputLayout(inputLayout);
  shader-&gt;SetVertexShader(vertexShader);
  shader-&gt;SetPixelShader(pixelShader);

  Add(shader-&gt;GetName(), shader);
}
</code></pre>
</li>
</ul>
<p>void ResourceMGR::CreateDefaultMaterial()
{
    shared_ptr material = make_shared();
    material-&gt;SetName(L&quot;Default&quot;);
    material-&gt;SetShader(Get(L&quot;Default&quot;));
    material-&gt;SetTexture(Get(L&quot;Test&quot;));
    Add(material-&gt;GetName(), material);
}
...</p>
<pre><code>- 다른 CreateDefault 함수들과 마찬가지로 MeshRenderer class의 생성자에서 VertexShader, InputLayout, PixelShader를 만들어주는 부분을 가져와 CreateDefaultShader에 붙여넣어준 뒤 동적 메모리를 갖는 변수로 만들어준다
만들어진 변수들을 가지고 shader 클래스 변수에 값을 넘겨줄 것이다
- 끝이나면 Add를 통해 현재 Shader의 이름을 Key 값으로 shader안에 있는 값들이 map안에 저장될 것이다
- 또한 CreateDefaultMaterial 함수에서도 Material에 Shader와 Texture 값을 넘겨줘 저장한 뒤 map에 저장할 것이다
- 이때는 우리가 CreateDefault 함수를 사용해 만든 Shader와 Texture의 정보를 가져와 Material에 넘겨줘야하기 때문에 Get 함수를 사용해 Key값으로 된 정보를 넘겨줘야 한다
- 마찬가지로 정보를 다 넘겨줬으면 Add 함수를 통해 map안에 저장해준다
- 이렇게 분리해서 값을 셋팅하고 저장해주면 같은 리소스들을 여러번 생성하지 않고 한번 생성된 리소스를 저장해놓고 재 사용이 가능해진다

### 오류
- 빌드시 여러가지 오류가 뜰탠데 그 이유는 MeshRenderer에서 Material에 저장된 정보들을 RebderMGR에서 PipelineInfo에 전달해주는 부분에서 함수들이 다 없어졌으므로 문제가 생길것이다
``` C++
public:
    void SetMesh(shared_ptr&lt;Mesh&gt; mesh);
    void SetMaterial(shared_ptr&lt;Material&gt; material);
    void SetShader(shared_ptr&lt;Shader&gt; shader);
    void SetTexture(shared_ptr&lt;Texture&gt; texture);

    shared_ptr&lt;Mesh&gt; GetMesh() { return m_pMesh; }
    shared_ptr&lt;Material&gt; GetMaterial() { return m_pMaterial; }
    shared_ptr&lt;VertexShader&gt; GetVertexShader() { return m_pMaterial-&gt;GetShader()-&gt;GetVertexShader(); }
    shared_ptr&lt;PixelShader&gt; GetPixelShader() { return m_pMaterial-&gt;GetShader()-&gt;GetPixelShader(); }
    shared_ptr&lt;InputLayout&gt; GetInputLayout() { return m_pMaterial-&gt;GetShader()-&gt;GetInputLayout(); }
    shared_ptr&lt;Texture&gt; GetTexture() { return m_pMaterial-&gt;GetTexture(); }

private:
    ComPtr&lt;ID3D11Device&gt; m_pDevice;

    //Mesh
    shared_ptr&lt;Mesh&gt; m_pMesh;
    //Material
    shared_ptr&lt;Material&gt; m_pMaterial;

cpp
void MeshRenderer::SetMesh(shared_ptr&lt;Mesh&gt; mesh)
{
    m_pMesh = mesh;
}

void MeshRenderer::SetMaterial(shared_ptr&lt;Material&gt; material)
{
    m_pMaterial = material;
}

void MeshRenderer::SetShader(shared_ptr&lt;Shader&gt; shader)
{
    m_pMaterial-&gt;SetShader(shader);
}

void MeshRenderer::SetTexture(shared_ptr&lt;Texture&gt; texture)
{
    m_pMaterial-&gt;SetTexture(texture);
}</code></pre><ul>
<li>MeshRenderer Class에서 Mesh와 Material 객체를 만들어주고 Texture 객체는 Material 안에 다 있으므로 지워주도 된다</li>
<li>각각의 정보들을 셋팅하고 Return해줄 함수들도 만들어 구현해주면 이제 RenderMGR에서 가져다 사용할 수 있게된다</li>
<li>이때 Update 함수는 사용하지 않으므로 지워준다(나는 혹시 몰라 일단 지우진 않았다)<pre><code class="language-C++">RenderMGR.cpp
</code></pre>
</li>
</ul>
<p>void RenderMGR::RenderObjects()
{
...
    PipelineInfo info;</p>
<pre><code>info.inputLayout = meshRenderer-&gt;GetInputLayout();
info.vertexShader = meshRenderer-&gt;GetVertexShader();
info.pixelShader = meshRenderer-&gt;GetPixelShader();</code></pre><p>...
}</p>
<pre><code>- RenderMGR Class에서 RenderObjects 함수에 PipelineInfo에 값을 지정해줄 때 meshRenderer에서 꺼내서 알맞는 값을 저장해줬었는데 이 함수들이 바뀌었으므로 각각 알맞는 함수로 교체해 저장해주면 오류가 사라질 것이다
- 이는 MeshRenderer에 우리가 원하는 메쉬랑 Materila을 먼저 설정하고 그것을 꺼내서 파이프라인에 넘겨줄 수 있게 되는 것이다
### SceneMGR Material 설정
- 이제 SceneMGR에서 GameObject에대한 Material 설정을 해줘야 한다
``` C++
SceneManager.cpp

shared_ptr&lt;Scene&gt; SceneManager::LoadTestScene()
{
...
        shared_ptr&lt;Material&gt; material = RESOURCES-&gt;Get&lt;Material&gt;(L&quot;Default&quot;);
        meshRenderer-&gt;SetMaterial(material);

        shared_ptr&lt;Mesh&gt; mesh = RESOURCES-&gt;Get&lt;Mesh&gt;(L&quot;Rectangle&quot;);
        meshRenderer-&gt;SetMesh(mesh);
    }
    scene-&gt;AddGameObject(m_pMonster);

    return scene;
}</code></pre><ul>
<li>Mesh와 마찬가지로 SceneMGR에 LoadTestScene 함수에서 ResourceMGR에서 Key 값으로 저장한 Material을 찾아와 Material 변수에 저장해주면된다<h3 id="결과-1">결과<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/1d9ad612-ed96-4272-aef2-b8b31608e67f/image.png" /></h3>
</li>
<li>긴 작업을 했지만 같은 결과가 나오는 것을 볼 수 있다</li>
<li>이를 통해 GameObject에서 이것저것 다 들고 이런저런 행동을 해줬지만 이를 분리시켜 각각의 클래스가 하나의 행동을 할 수 있게 해주었고, Resource도 분리하고, 같은 Resource가 존재하면 또다시 생성하는 것이 아닌 저장되어있던 것을 가져와 사용할 수 있게 된 것이다</li>
<li>우리가 ResourceBase에 Save와 Load라는 함수를 만들고 구현은 하지 않았지만 나중에서는 리소스 파일들을 불러와 저장해주고 그 리소스들을 Load시키는 것들을 하게되면 상용엔진에서 사용하는 것처럼 될 것이다</li>
</ul>