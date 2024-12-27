<h2 id="이진트리">이진트리</h2>
<h3 id="정의">정의</h3>
<ul>
<li>긱 노드의 자식노드 수가 2개 이하로 구성되어있는 트리
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/7478b2bb-b762-416f-a382-2e89d2f2931f/image.png" /><h3 id="종류">종류</h3>
<h4 id="정이진-트리full-binary-tree">정이진 트리(full binary tree)</h4>
</li>
<li>자식 노드가 0 또는 2개인 이진 트리를 의미합니다. </li>
</ul>
<h4 id="완전-이진-트리complete-binary-tree">완전 이진 트리(complete binary tree)</h4>
<ul>
<li>왼쪽에서부터 채워져 있는 이진 트리를 의미합니다. 마지막 레벨을 제외하고는 모든 레벨이 완전히 채워져 있으며 마지막 레벨의 경우 왼쪽부터 채워져 있습니다.</li>
</ul>
<h4 id="변질-이진-트리degenerate-binary-tree">변질 이진 트리(degenerate binary tree):</h4>
<ul>
<li>리프노드 제외, 자식 노드가 하나밖에 없는 이진 트리를 의미합니다. </li>
</ul>
<h4 id="포화-이진-트리perfect-binary-tree">포화 이진 트리(perfect binary tree)</h4>
<ul>
<li>모든 노드가 꽉 차 있는 이진 트리를 의미합니다.<h4 id="균형-이진-트리balanced-binary-tree">균형 이진 트리(balanced binary tree)</h4>
</li>
<li>트리의 모든 노드에 대해 왼쪽 하위 트리와 오른쪽 하위 트리의 높이 차이가 1 이하인 이진 트리</li>
<li>트리의 어느 한쪽이 지나치게 치우치지 않도록 구조가 유지됨</li>
<li>이러한 균형 덕분에, 탐색, 삽입, 삭제 등의 연산에서 시간 복잡도가 O(log n)으로 보장될 수 있습니다.</li>
<li>높이차이는 각 하위 트리의 전체 높이를 기준으로 계산 </li>
<li>레드-블랙 트리(Red-Black Tree)<ul>
<li>균형 이진 트리의 한 예로, 자가 균형을 유지하기 위한 특정한 규칙들을 갖춘 이진 탐색 트리</li>
<li>이 규칙들 덕분에 최악의 경우에도 효율적인 연산을 보장하며, C++의 std::map과 std::set 같은 데이터 구조의 내부 구현에 사용</li>
</ul>
</li>
</ul>