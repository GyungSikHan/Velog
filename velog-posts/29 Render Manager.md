<h2 id="render-manager">Render Manager</h2>
<ul>
<li>이제 렌더링을 RenderManager 클래스에서 하게될 것이다</li>
<li>또한 MeshRenderer 클래스에서 일부분이 전시간에 만든 Material클래스로 빠져야 된다</li>
<li>RenderManager는 SceneMGR처럼 물체를 들고 있는 Manager인대 그리는 물체들을 들고있는 클래스가 될 것이다</li>
<li>RenderHelper 클래스도 같이 만들어 렌더링시 필요한 것들을 관리할 수 있게 해줄것이다<pre><code class="language-C++">RenderHelper.h
struct TransformData
{
  Matrix World = Matrix::Identity;
};
</code></pre>
</li>
</ul>
<p>struct CameraData
{
    Matrix View = Matrix::Identity;
    Matrix Projection = Matrix::Identity;
};</p>
<pre><code>- 사실상 Struct.h에서 있던 Transform이라던지 CameraData는 렌더링시 넘겨줘야 하는 것이므로 RenderHelper.h로 옮겨준다
```C++
#pragma once
#include &quot;RenderHelper.h&quot;

class RenderMGR
{
public:
    RenderMGR(ComPtr&lt;ID3D11Device&gt; device, ComPtr&lt;ID3D11DeviceContext&gt; deviceContext);
    ~RenderMGR();

    void Init();
    void Update(shared_ptr&lt;Graphics&gt; graphics);

private:
    void PushCameraData();
    void PushTransformData();

    void GatherRenderableObjects();
    void RenderObjects();

private:
    ComPtr&lt;ID3D11Device&gt; m_pDevice;
    ComPtr&lt;ID3D11DeviceContext&gt; m_pDeviceContext;
    shared_ptr&lt;Pipeline&gt; m_pPipeline;

private:
    //Camera
    CameraData m_cCameraData;
    shared_ptr&lt;ConstantBuffer&lt;CameraData&gt;&gt; m_pCameraBuffer;

    //SRT
    TransformData m_ctransformData;
    shared_ptr&lt;ConstantBuffer&lt;TransformData&gt;&gt; m_pTransformBuffer;

    //Animation

    shared_ptr&lt;Rasterizer&gt; m_pRS;
    shared_ptr&lt;SamplerState&gt; m_pSampler;
    shared_ptr&lt;BlendState&gt; m_pBlend;

    vector&lt;shared_ptr&lt;GameObject&gt;&gt; m_vRenderObject;
};</code></pre><ul>
<li>렌더링을 위한 클래스 이므로 생성자에서 device와 deviececontext를 받아와 줄것이다</li>
<li>나중에 shared_ptr_this를 사용하게 됐을 때 생성자에서 아직 weak_ptr이 채워지지 않은 상태에서 호출을 하게되면 오류가 생기므로 Init 함수를 생성하여 여기서 기본 값들을 초기화 해줄것이다, Update시 Graphics 데이터를 가져와 Game class에 Update함수에 시작과 끝에 해주었던 Graphics-&gt;RenderBegin과 RenderEnd()를 여기서 대신하게 만들어 줄것이다</li>
<li>또한 Shader로 값을 넘겨주기위해 CameraData와 TransformData를 ConstantBuffer로 복사해주기위해 Push라는 이름의 함수들도 만들어준다</li>
<li>그림을 그릴 Objects들을 가져오는 함수와 그 Object를 그려줄 함수인 GatherRenderableObjects, RenderObjcets 함수들도 만들어준다</li>
<li>Mesh를 그리는 MeshRenderer 클래스에서 Camera, Transform 데이터를 GPU와 통신을 하기위한 버퍼로 만들어 이를 통해 메모리에 고속복사를 해서 사용을 했는데 이때 동일한 물체가 여러개 늘어났을 때 늘어난 갯수만큼 Buffer를 만들지 않고 하나만 생성하여 재사용하도록 하기위해 RenderMGR에서 들고있는것이 더 나을것이기 때문에 옮겨준다</li>
<li>마찬가지로 MeshRederer에서 파이프라인과 연관성이 있는 Rasterizer, SamplerState, BlendState역시 옮겨준다</li>
<li>렌더링할 오브젝트중 지금 현재 그려줘야할 오브젝트들을 가져와 저장해줄 수 있게 Vector로 GameObject를 배열로 저장할 수 있게 해준다<pre><code>cpp
RenderMGR::RenderMGR(ComPtr&lt;ID3D11Device&gt; device, ComPtr&lt;ID3D11DeviceContext&gt; deviceContext)
  :m_pDevice(device),m_pDeviceContext(deviceContext)
{
}
</code></pre></li>
</ul>
<p>RenderMGR::~RenderMGR()
{
}</p>
<p>void RenderMGR::Init()
{
    m_pPipeline = make_shared(m_pDeviceContext);</p>
<pre><code>//CreateCameraBuffer
m_pCameraBuffer = make_shared&lt;ConstantBuffer&lt;CameraData&gt;&gt;(m_pDevice, m_pDeviceContext);
m_pCameraBuffer-&gt;Create();
//CreateConstantBuffer
m_pTransformBuffer = make_shared&lt;ConstantBuffer&lt;TransformData&gt;&gt;(m_pDevice, m_pDeviceContext);
m_pTransformBuffer-&gt;Create();

//Rasterrize
m_pRS = make_shared&lt;Rasterizer&gt;(m_pDevice);
m_pRS-&gt;Create();

//CreateBlendState
m_pBlend = make_shared&lt;BlendState&gt;(m_pDevice);
m_pBlend-&gt;Create();

//CreateSamplerState
m_pSampler = make_shared&lt;SamplerState&gt;(m_pDevice);
m_pSampler-&gt;Create();</code></pre><p>}</p>
<p>void RenderMGR::Update(shared_ptr graphics)
{
    graphics-&gt;RenderBegin();</p>
<pre><code>PushCameraData();
GatherRenderableObjects();
RenderObjects();

graphics-&gt;RenderEnd();</code></pre><p>}</p>
<p>void RenderMGR::PushCameraData()
{
    m_cCameraData.View = Camera::m_mMatView;
    m_cCameraData.Projection = Camera::m_mProjection;</p>
<pre><code>m_pCameraBuffer-&gt;CopyData(m_cCameraData);</code></pre><p>}</p>
<p>void RenderMGR::PushTransformData()
{
    //물체마다 Transform이 다를것이므로 그때 알아서 채워주면 됨
    m_pTransformBuffer-&gt;CopyData(m_cTransformData);
}</p>
<p>void RenderMGR::GatherRenderableObjects()
{
    m_vRenderObject.clear();</p>
<pre><code>const vector&lt;shared_ptr&lt;GameObject&gt;&gt;&amp; gameObjects = SCENE-&gt;GetActiveScene()-&gt;GetGameObjects();
for (const shared_ptr&lt;GameObject&gt;&amp; gameObject : gameObjects)
{
    shared_ptr&lt;MeshRenderer&gt; mesh = gameObject-&gt;GetMeshRenderer();
    if (mesh != nullptr)
        m_vRenderObject.push_back(gameObject);
}</code></pre><p>}</p>
<p>void RenderMGR::RenderObjects()
{
    for (const shared_ptr&amp; gameObject :    m_vRenderObject)
    {
        shared_ptr mesh = gameObject-&gt;GetMeshRenderer();
        if (mesh == nullptr)
            continue;
        shared_ptr transform = gameObject-&gt;GetTransform();
        if(transform == nullptr)
            continue;</p>
<pre><code>    //SRT
    m_cTransformData.World = transform-&gt;GetWorldMatrix();
    PushTransformData();

    //IA - VS - RS - PS - OM
    PipelineInfo info;

    info.inputLayout = mesh-&gt;GetInputLayout();
    info.vertexShader = mesh-&gt;GetVertexShader();
    info.pixelShader = mesh-&gt;GetPixelShader();
    info.rs = m_pRS;
    info.blend = m_pBlend;

    m_pPipeline-&gt;UpdatePipeline(info);

    m_pPipeline-&gt;SetVertexBuffer(mesh-&gt;GetVertexBuffer());
    m_pPipeline-&gt;SetIndexBuffer(mesh-&gt;GetIndexBuffer());

    m_pPipeline-&gt;ConstantBuffer(0, EVertexShader, m_pCameraBuffer);
    m_pPipeline-&gt;ConstantBuffer(1, EVertexShader, m_pTransformBuffer);

    m_pPipeline-&gt;SetTexture(0, EPixelShader, mesh-&gt;GetTexture());
    m_pPipeline-&gt;SetSamplerState(0, EPixelShader, m_pSampler);

    m_pPipeline-&gt;DrawIndexed(mesh-&gt;GetGeometry()-&gt;GetIndexCount(), 0, 0);
}</code></pre><p>}</p>
<pre><code>- RenderMGR에서 Pipeline을 직접 만들어서 사용하기 위해 Init 함수에서 make_ptr을 통해 동적으로 할당해준 뒤 MeshRenderer에 Init 함수에서 해줬던 버퍼도 만들어주고 파이프라인에 연관되었던 Rasterizer, SamplerState, BlendState 역시 동적으로 할당해준 뒤 Create 함수를 호출해주고 MeshRenderer에서는 지워준다
- Update 함수에서는 기존 MeshRenderer에서 Pipeline-&gt;RenderBegin, RenderEnd 함수를 호출하는 것을 옮겨서 할것이다
- 또한 그 사이에 렌더링해야하는 물체들을 모두 가져오는 함수인 GaterRenderableObjects 함수와, 물체들을 렌더링하는 RenderObejcts 함수를 호출해준다
- PushCameraData 함수는 CameraData안에 있는 View와 Projection에 Camera::mMatView, Camera::m_mProjection를 각각 저장해준다
- 만약에 RenderMGR에서 카메라도 관리하려면 여러개의 카메라들 중 제일 처음에 들고있는 카메라나 특정 카메라의 값을 넘겨주는 방식을 사용할 수도 있다
- 그 후 CameraBuffer의 CopyData 함수에 CameraData 값을 넘겨주면 CPU값을 GPU로 복사해주게 되는것이다
- 마찬가지로 PushTransformData 함수에서 TransformBuffer에 CopyData를 통해 TransformData 값을 넘겨주면 GPU로 복사가 된다
- 이때 TransformData는 물체들마다 값이 다르기 때문에 알아서 채워주면 된다
- GatherRenderableObjects 함수에서는 기존 배열의 데이터를 전부 날려주고 현재 Scene에 있는 모든 물체들을 가져와 하나한 MeshRenderer가 존재하는지 판단해 존재한다면 렌더링 해야되는 물체이므로 배열에 저장해준다
- RenderObjects 함수에서는 배열에 저장된 물체들을 그려주면 되는대 배열에 있는 값들 하나하나가 MeshRenderer가 null이거나 Transform이 null이 아닌경우 TransformData안에 world값에 Transform의 월드 변환 행렬인 GetWorldMatrix 값을 저장해준뒤 PushTransformData 함수를 호출해준다
- 이렇게 되면 MeshRenderer에 Update 함수에서 Camera와 Transform을 Update하는 함수가 없어도 되므로 지워준뒤 Render함수에 있는 것들을 모두 가져와 PushTransformData를 호출해준것 밑에 붙여넣어준다
- 이렇게되면 PipelineInfo에 값을 저장해주던 변수들과 m_pPipeline에 있는 함수에 값을 넘겨주던 변수들이 MeshRenderer에 존재하지만 나중에 이들을 Mesh와 Meterial로 나눠 관리할것인데 아직은 그렇게 하지 않을 뿐더러 Get함수를 만들어 관리하기 애매하므로 MeshRenderer에서 friend 키워드를 사용해 RebderMGR에서 그 변수들을 가져와 사용할 수 있게 해준다(하지만 나는 Get 함수들을 만들어 사용했다)
- 결론은 RenderMGR에서 모든 물체들을 대상으로 렌더링을 처리해주는 클래스이고 나중에는 PipelineInfo와 Pipeline에 값을 저장하거나 그려주는 부분은 따로 함수를 만들어 관리해줄 수 있지만 현재는 공용으로 관리하는 부분과 Mesh와 Materal로 빠질 부분이 섞여있기 때문에 나눠주지 않은것이다
- 이제 MeshRenderer에 Render 함수는 없어도 되고 물체에서 MeshRenderer가 있는지 없는지 판단하여 RenderMGR에서 그려주게 되는 것이다
## RenderMGR 사용하기
- 이제 Game Class에서 RenderMGR 클래스를 사용하여 이미지를 그릴 것이다
```C++
class Game
{
...
public:
...
    shared_ptr&lt;RenderMGR&gt; GetRenderMGR() { return m_pRenderMGR; }
private:
...
    shared_ptr&lt;RenderMGR&gt; m_pRenderMGR;
};
cpp
void Game::Init(HWND hWnd)
{
...
    m_pRenderMGR = make_shared&lt;RenderMGR&gt;(graphics-&gt;GetDevice(), graphics-&gt;GetDeviceContext());
    m_pRenderMGR-&gt;Init();
...
}

