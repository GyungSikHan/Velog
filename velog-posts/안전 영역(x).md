<p><a href="https://www.acmicpc.net/problem/2468">https://www.acmicpc.net/problem/2468</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;vector&gt;

using namespace std;
int dy[4] = { 0,-1,0,1 };
int dx[4] = { -1,0,1,0 };
int n;
int arr[101][101];
bool visited[101][101];
int Maxdata;
int Maxcount;

void DFS(int data, int y, int x)
{
    visited[y][x] = true;
    for (int i = 0; i &lt; 4; i++)
    {
        int ny = y + dy[i];
        int nx = x + dx[i];

        if(ny &gt;= 0 &amp;&amp; ny &lt; n &amp;&amp; nx &gt;= 0 &amp;&amp; nx &lt;n)
        {
            if(visited[ny][nx] == false &amp;&amp; arr[ny][nx] &gt; data)
            {
                DFS(data, ny, nx);
            }
        }
    }
}

int main()
{
    cin &gt;&gt; n;
    for (int i = 0; i &lt; n; i++)
    {
        for (int j = 0; j &lt; n; j++)
        {
            int temp{};
            cin &gt;&gt; temp;
            arr[i][j] = temp;
            Maxdata = max(Maxdata, temp);
        }
    }
    int temp{};
    for (int k = 0; k &lt;= Maxdata; k++)
    {
        Maxcount = 0;
        fill(&amp;visited[0][0], &amp;visited[0][0] + 101 * 101,0);
        for (int i = 0; i &lt; n; i++)
        {
            for (int j = 0; j &lt; n; j++)
            {
                if (visited[i][j] == false &amp;&amp; arr[i][j] &gt; k)
                {
                    Maxcount++;
                    DFS(k, i, j);
                }
            }
        }
        temp = max(Maxcount, temp);
    }

    cout &lt;&lt; temp &lt;&lt; endl;
}</code></pre>
<ul>
<li>입력받은 값 중 가장 큰 값을 저장해놓고 3중 for문을 돌면서 비가 내리지 않았을 때 부터 MaxData까지 잠겼을 때 까지 for문을 돌면서 맵의 시작 위치를 for문으로 바꿔가며 DFS를 풀어주면 된다</li>
<li>이때 DFS를 호출할 조건은 visited[i][j]가 false이고 arr[i][j]가 현재 비가 내린 양 k보다 커야한다</li>
</ul>