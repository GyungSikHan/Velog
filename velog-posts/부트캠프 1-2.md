<h2 id="블루프린트란">블루프린트란?</h2>
<hr />
<ul>
<li>언리얼 엔진에서 제공하는 비주얼 스크립팅 시스템</li>
<li>복잡한 코드 작성 없이 노드 기반으로 그림을 그려 프로그래밍을 가능하게 하는 시스템</li>
<li>협업에서 중요한 프로젝트의 프로토타입이나 간단한 로직을 이용해 게임을 제작하기도 함</li>
</ul>
<h2 id="문자열-출력">문자열 출력</h2>
<hr />
<ul>
<li>문자열 출력 함수 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/d5317d6f-460a-4a11-9da8-b37923d34c35/image.png" />
  - 블프에선 문자열을 출력할 때 크게 Prent Text, Prent String 두 함수를 사용한다
  - Text VS String
      - Text
          - 주로 사용자에게 보여지는 내용이나 문서의 본문에 사용
          - 프로그래밍의 특정 데이터 타입이 아닌 일반적인 텍스트 데이터를 의미
          - 여러줄의 문자열이나 서식이 있는 텍스트 포함 가능
          - 주로 문서나 UI등에서 자주 사용
      - String
          - 연속된 문자의 배열로 취급하며 각 문자에 Index로 접근 가능
          - 프로그래밍의 특정 데이터 타입으로 문자열 관련 연산이 가능
          - 프로그래밍에서 문자열 데이터를 다룰 대 사용</li>
<li>문자 출력<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a62c35ce-c8e7-4037-9efb-7879681a9ecf/image.png" />
- 우리는 문자를 띄어 확인만 할 것이므로 Print Text 함수를 사용했다
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/84d90f29-69f7-4671-a2f2-46e95031b8a4/image.png" />

</li>
</ul>
<blockquote>
<p>💡
Event : 일종의 트리거로 어떤 상황에서 호출될 것이라 약속하는 의미</p>
<ul>
<li>BeginPlay : 게임 시작시에 한번만 호출되는 이벤트</li>
<li>Tick : 매 프레임 계속해서 호출되는 이벤트</li>
</ul>
</blockquote>
<h2 id="변수">변수</h2>
<hr />
<ul>
<li>변수란?<ul>
<li>데이터를 저장하고 관리하는 컨테이너</li>
<li>게임 내에서 값을 저장하거나, 오브젝트와 상호작용을 추적, 로직의 조건을 결정하는데 사용</li>
</ul>
</li>
<li>변수 추가<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/de7a4399-5b9c-466a-8a6c-300d4e7f421c/image.png" />
- 변수 종류
      <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/08358cc8-71c7-4336-b1bc-234d7370323a/image.png" />


</li>
</ul>
<h2 id="변수-get-set">변수 Get, Set</h2>
<hr />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/c68b8313-aa47-43a9-9079-29f601b7b15e/image.png" />
- Set
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7f55e96e-1e27-42de-90f9-7449c5b962ed/image.png" />
    - Set은 프로그래밍 언어에서 변수에 값을 저장해주는 것을 의미한다
- Get
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1d0a42bc-f18c-4ced-9bfc-7a884a981779/image.png" />    
    - Get은 프로그래밍 언어에서 변수를 가져와 사용하는 것을 의미한다

<h2 id="사칙연산">사칙연산</h2>
<hr />
<ul>
<li>사직연산 스크립팅<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9e7b7b47-0f9f-4ccc-8730-d84b61724ad9/image.png" />


</li>
</ul>
<pre><code>- 위의 스크립팅을 이용하여 변수들의 사칙 연산을 할 수 있다</code></pre><h2 id="비교-연산자">비교 연산자</h2>
<hr />
<ul>
<li>비교 연산자<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/4ccdc02a-8ce3-4665-8c95-1a8947b63283/image.png" />


</li>
</ul>
<pre><code>- 위의 스크립팅을 이용하여 변수들을 비교해 조건에 참 거짓을 반환 받을 수 있다</code></pre><h2 id="논리-연산자">논리 연산자</h2>
<hr />
<ul>
<li><p>논리 연산자</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/20eb36e7-7bc5-412f-8f8a-cd63e0e8b557/image.png" />


