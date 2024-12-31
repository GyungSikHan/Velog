<h2 id="인접-리스트">인접 리스트</h2>
<h3 id="인접-리스트란">인접 리스트란</h3>
<p>2차원 배열이 아닌 연결 리스트를 여러개 사용해서 만든 그래프
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/40135539-2a81-4ef3-94ef-66458a8c0196/image.png" />
이 그래프를 인접 리스트를 사용하면 밑의 리스트처럼 나타낼 수 있다
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/0728adc5-af7c-431c-a25e-32d0401b6430/image.png" /></p>
<h3 id="코드로-나타내기">코드로 나타내기</h3>
<pre><code class="language-C++">#include&lt;iostream&gt;
#include&lt;vecetor&gt;
using namespace std; 
const int V = 4;
vector&lt;int&gt; adj[V];
int main()
{
    adj[0].push_back(1);
    adj[0].push_back(2);
    adj[0].push_back(3);
    adj[1].push_back(0);
    adj[1].push_back(2);
    adj[2].push_back(0);
    adj[2].push_back(1);
    adj[3].push_back(0); 

    for(int i = 0; i &lt; 4; i++)
    {
        cout &lt;&lt; i &lt;&lt; &quot; :: &quot;;
        for(int there : adj[i])
            cout &lt;&lt; there &lt;&lt; &quot; &quot;;
        cout &lt;&lt; '\n'; 
    }
    // 이렇게도 할 수 있다.
    for(int i = 0; i &lt; 4; i++)
    {
        cout &lt;&lt; i &lt;&lt; &quot; :: &quot;;
        for(int j = 0; j &lt; adj[i].size(); j++)
            cout &lt;&lt; adj[i][j] &lt;&lt; &quot; &quot;;
        cout &lt;&lt; '\n'; 
    }
} 
/*
0 :: 1 2 3 
1 :: 0 2 
2 :: 0 1 
3 :: 0 
*/
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre>
<h3 id="list가-아닌-vector를-사용한-이유">list가 아닌 vector를 사용한 이유</h3>
<h4 id="list">list</h4>
<ul>
<li>n번째 인덱스 삽입 삭제 : O(1)</li>
<li>마지막 요소에 삽입 삭제 : O(1)</li>
<li>특정 요소 탐색 : O(n)</li>
<li>n번째 요소 참조 : O(n)<h4 id="vector">vector</h4>
</li>
<li>n번째 인덱스에 삽입 삭제 : O(n)</li>
<li>마지막 요소에 삽입 삭제 : O(1)</li>
<li>특정 요소 탐색 : O(n)</li>
<li>n번째 요소 참조 : OP(1)</li>
</ul>
<p>인접 리스트를 구현할 때 많이 사용되는 연산은 마지막 요소에 삽입과 해당 배열을 탐색하는 연산이기 때문에 vector로 구현해도 무방함
따라서 vector나 list 편한것으로 구현해도 무방</p>
<h3 id="예시-문제">예시 문제</h3>
<pre><code>Q. 인접리스트를 기반으로 탐색하기
1번.
정점은 0번 부터 9번까지 10개의 노드가 있다. 1 - 2 /  1 - 3 / 3 - 4 라는 경로가 있다. (1번과 2번, 1번과 3번, 3번과 4번은 연결되어있다.) 

이를 인접리스트로 표현한다면? 
2번. 

0번부터 방문안한 노드를 찾고 해당 노드부터 방문, 연결된 노드를 이어서 방문해서 출력하는 재귀함수를 만들고 싶다면 어떻게 해야할까? 또한, 정점을 방문하고 다시 방문하지 않게 만드려면 어떻게 해야할까? 

[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</code></pre><pre><code class="language-C++">#include&lt;iostream&gt;
#include &lt;vector&gt;

using namespace std;

const int length = 10;
vector&lt;vector&lt;int&gt;&gt; list(length);
bool visited[length];

void Go(int index)
{
    cout &lt;&lt; index &lt;&lt; endl;
    visited[index] = true;
    for (int data : list[index])
    {
        if (visited[data] == false)
            Go(data);
    }
}

int main()
{
    list[1].push_back(2);
    list[1].push_back(3);

    list[2].push_back(1);

    list[3].push_back(1);
    list[3].push_back(4);

    list[4].push_back(3);

    for (int i = 0; i &lt; length; i++)
        if (list[i].size() != 0 &amp;&amp; visited[i] == false)
            Go(i);
}</code></pre>