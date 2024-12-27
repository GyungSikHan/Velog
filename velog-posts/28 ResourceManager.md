<h2 id="game-class-전역-사용">Game class 전역 사용</h2>
<pre><code class="language-C++">Game class
{
    ...
}
extern unque_ptr&lt;Game&gt; GGame();</code></pre>
<ul>
<li>extern을 통해 GGame이라는 변수를 전역에서 참조할 수 있도록 만들어준다</li>
<li>이를 통해 Game 객체를 변수로 만들어서 사용했던 API에서 GGame으로 찾아서 바꿔준다</li>
<li>다 고치고 문제가 없는지 빌드를 하게되면 GameObejct의 FixedUpdate()함수에서 예외가 발생할수도 있다</li>
<li>이것을 확인해보면 component가 null일때 FixedUpdate()함수가 불려지는 것이므로 예외처리를 해준다<h2 id="이미지-안뜸">이미지 안뜸</h2>
</li>
<li>그리고 다시 실행시 창은 뜨지만 이미지는 아무것도 뜨지 않을것이다</li>
<li>이는 구조를 계속해서 바꾸면서 MeshRenderer의 Render() 함수를 어디서도 호출해주지 않기 때문이다</li>
<li>하지만 MeshRenderer에서는 어디에서도 Pipeline 변수를 가져와 Render 함수에 연결하여 그림을 그려달라 할 수 없다</li>
<li>이를 위해 Game 클래스에서 Pipeline 변수를 가져와 MeshRenderer에서 Render()를 할 수 있게 할 것이다<pre><code class="language-C++">Game class
{
...
private:
  chared_ptr&lt;Pipeline&gt; GetPipeline(){return m_pPipeline;}
...
}</code></pre>
</li>
</ul>
<hr />
<p>MeshRenderer.cpp
...
void MeshRenderer::Update()
{
...
    Render(GGame-&gt;GetPipeline())
}
...</p>
<pre><code>![](https://velog.velcdn.com/images/gksrudtlr2/post/2857d680-dced-42de-a8ec-bfeb2e2e1498/image.png)

- 이렇게 Pipeline을 가져와 MeshRenderer에서 Update마다 Render()를 호출하게 되면 지금까지 처럼 이미지가 잘 나올것이다
- 하지만 MeshRenderer를 더 수정할 계획이다
## InputMGR, TimeMGR 추가
![](https://velog.velcdn.com/images/gksrudtlr2/post/49135f3d-f03a-4b26-8e26-762ade675dc9/image.png)
- 강의에서 올려준 파일에 InputMGR과 TimeMGR을 프로젝트에 추가시켜 준다
- TimeMGR은 WinAPI에서 제공하는 기능을 통해 Update()에서 매 프레임 시간이나 FPS를 체크해주는 기능이 구현되어있다
- InputMGR은 현재 어떠한 키가 눌렸는지를 판단하거나 눌렀을 때, 누르고 있을 때, 키를 땟을 때 등을 판단해주는 기능이 구현되어있다
```C++
Game class
class InputManager;
class TimeManager;
{
...
public:
    shared_ptr&lt;InputManager&gt; GetInputMGR() {return m_pInputMGR;}
    shared_ptr&lt;TimeManager&gt; GetTimeMGR() { return m_pTimeMGR; }
    ...
private:
    shared_ptr&lt;InputManager&gt; m_pInputMGR;
    shared_ptr&lt;TimeManager&gt; m_pTimeMGR;
}</code></pre><ul>
<li>이 파일들을 사용하기 위해 Game class에 전방선언 후 변수로 생성하여 외부에서 사용할 수 있게 만든다<pre><code class="language-C++">pch.h
#define INPUT GAME-&gt;GetInputMGR()
#define TIME GAME-&gt;GetTimeMGR()</code></pre>
</li>
<li>많이 사용할수도 있으므로 pch.h에 메크로를 만들어 놔도 괜찮다<pre><code class="language-C++">Game.cpp
...
void Game::Init(HWND hWnd)
{
  ...
  m_pInputMGR = make_shared&lt;InputManager&gt;();
  m_pInputMGR-&gt;Init(hwnd);
  m_pTimeMGR = make_shared&lt;TimeManager&gt;();
  m_pTimeMGR-&gt;Init();
  ...
}
</code></pre>
</li>
</ul>
<p>void Game::Update()
{
    ...
    TIME-&gt;Update();
    INPUT-&gt;Update();
    ...
}
...</p>
<p>```</p>
<ul>
<li>InputMGR과 TimeMGR도 역시 make_shared&lt;&gt;()를 통해 동적 할당과 함께 초기화를 해주고, Update()함수에서 Update()될때 마다 호출해줘야 하므로 위의 코드도 추가해준다</li>
</ul>
<p>MeshRenderer에 너무 많은 기능이 있고 같은 메쉬가 여러개 그려진다 할때 모든 메쉬들이 MeshRenderer를 가지고 있을 것이다
이때 문제점이 각각의 메쉬마다 Gemoetry, VertexBuffer등 동일한 데이터를 써도 되는 애들이 메쉬의 갯수만큼 만들어지는 문제가 생긴다</p>