</li>
</ul>
<pre><code>- 여러 조건을 조합하거나 반전하여 복잡한 논리적 흐름을 처리할 때 사용</code></pre><h2 id="블루프린트-흐름-제어">블루프린트 흐름 제어</h2>
<hr />
<ul>
<li><p>Branch</p>
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/daa2b886-b537-4009-847a-ea5825502346/image.png" />


</li>
</ul>
<pre><code>- 조건에 따라 참 거짓으로 나누는 노드
- 프로그래밍 언어의 if-else와 유사
- 조건은 반드시 Bool 타입이여야 한다</code></pre><ul>
<li><p>Sequence</p>
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/564abdcb-d2ff-4323-afe8-510d596eb742/image.png" />


</li>
</ul>
<pre><code>- 실행 흐름을 여러 개의 출력으로 분리하고 순차적으로 각 출력 핀을 실행하는 노드
- 노드의 양이 많아지는 경우 사용할 수 있다
- 프로그래밍 언어에서는 존재하지 않음(?)</code></pre><ul>
<li><p>Flip Flop</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cf18fe65-bdb7-4049-97aa-a8bf080db2dd/image.png" />


</li>
</ul>
<pre><code>- 실행 흐름을 번갈아가며 두 개의 출력 핀으로 구분하여 실행
- 하나의 실행 핀으로 입력받고 두개의 실행 핀이 번갈아가며 실행됨
- 반복적으로 번갈아 실행되는 동작을 간단히 구현할 수 있고 상태 전환을 쉽게 관리할 수 있다
- 예를 들어 롤의 징크스 Q처럼 누를 때 마다 무기가 바뀌거나 하는 식으로 사용할 수 있을 것 같다</code></pre><h2 id="반복문">반복문</h2>
<hr />
<ul>
<li><p>특정 행동을 반복하도록 시키기 위한 문법</p>
</li>
<li><p>While Loop, For Loop를 사용해 볼 것이다</p>
</li>
<li><p>While Loop</p>
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/cc2cc2e5-784e-4c58-88d7-7b1deae861e1/image.png" />

<ul>
<li>While Loop는 프로그래밍 언어의 while 문과 같다</li>
<li>특정 조건이 참인 동안 Loop Body에 연결된 노드들이 반복해서 실행된다</li>
<li>조건이 거짓일 경우 Completed에 연결된 노드가 실행되며 반복문이 끝이 난다</li>
</ul>
</li>
<li><p>For Loop</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/a5576c41-ef17-4e68-97b4-376cd32ed5d3/image.png" />

<ul>
<li>For Loop는 프로그래밍 언어의 for문과 같다</li>
<li>특정 범위 동안 Loop Body에 연결 된 노드를 반복해서 실행된다</li>
<li>index는 현재 index의 값을 의미한다</li>
<li>조건을 만족하지 않다면 Completed에 연결된 노드가 실행되며 반복문이 종료된다</li>
</ul>
</li>
</ul>
<h2 id="열거형">열거형</h2>
<hr />
<ul>
<li><p>열겨형(Enum)</p>
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/7ec30e38-4de1-4bfa-9385-9d6f60ec2050/image.png" />
<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/db5c26ce-0362-4376-9ac7-e36f2fffc35e/image.png" />
  - 관련 있는 상수들을 한데 묶어 사용하는 방법
  - 묶여있는 데이터들은 0부터 상수형으로 사용 가능하며 꼭 0이 아니더라고 지정한 숫자로 사용 가능하다
  - 프로그래밍 언어의 Enum과 같다
 <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/60a14a07-a2a4-40ff-ac7d-7d51405cc8b9/image.png" />
  - Switch On 노드를 사용하여 해당하는 값마다 원하는 로직을 설정 가능하다

</li>
</ul>
<h2 id="숙제">숙제</h2>
<hr />
<ol>
<li>수업 시간에 만든 총 게임 버그수정<ol>
<li>총알이 다 떨어지면 못쏘게 하기</li>
<li>총알이 가득 차 있을 때 총알 재장전 못하게 하기</li>
</ol>
</li>
<li>텍스트 기능 추가<ol>
<li>총알 피격하면 HP 깍이게 만들기</li>
<li>체력 회복 기능</li>
</ol>
</li>
</ol>
<ul>
<li><p>완성</p>
  <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/995afe67-d4ea-481e-9bca-0098eba9cae8/image.png" />


