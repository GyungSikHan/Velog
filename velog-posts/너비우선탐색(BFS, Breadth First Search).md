<h2 id="bfs">BFS</h2>
<h3 id="정의">정의</h3>
<ul>
<li>그래프를 탐색하는 알고리즘으로 어떤 정점에서 시작해 다음 깊이의 정점으로 이동하기 전 현재 깊이의 모든 정점을 탐색하며 방문한 정점은 다시 방문하지 않는 알고리즘</li>
<li>가중치를 가진 그래프에서 최단거리 알고리즘으로 많이 쓰임
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/ca74b554-2296-4011-ab84-9ea007ba7c93/image.png" /></li>
<li>레이어별, 레벨별로 탐색한다는 뜻<h3 id="수도코드">수도코드</h3>
</li>
</ul>
<ol>
<li>시작 지점을 방문처리를 하고 queue에 push한뒤 queue가 비어있지 않다면 while 반복문을 통해 queue의 앞단에 있는 값을 꺼내 그 값을 중심으로 인접한 노드들을 탐색하는 방법으로 방문한 정점은 방문하지 않고 그렇지 않았다면 방문처리를 해주면서 queue에 push하면서 방문처리를 함<pre><code class="language-C++">BFS(G, u)
 u.visited = true
 q.push(u);
 while(q.empaty()) 
     u = q.front() 
     q.pop()
     for each v ∈ G.Adj[u]
         if v.visited == false
             v.visited = true
             q.push(v) </code></pre>
</li>
<li>1번 방법은 방문처리만 하는 코드로 같은 가중치가 존재할 때 최단거리 알고리즘으로 사용하는 방법으로 최단거리 배열을 방문하면서 만들어줌<pre><code class="language-C++">BFS(G, u)
 u.visited = 1
 q.push(u);
 while(q.empaty()) 
     u = q.front() 
     q.pop()
     for each v ∈ G.Adj[u]
         if v.visited == false
             v.visited = u.visited + 1
             q.push(v) </code></pre>
<h3 id="qna">QNA</h3>
</li>
<li>가중치가 1이 아닌 다른 수일때<ul>
<li>시작 정점부터 도착 정점까지 레벨을 구해 그 차이에 가중치를 곱해주면 됨</li>
</ul>
</li>
<li>시작 지점이 다수일 경우 <ul>
<li>시작 지점을 모두 최단거리 배열을 1로 초기화한 후 시작</li>
</ul>
</li>
<li>왜 가중치가 같은 그래프에서만 사용가능한가?<ul>
<li>다른 가중치의 합을 표현할 방법이 없음(사실 가중치를 변수로 받아 표현하는 등 방법이 있지만 다른 알고리즘이 더 효율적)</li>
<li>더 좋은 가중치가 다른 최단거리 알고리즘이 존재 : 다익스트라, 벨만포드 등<h3 id="예시-문제">예시 문제</h3>
<pre><code>예시문제. 당근마킷 엔지니어 승원이
</code></pre></li>
</ul>
</li>
</ol>
<p>승원이는 당근을 좋아해서 당근마킷에 엔지니어로 취업했다. 당근을 매우좋아하기 때문에 차도 당근차를 샀다. 이 당근차는 한칸 움직일 때마다 당근을 내뿜으면서 간다. 즉, &quot;한칸&quot; 움직일 때 &quot;당근한개&quot;가 소모된다는 것이다. 승원이는 오늘도 아침 9시에 일어나 당근마킷으로 출근하고자 한다. 승원이는 최단거리로 당근마킷으로 향한다고 할 때 당근몇개를 소모해야 당근마킷에 갈 수 있는지 알아보자. 이 때 승원이는 육지로만 갈 수 있으며 바다로는 못간다. 맵의 1은 육지며 0은 바다를 가리킨다. 승원이는 상하좌우로만 갈 수 있다. </p>
<p>입력
맵의 세로길이 N과 가로길이 M 이 주어지고 이어서 N * M의 맵이 주어진다. 그 다음 줄에 승원이의 위치(y, x)와 당근마킷의 위치(y, x)가 주어진다. 이 때 승원이의 시작위치(y, x)에서 &quot;당근한개&quot;가 이미 소모된 상태로 본다.
출력
당근을 몇개 소모해야 하는지 출력하라.
범위
1 &lt;= N &lt;= 100
1 &lt;= M &lt;= 100 
예제입력
5 5
0 0
4 4
1 0 1 0 1
1 1 1 0 1
0 0 1 1 1
0 0 1 1 1
0 0 1 1 1
예제출력</p>
<p>9
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</p>
<pre><code>```C++
#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;
int dy[4] = { 0,-1,0,1 };
int dx[4] = { -1,0,1,0 };
int n, m,sy,sx,cy,cx;
vector&lt;vector&lt;int&gt;&gt; map;
vector&lt;vector&lt;int&gt;&gt; visited;

void BFS(int y, int x)
{
    visited[y][x] = 1;
    queue&lt;pair&lt;int, int&gt;&gt; q;
    q.push({ y,x });
    int level = 1;
    while (q.empty() == false)
    {
        int curry = q.front().first;
        int currx = q.front().second;
        if(curry == cy &amp;&amp; currx == cx)
            break;
        q.pop();

        for (int i = 0; i &lt; 4; i++)
        {
            int nexty = curry + dy[i];
            int nextx = currx + dx[i];
            if(nexty &gt;= 0 &amp;&amp; nexty &lt; n &amp;&amp; nextx &gt;= 0 &amp;&amp; nextx &lt; m)
            {
                if(map[nexty][nextx] == 1 &amp;&amp; visited[nexty][nextx] == 0)
                {
                    visited[nexty][nextx] = visited[curry][currx] + 1;
                    q.push({ nexty,nextx });
                }
            }
        }
    }
}

int main()
{
    cin &gt;&gt; n &gt;&gt; m;
    cin &gt;&gt; sy &gt;&gt; sx;
    cin &gt;&gt; cy &gt;&gt; cx;
    map.resize(n, vector&lt;int&gt;(m, 0));
    visited.resize(n, vector&lt;int&gt;(m, 0));

    for (int i = 0; i &lt; n; i++)
        for (int j = 0; j &lt; m; j++)
            cin &gt;&gt; map[i][j];

    BFS(sy, sx);

    cout &lt;&lt; visited[cy][cx] &lt;&lt; endl;
}</code></pre>