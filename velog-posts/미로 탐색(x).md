<p><a href="https://www.acmicpc.net/problem/2178">https://www.acmicpc.net/problem/2178</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;
using namespace std;

int dx[4] = { -1,0,1,0 };
int dy[4] = { 0,-1,0,1 };
int n, m;
queue&lt;pair&lt;int, int&gt;&gt; q;
vector&lt;vector&lt;int&gt;&gt; v;
vector&lt;vector&lt;int&gt;&gt; visited;

void BFS(int y, int x)
{
    q.push({y, x});
    visited[y][x] = 1;

    while (q.empty() == false)
    {
        int curry = q.front().first;
        int currx = q.front().second;
        q.pop();

        for (int i = 0; i &lt; 4; i++)
        {
            int ny = curry + dy[i];
            int nx = currx + dx[i];
            if(ny &gt;=0 &amp;&amp; ny &lt; n &amp;&amp; nx &gt;= 0 &amp;&amp; nx &lt; m)
            {
                if(visited[ny][nx] == false &amp;&amp; v[ny][nx] == 1)
                {
                    visited[ny][nx] = visited[curry][currx] + 1;
                    q.push({ ny,nx });
                }
            }
        }
    }
}

int main()
{
    cin &gt;&gt; n &gt;&gt; m;
    v.resize(n, vector&lt;int&gt;(m, 0));
    visited.resize(n, vector&lt;int&gt;(m, 0));
    for (int i = 0; i &lt; n; i++)
        for (int j = 0; j &lt; m; j++)
            scanf_s(&quot;%1d&quot;, &amp;v[i][j]);


    BFS(0,0);
    cout &lt;&lt; visited[n-1][m-1] &lt;&lt; endl;
}</code></pre>
<ul>
<li>이상하게 DFS로 풀었는데 틀렸다</li>
<li>뭔가 잘못 풀었던 것 같지만 아에 새로 BFS를 구현하여 풀었다</li>
</ul>