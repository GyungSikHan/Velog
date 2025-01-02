<h2 id="dfs">DFS</h2>
<h3 id="정의">정의</h3>
<ul>
<li>그래프를 탐색할때 사용하는 알고리즘으로 어떤 노드부터 시작해 인접한 노드들을 재귀적으로 방문하며 방문한 정점은 다시 방문하지 않으며 각 분기마다 가장 멀리있는 노드까지 탐색하는 알고리즘<h3 id="수도코드">수도코드</h3>
<pre><code class="language-C++">DFS(u, adj
  u.visited = true
  for each v ∈ adj[u]
      if v.visited == false
          DFS(v, adj)</code></pre>
<ul>
<li>어떤 정점의 u의 visited를 참으로 바꾸고 u로부터 연결되어 있는 v지점을 탐색</li>
<li>이때 방문하지 않았었다면 노드에 대해 재귀적으로 DFS 호출<h3 id="구현-방법">구현 방법</h3>
</li>
</ul>
<ol>
<li>돌다리를 두들겨 보기<ul>
<li>방문이 되어어있지 않으면 방문을 하고 그렇지 않으면 방문을 하지 않는 방법<pre><code class="language-C++">void DFS(int here
{
visited[here] = true;
for(int there : adj[here]
{
 if(visited[there] == true)
     continue;
 //visited[there] = true; // 방문 처리를 여기서 해도 됨
 DFS(there);
}
}</code></pre>
</li>
</ul>
</li>
</ol>
</li>
</ul>
<ol start="2">
<li>못먹어도 GO<ul>
<li>방문했던 안했던 일단 DFS를 호출하고 해당 함수에서 방문되었다면 return을 해 함수를 종료시키는 방법<pre><code class="language-C++">void DFS(int here
{
if(visited[here] == true)
  return;
visited[here] = true;
for(int there : adj[here]
  DFS(there);
}</code></pre>
<h3 id="연습-문제">연습 문제</h3>
<pre><code>Q. 종화는 방구쟁이야!
</code></pre></li>
</ul>
</li>
</ol>
<p>종화는 21세기 유명한 방구쟁이다. 종화는 방구를 낄 때 &quot;이러다... 다 죽어!!&quot; 를 외치며 방구를 뀌는데 이렇게 방귀를 뀌었을 때  방귀는 상하좌우 네방향으로 뻗어나가며 종화와 연결된 &quot;육지&quot;는 모두 다 오염된다. &quot;바다&quot;로는 방구가 갈 수 없다. 맵이 주어졌을 때 종화가 &quot;이러다... 다 죽어!!&quot;를 &quot;최소한&quot; 몇 번외쳐야 모든 육지를 오염시킬 수 있는지 말해보자. 1은 육지며 0은 바다를 가리킨다. </p>
<p>입력
맵의 세로길이 N과 가로길이 M 이 주어지고 이어서 N * M의 맵이 주어진다. </p>
<p>출력
 &quot;이러다... 다 죽어!!&quot;를 몇 번외쳐야하는지 출력하라. </p>
<p>범위
1 &lt;= N &lt;= 100
1 &lt;= M &lt;= 100 </p>
<p>예제입력
5 5
1 0 1 0 1
1 1 0 0 1
0 0 0 1 1
0 0 0 1 1
0 1 0 0 0
예제출력
4
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</p>
<pre><code>```C++
#include &lt;iostream&gt;
#include&lt;vector&gt;

using namespace std;
int dy[4] = { 0,-1,0,1 };
int dx[4] = { -1,0,1,0 };
int n, m,Count;
vector&lt;vector&lt;int&gt;&gt; map;
vector&lt;vector&lt;bool&gt;&gt; visited;

void DFS(int y, int x)
{
    visited[y][x] = true;
    for (int i = 0; i &lt; 4; i++)
    {
        int ny = dy[i] + y;
        int nx = dx[i] + x;

        if (ny &gt;= 0 &amp;&amp; ny &lt; n &amp;&amp; nx &gt;= 0 &amp;&amp; nx &lt; m)
            if (map[ny][nx] == 1 &amp;&amp; visited[ny][nx] == false)
                DFS(ny, nx);
    }
}

int main()
{
    cin &gt;&gt; n &gt;&gt; m;
    map.resize(n, vector&lt;int&gt;(m, 0));
    visited.resize(n, vector&lt;bool&gt;(m, false));

    for (int i = 0; i &lt; n; i++)
        for (int j = 0; j &lt; m; j++)
            cin &gt;&gt; map[i][j];

    for (int i = 0; i &lt; n; i++)
    {
        for (int j = 0; j &lt; m; j++)
        {
            if (map[i][j] == 1 &amp;&amp; visited[i][j] == false)
            {
                Count++;
                DFS(i, j);
            }
        }
    }

    cout &lt;&lt; Count &lt;&lt; endl;
}</code></pre><h3 id="디버깅-팁">디버깅 팁</h3>
<ul>
<li><p>DFS가 퍼져나가는 것이 상상이 안될땐 노드나 좌표를 출력해보면 된다</p>
<pre><code class="language-C++">위의 문제로 예시
void DFS(int y, int x)
{
  cout &lt;&lt; y &lt;&lt; &quot; : &quot; &lt;&lt; x &lt;&lt; '\n'; // 현재 좌표를 출력하여 어떻게 퍼져나가는지 확인해 볼 수 있다
  visited[y][x] = true;
  for (int i = 0; i &lt; 4; i++)
  {
      int ny = dy[i] + y;
      int nx = dx[i] + x;

      if (ny &gt;= 0 &amp;&amp; ny &lt; n &amp;&amp; nx &gt;= 0 &amp;&amp; nx &lt; m)
          if (map[ny][nx] == 1 &amp;&amp; visited[ny][nx] == false)
              DFS(ny, nx);
  }
}</code></pre>
</li>
</ul>