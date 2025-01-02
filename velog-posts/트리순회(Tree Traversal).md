<h2 id="트리순회">트리순회</h2>
<h3 id="정의">정의</h3>
<ul>
<li>트리 구조에서 각각의 노드를 정확히 한번만, 체계적인 방법으로 방문하는 과정</li>
<li>노드를 방문하는 순서에 따라 후위, 전위, 중위, 레벨 순회가 있음</li>
<li>이진트리를 기반으로 설명하지만 모든 트리에서 일반화 시킬 수 있음<h3 id="후위순회postorder-traversal">후위순회(Postorder Traversal)</h3>
</li>
<li>자식들 노드를 방문하고 자신의 노드를 방문하는 것<pre><code class="language-C++">수도코드
Postordr(node)
  if(node.visited == false)
      postorder(node-&gt;left)
      postorder(node-&gt;right)
      node.visited = true</code></pre>
<h3 id="전위순회preorder-traversal">전위순회(Preorder Traversal)</h3>
</li>
<li>자신의 노드를 방문하고 다음 노드들을 방문하는 것(DFS를 생각하면 됨)<pre><code class="language-C++">수도코드
Preorder(node)
  if(node.visited == false)
      node.visited = true
      Preorder(node-&gt;left)
      Preorder(node-&gt;rigiht)</code></pre>
<h3 id="중위순회inorder-traversal">중위순회(Inorder Traversal)</h3>
</li>
<li>왼쪽 노드를 먼저 방문한 뒤 자신 노드를 방문하고 오른쪽 노드를 방문하는 것<pre><code class="language-C++">수도코드
Inorder(node)
  if(node.visited == false)
      Inorder(node-&gt;left)
      node.visited = true
      Inorder(node-&gt;right)</code></pre>
<h3 id="레벨순회level-traversal">레벨순회(Level Traversal)</h3>
</li>
<li>BFS를 생각하면 됨<h3 id="예제-문제">예제 문제</h3>
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/e115adbe-ee86-4615-8755-3cc485481816/image.png" /><pre><code>Q. 위의 그래프가 주어졌을 때 preorder, inorder, postorder를 구현하라. 
</code></pre></li>
</ul>
<p>수도코드를 보고 코드를 구축하는 연습을 하셔야 합니다. 아래와 같이 그래프가 주어졌을 때 비어진 함수를 채워서 preorder, inorder, postorder를 구현하고 이 때 방문했을 때 해당 노드를 출력하는 것을 구현해보세요. 
[출처] [알고리즘 강의] 2주차. 그래프이론, 인접행렬, 인접리스트, DFS, BFS, 트리순회|작성자 큰돌</p>
<pre><code>```C++
#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;

vector&lt;int&gt; adj[1004];
bool visited[1004];

void postOrder(int here)
{
    if(visited[here] == true)
        return;
    if(adj[here].size() == 1)
        postOrder(adj[here][0]);
    if(adj[here].size() == 2)
    {
        postOrder(adj[here][0]);
        postOrder(adj[here][1]);
    }
    visited[here] = true;
    cout &lt;&lt; here &lt;&lt; &quot; &quot;;
}
void preOrder(int here)
{
    if(visited[here] == true)
        return;
    visited[here] = true;
    cout &lt;&lt; here &lt;&lt; &quot; &quot;;
    if (adj[here].size() == 1)
        preOrder(adj[here][0]);
    if (adj[here].size() == 2)
    {
        preOrder(adj[here][0]);
        preOrder(adj[here][1]);
    }
}
void inOrder(int here)
{
    if (visited[here] == true)
        return;
    if (adj[here].size() == 1)
    {
        inOrder(adj[here][0]);
        visited[here] = true;
        cout &lt;&lt; here &lt;&lt; &quot; &quot;;
    }
    if (adj[here].size() == 2)
    {
        inOrder(adj[here][0]);
        visited[here] = true;
        cout &lt;&lt; here &lt;&lt; &quot; &quot;;
        inOrder(adj[here][1]);
    }
    else
    {
        visited[here] = true;
        cout &lt;&lt; here &lt;&lt; &quot; &quot;;
    }
}
int main()
{
    adj[1].push_back(2);
    adj[1].push_back(3);
    adj[2].push_back(4);
    adj[2].push_back(5);
    int root = 1;
    cout &lt;&lt; &quot;\n 트리순회 : postOrder \n&quot;;
    postOrder(root);
    memset(visited, false, sizeof(visited));
    cout &lt;&lt; &quot;\n 트리순회 : preOrder \n&quot;;
    preOrder(root);
    memset(visited, false, sizeof(visited));
    cout &lt;&lt; &quot;\n 트리순회 : inOrder \n&quot;;
    inOrder(root);
    return 0;
}</code></pre><h3 id="정리">정리</h3>
<p><img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/10a59409-c089-4488-a7ff-0e14c7f8dba3/image.png" /></p>