void Game::Update()
{
    TIME-&gt;Update();
    INPUT-&gt;Update();
    SCENE-&gt;Update();
}

void Game::Render()
{
    RENDER-&gt;Update(graphics);
}</code></pre><ul>
<li>Game Class에서 RenderMGR 객체를 만들어주고 GetRenderMGR 함수를 통해 객체를 리턴해주는 함수도 만들어준다</li>
<li>이때 원래있던 Pipeline 객체는 RenderMGR에서 만들어 사용하므로 지워준다</li>
<li>Init 함수에서도Pipeline을 만드는 것을 지워주고 대신 RenderMGR을 make_shared를 통해 동적으로 만들어주고 Init 함수를 호출해준다</li>
<li>Update 함수에서는 Graphics를 이용해 RenderBegin과 RenderEnd를 하는것을 지워주고 Render 함수에서 RenderMGR의 Update를 호출하는 식으로 RenderBegin과 RenderEnd를 하게 바꿔줄 것이다</li>
<li>이때 미리컴파일된 헤더 pch.h에서 메크로로 #define RENDER Game-&gt;GetRenderMGR()을 만들어 편하게 사용할 수 있게 한다<h2 id="결과">결과</h2>
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/5e450dd0-a804-4186-b852-a7a7c4dc77a2/image.png" /></li>
<li>다행이 결과가 잘 나왔다</li>
<li>핵심은 나중에 조명이 추가된다고 하면 조명들도 RenderMGR에 GameObject 객체들을 저장하는 배열에 따로 들고있어 편리하게 작업할 수 있게 될것이다</li>
<li>구조는 정해지지 않았으므로 더 발전시키면 되는 것이고 중요한 것은 버퍼나 이런것을 공용으로 관리하니까 MeshRenderer가 아무리 많아도 여러개를 관리할 필요가 없고, MeshRenderer에 남아있는 Mesh나 Material을 담당하는 매개변수들만 물체마다 리소스를 들고있고 리소스를 재활용해 사용하게 되는 부분이라고 생각하면 된다</li>
</ul>