<h2 id="scene">Scene</h2>
<hr />
<ul>
<li>Scene는 게임에서 관리하는 오브젝트들을 묶어서 통합으로 관리하는 클래스가 될 것이다</li>
<li>즉 하나의 맵, 오브젝트, UI등을 모아 놓은 게임의 단위를 말한다</li>
</ul>
<pre><code class="language-cpp">Scene.h
{
public:
    const vector&lt;shared_ptr&lt;GameObject&gt;&gt;&amp; GetGameObjects() { return m_pGameObjects; }
private:
    vector&lt;shared_ptr&lt;GameObject&gt;&gt; m_pGameObjects;
}
-------------------------------------------------------------------------------------
Scene.cpp

void Scene::Awake()
{
    for (const shared_ptr&lt;GameObject&gt;&amp; game : m_pGameObjects)
        game-&gt;Awake();
}

void Scene::Start()
{
    for (const shared_ptr&lt;GameObject&gt;&amp; game : m_pGameObjects)
        game-&gt;Start();
}

void Scene::Update()
{
    for (const shared_ptr&lt;GameObject&gt;&amp; game : m_pGameObjects)
        game-&gt;Update();
}

void Scene::LateUpdate()
{
    for (const shared_ptr&lt;GameObject&gt;&amp; game : m_pGameObjects)
        game-&gt;LateUpdate();
}

void Scene::FixedUpdate()
{
    for (const shared_ptr&lt;GameObject&gt;&amp; game : m_pGameObjects)
        game-&gt;FixedUpdate();
}

void Scene::AddGameObject(shared_ptr&lt;GameObject&gt; gameObject)
{
    m_pGameObjects.push_back(gameObject);
}

void Scene::RemoveGameObject(shared_ptr&lt;GameObject&gt; gameObject)
{
    vector&lt;shared_ptr&lt;GameObject&gt;&gt;::iterator iter = std::find(m_pGameObjects.begin(), m_pGameObjects.end(), gameObject);
    if (iter != m_pGameObjects.end())
        m_pGameObjects.erase(iter);
}
</code></pre>
<ul>
<li>GetGameObjects() 함수는 맴버 변수인 m_pGameObjects를 리턴해주는 함수이다</li>
<li>Awake, Start, Update, LateUpdate, FixedUpdate 함수들은 m_pGameObjects 변수를 가지고 for each을 사용하여 변수에 저장된 모든 GameObject들의 같은 이름의 함수들을 실행시켜 준다</li>
<li>AddGameObject() 함수는 말 그대로 GameObject 변수를 가져와 m_pGameObject안에 push_back해 Scene에 오브젝트를 추가해주는 함수이다</li>
<li>RemoveGameObject() 함수는 GameObject 변수를 가져와 m_pGameObject 안에 있다면 지워주는 함수로 Scene에 오브젝트를 제거하는 함수이다</li>
</ul>
<h2 id="scenemanager">SceneManager</h2>
<hr />
<ul>
<li>SceneManager는 여러개의 씬 중 하나를 들고있는 목적을 가진 클래스가 될 것이다</li>
<li>즉 현재 화면에 나온 Scene을 들고 있을 것이다</li>
</ul>
<pre><code class="language-cpp">SceneManager.h
{
public:
    shared_ptr&lt;Scene&gt; GetActiveScene() { return m_pActiveScene; }
private:
    shared_ptr&lt;Graphics&gt; m_pGraphics;
    shared_ptr&lt;Scene&gt; m_pActiveScene;
}
---------------------------------------------------------------------------------------
SceneManager.cpp
SceneManager::SceneManager(shared_ptr&lt;Graphics&gt; graphics)
    :m_pGraphics(graphics)
{
}

void SceneManager::Init()
{
    if(m_pActiveScene == nullptr)
        return;

    m_pActiveScene-&gt;Awake();
    m_pActiveScene-&gt;Start();
}

void SceneManager::Update()
{
    if (m_pActiveScene == nullptr)
        return;

    m_pActiveScene-&gt;Update();
    m_pActiveScene-&gt;LateUpdate();

    m_pActiveScene-&gt;FixedUpdate();
}

void SceneManager::LoadScene(wstring sceneName)
{
    m_pActiveScene = LoadTestScene();
    Init();
}