</li>
</ul>
<pre><code>- 마우스 입력시 총알이 나가며 총알이 없다면 총알이 없다는 문구가 띄어진다
- 총알이 나갔을 때 HP를 Damage만큼 빼주면서 현재 HP 값을 출력한다
- 이때 HP가 0이하면 총을 더이상 쏘지 못하고 3초뒤에 게임이 종료될 수 있도록 하였다</code></pre>   <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/95065729-8d3b-4978-a33c-5a950e160a70/image.png" />


<pre><code>- R을 눌렀을 때 총알이 장전되며 총알이 가득 차 있다면 장전이 안되게 하였다</code></pre>   <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/97b523e7-f906-45b6-b467-331bc963a7f2/image.png" />


<pre><code>- HP가 가득 차있거나 0이 아닐 경우 H 버튼을 누르면 HP가 회복된다</code></pre><ol>
<li>While Loop를 이용한 구구단<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/1a329009-8dbf-4114-aff7-a271745691b1/image.png" />



</li>
</ol>
<ol>
<li>컴퓨터와 가위바위보<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/999b5931-383c-4b43-b5cd-78783b439e53/image.png" />


</li>
</ol>
<pre><code>1. Z,X,C를 입력하면 플레이어 Enum 변수에 바위, 가위, 보를 Set한뒤 Fuc 함수를 실행시키고 Result 함수를 실행하게 만들었다

   &lt;img src = &quot;https://velog.velcdn.com/images/gksrudtlr2/post/76d7d6fe-5d04-4f99-83d7-f3a975bf3bc0/image.png&quot; align = &quot;left&quot;&gt;


2. Fuc 함수는 0~2중 Random수를 입력받아 Swich On 노드를 이용하여 컴퓨터의 가위바위보 정보를 저장할 Enum 변수에 결과를 Set한다

   &lt;img src = &quot;https://velog.velcdn.com/images/gksrudtlr2/post/41700f8d-71c2-4952-9d14-2bf7a45740bb/image.png&quot; align = &quot;left&quot;&gt;


3. 플레이어의 Enum과 Computer의 Enum을 비교하여 두 값이 같다면 결과를 도출할 Enum 변수에 비김을 Set한다
 &lt;img src = &quot;https://velog.velcdn.com/images/gksrudtlr2/post/e15cec08-f72f-430d-ab33-1f5ce8921edb/image.png&quot; align = &quot;left&quot;&gt;


4. Branch가 False 라면 플레이어의 Enum에 따라 Switch On노드를 통해 Computer의 Enum과 비교해 누가 이겼는지를 결과 Enum 변수에 Set해준다
  &lt;img src = &quot;https://velog.velcdn.com/images/gksrudtlr2/post/5df7cb24-3936-4ef6-b5a9-303c172c4aa1/image.png&quot; align = &quot;left&quot;&gt;


5. Fun 함수가 끝이나면 Result 함수를 통해 플레이어와 Computer의 Enum 값을 출력하고 결과 Enum에 따라 승부 결과를 출력해 주었다</code></pre><ul>
<li>부가적 기능들<img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/9ae6c296-b2c2-41d9-a835-99addf49519b/image.png" />


</li>
</ul>
<pre><code>- Begin Play에서 총 게임과 가위바위보 게임의 입력을 못하게 막고 게임 선택 문구를 출력해준다
- 1,2,3번으로 게임을 선택하며 각각의 게임에 막아 놓은 입력을 풀어 게임 시작시 입력이 가능하게 해준다
- 4번은 게임을 종료하는 함수를 호출해준다</code></pre>   <img align="left" src="https://velog.velcdn.com/images/gksrudtlr2/post/6e79b3f2-48fb-471e-abff-13cc4c843325/image.png" />


<pre><code>- EndGame 함수는 QuitGame을 호출해주는 함수로 게임을 종료 시켜주는 함수이다</code></pre>