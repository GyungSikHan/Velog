<h2 id="인접행렬">인접행렬</h2>
<h3 id="정의">정의</h3>
<ul>
<li>그래프에서 정점과 간선의 관계를 나타내는 bool 타입 정사각형 행렬</li>
<li>행렬의 요소가 0 또는 1이라는 값을 가지며 0은 두 정점 사이의 경로가 없고 1은 두 정점 사이의 경로가 존재함을 의미</li>
<li>무방향 그래프는 양방향 그래프로 봐도 무방함<h3 id="행렬로-만들어보기">행렬로 만들어보기</h3>
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/bcd463ef-c9b9-4e37-bdb1-e6b07a5d9500/image.png" /></li>
<li>위의 무방향 그래프를 행렬로 만들기 위해 노드의 갯수만큼 2차원 배열로 만들어 줌</li>
<li>시작 노드를 첫번째 index로 간선이 연결된 노드들을 두번째 index로 하여 배열을 채워줌<pre><code class="language-C++">bool arr[4][4] = {
  {0, 1, 1, 1},
  {1, 0, 1 ,0},
  {1, 1, 0, 0},
  {1, 0, 0, 0},
}</code></pre>
</li>
<li>코드를 구축하기 위해 2중 for문을 통해 i에서 j로 가는 경로가 있다면 해당 정점으로부터 탐색을 하는 다양한 알고리즘을 통해 로직을 구축</li>
<li>y축을 중심으로 x축을 탐색하는게 더 좋다<h3 id="q-인접행렬을-기반으로-탐색하기">Q. 인접행렬을 기반으로 탐색하기</h3>
<pre><code>1번.
정점은 0번 부터 9번까지 10개의 노드가 있다. 1 - 2 /  1 - 3 / 3 - 4 라는 경로가 있다. (1번과 2번, 1번과 3번, 3번과 4번은 연결되어있다.) 
이를  이를 인접행렬로 표현한다면? 
2번. 
0번부터 방문안한 노드를 찾고 해당 노드부터 방문, 연결된 노드를 이어서 방문해서 출력하는 재귀함수를 만들고 싶다면 어떻게 해야할까? 또한, 정점을 방문하고 다시 방문하지 않게 만드려면 어떻게 해야할까? 
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre><pre><code class="language-C++">#include &lt;iostream&gt;
</code></pre>
</li>
</ul>
<p>using namespace std;</p>
<p>bool arr[10][10];
bool visited[10];</p>
<p>void Go(int from)
{
    visited[from] = true;
    cout &lt;&lt; from &lt;&lt; endl;
    for (int i = 0; i &lt; 10; i++)
    {
        if (visited[i] == false &amp;&amp; arr[from][i] == 1)
            Go(i);
    }
}</p>
<p>int main()
{
    arr[1][2] = true;
    arr[2][1] = true;
    arr[1][3] = true;
    arr[3][1] = true;
    arr[3][4] = true;
    arr[4][3] = true;</p>
<pre><code>for (int i = 0; i &lt; 10; i++)
{
    for (int j = 0; j &lt; 10; j++)
    {
        if (visited[i] == false &amp;&amp; arr[i][j] == true)
            Go(i);
    }
}</code></pre><p>}
```</p>