shared_ptr&lt;Scene&gt; SceneManager::LoadTestScene()
{
    //게임 엔진은 Scene을 선택해서 입장할 수 있게 만들어야 하지만
    //지금 단계에서는 하나의 특정 Scene만 띄우게 할 것이다

    shared_ptr&lt;Scene&gt; scene = make_shared&lt;Scene&gt;();

    //Camera
    shared_ptr&lt;GameObject&gt; m_pCamera = make_shared&lt;GameObject&gt;(m_pGraphics-&gt;GetDevice(), m_pGraphics-&gt;GetDeviceContext());
    {
        m_pCamera-&gt;GetOrAddTransform();
        m_pCamera-&gt;AddComponent(make_shared&lt;Camera&gt;());
        scene-&gt;AddGameObject(m_pCamera);
    }

    //monster
    shared_ptr&lt;GameObject&gt; m_pMonster = make_shared&lt;GameObject&gt;(m_pGraphics-&gt;GetDevice(), m_pGraphics-&gt;GetDeviceContext());
    {
        m_pMonster-&gt;GetOrAddTransform();
        m_pMonster-&gt;AddComponent(make_shared&lt;MeshRenderer&gt;(m_pGraphics-&gt;GetDevice(), m_pGraphics-&gt;GetDeviceContext()));
        //m_pMonster-&gt;GetTransform()-&gt;SetScale(Vec3(100.0f, 100.0f, 100.0f));
        scene-&gt;AddGameObject(m_pMonster);
    }

    return scene;
}</code></pre>
<ul>
<li>생성자에서는 Graphics 변수를 가져와 m_pGraphics 매개변수에 저장해준다</li>
<li>Init 함수에서는 m_pActiveScene 변수가 null이 아닐때 m_pActiveScene 변수를 통해 Awake(), Start() 함수를 호출하는 역할을 한다</li>
<li>Update() 함수 역시 Init 함수와 마찬가지로 m_pActiveScene가 null이 아니면 Update(), LateUpdate(), FixedUpdate() 함수를 호출하는 역할이다</li>
<li>LoadScene() 함수는 wstring으로 SceneManager에서 관리할 Scene을 가져와주고 지금은 아니지만 나중에 사용할 수 있게 해준다</li>
<li>또한 m_pActiveScene 안에 LoadTestScene()함수에 리턴된 Scene을 저장하고 Init() 함수를 호출해주는 역할을 한다</li>
<li>LoadTestScene은 Game Class에 Init() 함수에서 Camera와 m_pMonster 오브젝트를 만들고 Transform과 Component에 추가를 해준 뒤 Scene에 GameObject에 추가하여 각각의 정보를 추가하고 Scene에 배치될 오브젝트로 추가해준다</li>
<li>이렇게 저장된 Scene 변수를 리턴해주는 함수이다</li>
</ul>
<h2 id="game">Game</h2>
<hr />
<ul>
<li>Game class에서 GameObject를 추가하고 그 오브젝트를 렌더하는 부분을 지우고 SceneManager를 추가해 Scene을 관리하게 바꿔줄 것이다</li>
</ul>
<pre><code class="language-cpp">Game.h
{
public:
    shared_ptr&lt;SceneManager&gt; GetSceneManager() { return m_pScene; }
private:
    shared_ptr&lt;SceneManager&gt; m_pScene;
};

extern unique_ptr&lt;Game&gt; GGame;
---------------------------------------------------------------------------------------
#define GAME GGame
#define SCENE GGame-&gt;GetSceneManager()
---------------------------------------------------------------------------------------
Game.cpp

unique_ptr&lt;Game&gt; GGame = make_unique &lt; Game &gt;();

Game::Game()
{
}

Game::~Game()
{
    graphics.reset();

}

void Game::Init(HWND hWnd)
{
    hwnd = hWnd;

    graphics = make_shared&lt;Graphics&gt;(hwnd);
    pipeline = make_shared&lt;Pipeline&gt;(graphics-&gt;GetDeviceContext());
    m_pScene = make_shared&lt;SceneManager&gt;(graphics);

    SCENE-&gt;LoadScene(L&quot;Test&quot;);
}

void Game::Update()
{
    graphics-&gt;RenderBegin();
    SCENE-&gt;Update();
    graphics-&gt;RenderEnd();
}

void Game::Render()
{
}</code></pre>
<ul>
<li>Game Class를 전역에서 사용하기 위해 싱글톤으로 만들어도 되지만 unique_ptr&lt;&gt;을 통해 만들어 줬다</li>
<li>미리컴파일된 헤더에서 #define을 통해 매크로를 설정해주는데 굳이 안해도 된다</li>
<li>기존에 Init() 함수에서 GameObject를 추가하는 부분을 지우고 m_pScene을 동적으로 할당하고 만들어 놓은 메크로를 통해 m_pScene에 LoadScene() 함수를 호출하여 Scene을 Load해준다</li>
<li>Render() 함수에서 Graphics안에 RenderBegin(), RenderEnd() 함수를 Update로 옮겨주고 두 코드 사이에 SCENE 메크로를 통해 Scene class의 Update 함수를 호출하여 Scene 내에 GameObject를 그려줄 준비를 한다</li>
<li>Game class를 객체로 사용했던 곳에 GGame으로 바꿔주면 이번 강의는 끝이난다</li>
</ul>
<h2 id="간단하게-정리">간단하게 정리</h2>
<hr />
<ul>
<li>이번 강의에선 지금까지 Game Class에서 GameObject를 추가하고 그리는 것을 했었지만 이를 Scene Calss로 분리하고 관리하며 이러한 Scene을 관리하는 SceneManager Class를 만드는 수업이였다</li>
</ul>