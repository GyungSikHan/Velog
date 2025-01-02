<h3 id="dfs-bfs-비교">DFS, BFS 비교</h3>
<ul>
<li>공통점<ul>
<li>둘 다 시간복잡도와 공간복잡도는 인접 리스트로 이루어졌다면 O(V+E)이고 인접 행렬의 경우 O($V^2$)로 동일하다</li>
</ul>
</li>
<li>차이점</li>
</ul>
<table>
<thead>
<tr>
<th>이름</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>DFS</td>
<td>메모리를 덜 씀, 절단점 등 구할 수 있음, 코드가 더 짧으며 완탐의 경우 많이 사용, 시작 노드와 연결된 한 노드가 갈 수 있는 끝까지 간 후 돌아와 다음 노드를 탐색</td>
</tr>
<tr>
<td>BFS</td>
<td>메모리를 더 씀, 가중치가 같은 그래프내에 최단거리 구할 수 있음, 코드가 더 김, 시작 노드부터 같은 레벨에 있는 노드들을 탐색하여 마지막 레벨까지 탐색</td>
</tr>
<tr>
<td>- Tip</td>
<td></td>
</tr>
<tr>
<td>- <span style="color: yellow;">&quot;퍼져나간다&quot;, &quot;탐색한다&quot;라는 글자가 있으면 반드시 DFS, BFS를 생각해야한다!!!!</span></td>
<td></td>
</tr>
</tbody></table>