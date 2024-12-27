<h2 id="이진-탐색트리">이진 탐색트리</h2>
<p><img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/62e2be80-575e-46e1-b357-cf76f10815e7/image.png" /></p>
<h3 id="정의">정의</h3>
<ul>
<li>이진트리의 일종으로 노드의 오른쪽 하위트리는 노드의 값보다 큰 값, 왼쪽 하위트리는 노드의 작은 값만 들어있는 트리</li>
<li>검색을 하기 용이하며, 이 특성을 이용하면 전체 탐색을 하지 않아도 됨<h3 id="시간-복잡도">시간 복잡도</h3>
<h4 id="평균">평균</h4>
</li>
<li>탐색, 삽입, 삭제 모두 O(logN)
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/45da7f32-09d4-4d68-81e7-f34a22e3f727/image.png" /><h4 id="최악">최악</h4>
</li>
<li>하지만 삽입 순서에 따라 달라짐</li>
<li>트리가 완성되었을 때 위의 그림처럼 선형적으로 나오게되면 O(N)이 나옴<h3 id="종류">종류</h3>
삽입 순서에 영향을 받기 때문에 삽입 순서가 어떻게 되든 회전을 통해 균형잡힌 이진트리로 만드는 트리가 존재함</li>
<li>AVL 트리</li>
<li>레드블랙 트리 : map, set의 내부 구현</li>
</ul>