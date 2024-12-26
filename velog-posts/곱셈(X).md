<p><a href="https://www.acmicpc.net/problem/1629">https://www.acmicpc.net/problem/1629</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;cmath&gt;

using namespace std;

long long a, b, c;
long long solve;

long long Solve(long long data, long long data2)
{
    if (data2 == 1)
        return data % c;
    long long temp = Solve(data, data2 / 2);
    temp = (temp * temp) % c;
    if (data2 % 2 == 1)
        temp = (temp * data) % c;
    return temp;
}

int main()
{
    cin &gt;&gt; a &gt;&gt; b &gt;&gt; c;
    cout &lt;&lt; Solve(a, b) &lt;&lt; endl;
}</code></pre>
<ul>
<li>제곱근을 pow나 for문을 이용해 풀면 숫자가 커질수록 시간이 오래걸려 시간 제한에 걸릴것이다</li>
<li>그래서 미리 계산된 값을 저장해 이용할 것이다</li>
<li>$2^8$을 예를 들어 보면 $2^8 = 2^4 * 2^4$이고 $2^4 = 2^2 * 2^2$ 이를 이용할 것이다</li>
<li>또한 분배법칙을 이용해 (a + b) % c = a % c + b % c 이고 $(a * b)$ % c = a % $c * b$ % c 를 이용하면 더 쉽게 풀 수 있다</li>
<li>따라서 Solve라는 함수를 재귀함수로 이용하여 data2가 1일 때 까지 안으로 들어갈 것이다</li>
<li>data2 == 1일 때 data % c 를 리턴하여 $a^1$ % c 값을 반환해 주는 것이다</li>
<li>이를 위해 temp라는 변수에 Solve(data, data2/2)를 한 값을 저장해 줄 것이다</li>
<li>이렇게 나온 temp를 이용해 예시에서 보여준 것처럼 (temp * temp) % c를 계산하여준다</li>
<li>이때 data2가 홀수일 경우가 있으므로 data2 % 2 == 1일때 temp에 (temp * data) % c를 하여 홀수번 제곱근을 할 경우도 생각해줘야한다</li>
<li>이를 통해 재귀함수를 모두 탈출하면 시간도 절약하면서 원하는 값을 얻을 수 있다</li>
</ul>