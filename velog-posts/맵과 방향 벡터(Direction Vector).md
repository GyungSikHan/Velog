<h2 id="map으로-된-방향-벡터">Map으로 된 방향 벡터</h2>
<p><img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/347596c3-6bff-4dc6-a929-bd81b290faed/image.png" /></p>
<h3 id="맵으로-주어짐">맵으로 주어짐</h3>
<ul>
<li><p>위의 그림처럼 Map으로 주어지는 그래프 문제들이 있다</p>
</li>
<li><p>맵은 하나의 그래프로 4가지 방향으로 한칸씩 움직이며 탐색이 가능하다 생각하면 된다</p>
</li>
<li><p>이때 맵은 인접 행렬이 절대 아니다!!!</p>
<h3 id="4방향-탐색과-방향-벡터">4방향 탐색과 방향 벡터</h3>
</li>
<li><p>4가지 방향인 상하좌우를 y,x 축을 중심으로 움직일 수 있을 것이다</p>
</li>
<li><p>이때 갈 수 있는 방향을 각각 배열로 만들어 움직이는 방향을 저장해준다</p>
<pre><code class="language-C++">int dy[4] = { 1,0,-1,0};
int dx[4] = {0,1,0,-1};
for    (int i = 0; i &lt; 4 &lt; i++)
{
  ny = dy[i] + y;
  nx = dy[i] + x;
}</code></pre>
<h3 id="예시-문제">예시 문제</h3>
<pre><code>Q1. {0, 0}좌표에서 dy, dx를 만들어 4방향(위, 오른쪽, 아래, 왼쪽)을 탐색하며 좌표를 출력하시오.
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre><pre><code class="language-C++">#include &lt;iostream&gt;
using namespace std;
int dy[4] = { 0,1,0,-1 };
int dx[4] = { -1,0,1,0 };
int main()
{
  int x{}, y{};
  for (int i = 0; i &lt; 4; i++)
  {
      int ny = y + dy[i];
      int nx = x + dx[i];
      cout &lt;&lt; ny &lt;&lt; &quot; &quot; &lt;&lt; nx &lt;&lt; endl;
  }
}</code></pre>
<pre><code>Q2.  {0, 0}좌표에서 dy, dx를 만들어 8방향(위, 오른쪽, 아래, 왼쪽 및 대각선방향포함)을 탐색하며 좌표를 출력하시오.
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre><pre><code class="language-C++">#include &lt;iostream&gt;
using namespace std;
int dy[8] = { 0,1,1,1,0,-1,-1,-1 };
int dx[8] = { -1,-1,0,1,1,1,0,-1 };
int main()
{
  int y{}, x{};
  for (int i = 0; i &lt; 8; i++)
  {
      int ny = y + dy[i];
      int nx = x + dx[i];
      cout &lt;&lt; ny &lt;&lt; &quot; &quot; &lt;&lt; nx &lt;&lt; endl;
  }
}</code></pre>
<pre><code>Q. 3 * 3 맵을 입력받아야 함. 이 맵은 1과 0으로 이루어져있고 {0, 0}은 무조건 1임을 보장한다. {0, 0}부터 4방향을 기준으로 한칸씩 탐색해나가며 방문한 정점은 다시 방문하지 않으며 방문하는 좌표를 출력하는 코드. 0은 갈 수 없는 지역. 1은 갈 수 있는 지역을 구현하시오.
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre><pre><code class="language-C++">#include &lt;iostream&gt;
using namespace std;
int arr[3][3];
bool visited[3][3];
int dy[4] = { 0,1,0,-1 };
int dx[4] = { -1,0,1,0 };
void Go(int y, int x)
{
  visited[y][x] = true;
  cout &lt;&lt; y &lt;&lt; &quot; &quot; &lt;&lt; x &lt;&lt; endl;
  for (int i = 0; i &lt; 4; i++)
  {
      int ny = dy[i] + y;
      int nx = dx[i] + x;

      if(ny &gt;= 0 &amp;&amp; ny &lt; 3 &amp;&amp; nx &gt;= 0 &amp;&amp;nx &lt; 3)
          if (visited[ny][nx] == false &amp;&amp; arr[ny][nx] != 0)
              Go(ny, nx);
  }
}
int main()
{
  arr[0][0] = 1;

  for (int i = 0; i &lt; 3; i++)
      for (int j = 0; j &lt; 3; j++)
          cin &gt;&gt; arr[i][j];
  Go(0, 0);
}</code></pre>
</li>
</ul>