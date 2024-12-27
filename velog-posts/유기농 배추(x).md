<p><a href="https://www.acmicpc.net/problem/1012">https://www.acmicpc.net/problem/1012</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;
int dy[4] = { 0,-1,0,1 };
int dx[4] = { -1,0,1,0 };
int t, n, m, k;
queue&lt;pair&lt;int, int&gt;&gt;q;
int farm[51][51], visited[51][51];

int butterfly;

void DFS(int y, int x)
{
    visited[y][x] = true;
    for (int i = 0; i &lt; 4; i++)
    {
        int Y = y + dy[i];
        int X = x + dx[i];

        if (Y &gt;= 0 &amp;&amp; Y &lt; n &amp;&amp; X &gt;= 0 &amp;&amp; X &lt; m)
        {
            if (farm[Y][X] == 1 &amp;&amp; visited[Y][X] == false)
                DFS(Y, X);
        }
    }
}


int main()
{
    cin &gt;&gt; t;
    while (t--)
    {
        cin &gt;&gt; n &gt;&gt; m &gt;&gt; k;
        butterfly = 0;
        fill(&amp;farm[0][0], &amp;farm[0][0]+51*51,0);
        fill(&amp;visited[0][0], &amp;visited[0][0]+51*51, 0);
        for (int i = 0; i &lt; k; i++)
        {
            int a{}, b{};
            cin &gt;&gt; a &gt;&gt; b;
            farm[a][b] = 1;
        }

        for (int i = 0; i &lt; n; i++)
        {
            for (int j = 0; j &lt; m; j++)
            {
                if(farm[i][j] == 1 &amp;&amp; visited[i][j] == 0)
                {
                    butterfly+=1;
                    DFS( i, j);
                }
            }
        }
        cout &lt;&lt; butterfly &lt;&lt; endl;
    }
}</code></pre>
<ul>
<li>BFS로 풀었는데 메모리 초과가 떳다</li>
<li>BFS보다는 DFS가 메모리가 더 적게 들기 때문에 DFS로 바꿔서 구현하면 풀린다</li>
</ul>