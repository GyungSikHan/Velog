<h2 id="c-ampaccelerated-massive-parallelism">C++ AMP(Accelerated Massive Parallelism)</h2>
<hr />
<h3 id="정의">정의</h3>
<p>C++ 프로그래밍 언어를 확장하여 GPU와 같은 테이터 병렬 하드웨어를 활용해 코드 실행을 가속화 하는 기술</p>
<p>(Visial Studio 2022 버전 17.0부터 더 이상 사용되지 않아 AMP 헤더를 포함하면 빌드 오류가 생김</p>
<p> 경고를 무음으로 표시하기 위해 헤더를 포함하기 전에 정의_SILENCE_AMP_DEPRECATION_WARNINGS 해야함)</p>
<h3 id="특징">특징</h3>
<ol>
<li>병렬 처리 최적화 : C++ AMP은 GPU의 병렬 청리 능력을 활용하여 대규모 데이터 처리 작업을 가속화함</li>
<li>프로그래밍 모델 : 다차원 배열, 인덱싱, 메모리 전송, 타일링 등을 지원하는 프로그래밍 모델을 제공</li>
<li>수학 함수 라이브러리 : 병렬 처리에 최적화된 수학 함수 라이브러리 포함</li>
<li>C++ 언어 확장 : 기존 C++ 언러을 확장하여 GPU 프로그래밍을 위한 새로운 키워드와 기능 추가</li>
</ol>
<h3 id="목적과-장점">목적과 장점</h3>
<ol>
<li>개발 생산성 확장 : Visial Studio와 완벽하게 통합되어, 개발자들이 익숙한 환경에서 GPU 프로그래밍 가능</li>
<li>이식성 : 다양한 하드웨어에서 실행 가능한 코드를 작성할 수 있도록 설계</li>
<li>접근성 : CUDA나 OPenCL과 같은 복잡한 GPGPU 프로그래밍 기술에 비해 진입 장벽이 낮음</li>
<li>성능 최적화 : GPU의 병렬 처리 능력을 활용하여 애플리케이션 성능을 크게 향상</li>
</ol>