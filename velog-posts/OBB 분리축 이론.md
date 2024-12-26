<h2 id="obb-vs-aabb">OBB VS AABB</h2>
<p>OBB와 AABB는 둘 다 객체의 경계를 단순화하여 충돌 감지에 사용되는 대표적 Bounding Volume
각각의 측성과 분리축 이론 적용 방식이 다름</p>
<h3 id="aabbaxis-aligned-bounding-box">AABB(Axis-Aligned Bounding Box)</h3>
<h4 id="정의">정의</h4>
<ul>
<li>좌표축에 정렬된 직육면체로, 각 면이 X, Y, Z 축과 평행</li>
<li>각 차원에서 최소점(min)과 최대점(max)로 정의됨<h4 id="주요-특징">주요 특징</h4>
</li>
</ul>
<ol>
<li>간단한 구조 : 회전이 없기 때문에 계산이 단순</li>
<li>효율성 : 충돌 감지 시 계산량이 적음</li>
<li>정확도 낮음 : 객체가 회전할 경우 경계가 비효율적으로 커질 수 있음<h3 id="obboriented-bounding-box">OBB(Oriented Bounding Box)</h3>
<h4 id="정의-1">정의</h4>
</li>
</ol>
<ul>
<li>임의의 방향으로 회전할 수 있는 직육면체</li>
<li>중심점, 세 축 방향(단위 벡터), 각 축의 반직경(helf-extents)로 정의<h4 id="주요-특징-1">주요 특징</h4>
</li>
</ul>
<ol>
<li>유연성 : 객체의 회전에 따라 경계가 더 정확하게 맞춰짐</li>
<li>복잡성 : 계산량이 많아 충돌 감지가 더 복잡함</li>
<li>정확도 높음 : 객체의 실제 형상과 더 가깝게 경계를 정의할 수 있음</li>
</ol>
<hr />
<h2 id="분리축-이론sat-separating-axis-theorem">분리축 이론(SAT, Separating Axis Theorem)</h2>
<h3 id="aabb에서-sat">AABB에서 SAT</h3>
<ul>
<li>분리축 개수 : 좌표축에 정렬되어 있으므로 X, Y, Z축만 분리축으로 고려하면 됨</li>
<li>충돌 검사 방법<ol>
<li>두 AABB의 각 축에 대해 최소-최대 범위가 겹치지 않으면 충돌하지 않음</li>
<li>한 축에서라도 두 범위가 겹치지 않으면 충돌하지 않음</li>
<li>모든 축에서 범위가 겹치면 충돌</li>
</ol>
</li>
<li>효율성 : 분리축이 3개 뿐이므로, OBB에 비해 계산량이 적음<h3 id="obb에서-sat">OBB에서 SAT</h3>
</li>
<li>분리축 계수 : 분리축이 많아짐<ol>
<li>OBB1의 3개 축</li>
<li>OBB2의 3개 축</li>
<li>두 OBB의 각 축 쌍에서 파생된 9개의 교차 축 -&gt; 총 15개 분리 축</li>
</ol>
</li>
<li>충돌 검사 방법<ol>
<li>각 축에 대해 두 OBB의 투명 범위를 계산</li>
<li>모든 축에서 투영이 겹쳐야 충돌로 판정</li>
<li>하나라도 겹치지 않으면 충돌하지 않음</li>
</ol>
</li>
<li>정확도 : 더 많은 축에서 비교하므로 충돌 감지가 더 정밀하게 이뤄짐</li>
</ul>
<hr />
<h2 id="사용-사례">사용 사례</h2>
<ul>
<li>AABB는 단순 물리 엔진, LOD(Level of Detail) 시스템, 초기 충돌 테스트에서 주로 사용</li>
<li>OBB는 더 높은 정밀도가 필요한 경우, 특히 게임의 정밀한 물리 계산, CAD, 시뮬레이션 등에서 사용</li>
</ul>
<hr />
<h2 id="결론">결론</h2>
<ul>
<li>AABB는 연산이 빠르지만, 정확도가 떨어진다</li>
<li>OBB는 정확도가 높지만 많은 연산을 요구한다</li>
<li>환경에 따라 두 기법을 조합하여 AAB로 간단히 충돌 감지를 수행한 후 필요할 때 OBB로 정밀 검사를 수행하는 다단계 충돌 감지 방식 사용함</li>
</ul>