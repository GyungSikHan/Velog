<h2 id="과제-링크">과제 링크</h2>
<p><a href="https://github.com/GyungSikHan/BootCampHomeWork.git">https://github.com/GyungSikHan/BootCampHomeWork.git</a></p>
<h2 id="과제-1번">과제 1번</h2>
<hr />
<h3 id="필수기능">필수기능</h3>
<ul>
<li>사용자로부터 5개의 숫자를 입력 받아 배열에 저장하고 이들의 합계와 평균을 계산해서 출력해주세요!</li>
<li>5개의 숫자를 입력 받는 공간은 배열을 활용할게요!</li>
<li>합과 평균을 구하는 동작은 main함수에 한번에 작성하지 말고 각각 함수를 구현해주시는 것으로 해요!<ul>
<li>왜 이렇게 하는 것이 좋은지를 한 번 더 생각해보면서 작성해봐요!<h3 id="도전기능">도전기능</h3>
</li>
</ul>
</li>
<li>정렬은 오름차순 정렬과 내림차순 정렬이 가능해야 합니다.</li>
<li>숫자 1을 입력 받으면 오름차순 정렬, 숫자 2를 입력 받으면 내림차순 정렬을 하도록 구현해주세요.<ul>
<li>입력을 구현하는 방법은 원격강의에서 배울겁니다!</li>
</ul>
</li>
<li><code>algorithm</code> 헤더의 <code>sort</code> 함수를 사용하지 않고 직접 구현해보세요.</li>
<li>오름차순 정렬과 내림차순 정렬 동작을 각각 함수로 구현해봐요!</li>
</ul>
<p>정렬 알고리즘에 대한 이해가 있어야 도전 기능을 마무리 할 수 있는데요! 구글에 <strong>정렬 알고리즘</strong>을 검색해서 쉬운 정렬 알고리즘에 대해서 공부해보고 적용하면 여러분들에게도 큰 의미가 있을겁니다!</p>
<h2 id="과제-2번">과제 2번</h2>
<hr />
<h3 id="필수기능-1">필수기능</h3>
<ul>
<li><p>Animal이라는 기본 클래스를 정의 합니다.</p>
<ul>
<li>Animal 클래스에는 <code>makeSound()</code>라는 순수 가상 함수를 포함합니다.</li>
</ul>
</li>
<li><p>Animal 클래스를 상속받아 다양한 동물 클래스를 생성합니다.</p>
<ul>
<li>예) Dog, Cat, Cow<ul>
<li>각 동물 클래스에서 makeSound()함수를 재정의하여 해당 동물의 소리를 출력하면 됩니다!</li>
</ul>
</li>
</ul>
</li>
<li><p>메인 함수에서 Animal 타입의 포인터 배열을 선언하고 Dog, Cat, Cow를 각각 배열의 원소로 선언합니다. → 이후 Animal 배열을 반복문으로 순회하면서 각 동물의 울음소리를 내게 합니다!</p>
</li>
<li><p>전체적인 구조는 아래와 같습니다.<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/843f0c0c-7238-4ffb-8588-3c1c3a8e2b8e/image.png" /></p>
<h3 id="도전기능-1">도전기능</h3>
</li>
<li><p>필수 기능 가이드에 있는 요구사항을 만족하는 코드를 구현했다면 아래 코드 스니펫을 보고 요구사항대로 <code>Zoo</code> 클래스를 정의해주세요!</p>
<ul>
<li><p><strong>[코드스니펫] Zoo 클래스 요구사항</strong></p>
<pre><code class="language-cpp">  class Zoo {
  private:
      Animal* animals[10]; // 동물 객체를 저장하는 포인터 배열
  public:
      // 동물을 동물원에 추가하는 함수
      // - Animal 객체의 포인터를 받아 포인터 배열에 저장합니다.
      // - 같은 동물이라도 여러 번 추가될 수 있습니다.
      // - 입력 매개변수: Animal* (추가할 동물 객체)
      // - 반환값: 없음
      void addAnimal(Animal* animal);

      // 동물원에 있는 모든 동물의 행동을 수행하는 함수
      // - 모든 동물 객체에 대해 순차적으로 소리를 내고 움직이는 동작을 실행합니다.
      // - 입력 매개변수: 없음
      // - 반환값: 없음
      void performActions();

      // Zoo 소멸자
      // - Zoo 객체가 소멸될 때, 동물 벡터에 저장된 모든 동물 객체의 메모리를 해제합니다.
      // - 메모리 누수를 방지하기 위해 동적 할당된 Animal 객체를 `delete` 합니다.
      // - 입력 매개변수: 없음
      // - 반환값: 없음
      ~Zoo();
  };
</code></pre>
</li>
</ul>
</li>
<li><p>랜덤으로 동물 객체를 반환하는 <code>createRandomAnimal()</code>함수를 구현하세요  자세한 사항은 아래 코드 스니펫을 참조하시면 됩니다!</p>
<ul>
<li><p><strong>[코드스니펫] createRandomAnimal() 함수 요구사항</strong></p>
<pre><code class="language-cpp">  #include &lt;cstdlib&gt;
  #include &lt;ctime&gt;

  // 랜덤 동물을 생성하는 함수
  // - 0, 1, 2 중 하나의 난수를 생성하여 각각 Dog, Cat, Cow 객체 중 하나를 동적으로 생성합니다.
  // - 생성된 객체는 Animal 타입의 포인터로 반환됩니다.
  // - 입력 매개변수: 없음
  // - 반환값: Animal* (생성된 동물 객체의 포인터)
  Animal* createRandomAnimal();
</code></pre>
</li>
</ul>
</li>
<li><p>전체적인 구조는 아래와 같습니다.
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/af99e0c6-fe98-4bf8-b642-6a9a11dd1160/image.png" /></p>
</li>
</ul>
<h2 id="소감-및-과제-해설">소감 및 과제 해설</h2>
<hr />
<h3 id="해설">해설</h3>
<p>1번 필수  과제는 C++ 기초적인 문법을 사용하여 배열만들고 함수로 합계와 평균을 구하는 쉬운 문제였다
도전 과제는 알고리즘을 구현하는 문제로 오름차순 내림차순으로 정렬을 하는 알고리즘을 구하는 것으로 나는 퀵소트로 구현했다
2번 필수 과제와 도전 과제는 둘다 한번에 구현할 수 있는 문제로 class를 만들어 기능을 구현하는 문제였다</p>
<h3 id="소감">소감</h3>
<p>문제를 풀면서 1번의 도전 과제는 오랜만에 퀵소트를 구현하려니 잘 기억이 나질않아 구글링을 통해 다시한번 개념을 정리할 수 있는 기회가 됐던것 같다
다른 문제들은 비교적 쉽게 풀었다</p>