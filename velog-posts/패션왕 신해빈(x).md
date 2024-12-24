<p><a href="https://www.acmicpc.net/problem/9375">https://www.acmicpc.net/problem/9375</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;map&gt;
#include &lt;string&gt;

using namespace std;

int t, n;
string a, b;

int main()
{
    cin &gt;&gt; t;
    while (t--)
    {
        map&lt;string, int&gt; m;
        cin &gt;&gt; n;
        for (int i = 0; i &lt; n; i++)
        {
            cin &gt;&gt; a &gt;&gt; b;
            m[b]++;
        }
        long long ret = 1;
        for (auto a : m)
        {
            ret *= ((long long)a.second + 1);
        }
        ret--;
        cout &lt;&lt; ret &lt;&lt; endl;
    }
}</code></pre>
<ul>
<li>경우의 수는 곱하기인 점을 생각하면 쉽게 풀린다</li>
<li>모든 경우 * data의 갯수</li>
<li>이를 가지고 첫번째 케이스에 적용시켜 보면 headgear가 2개 eyewear가 1개로 중복된 의상의 종류는 같이 입지 못하므로 dat가 2개가 된다</li>
<li>경우의 수는 모두 안 입는 경우, 둘중 하나만 입는 경우, 둘 다 입는 경우로 총 3가지 이다</li>
<li>따라서 모든 경우 * data의 갯수는 3 * 2 = 6 이 나오는대 이때 모두 입지 않는 경우는 존재하지 않는다 했으므로 결과 값에서 빼줘야 하므로 5가지 케이스가 나온다</li>
<li>이를 적용해 코드를 짜보자</li>
<li>중복된 데이터를 저장하지 못하게 하기 위해 map을 사용해 옷의 종류를 key 값으로 그 종류의 옷을 value로 사용해 줄 것이다</li>
<li>그 후 map 변수를 for each문을 통해 현재 옷 종류에 저장된 옷의 갯수에 1을 더한 뒤 그 값을 서로 곱해주면 모든 경우 * data의 갯수가 될 것이다<ul>
<li>이때 +1을 해주는 이유는 그 옷의 종류를 안입는 경우를 포함해서 계산하기 위해서이다</li>
<li>즉 모든 옷을 안 입는 경우와 어느 하나만 입거나 하는 경우도 포함하기 위함이다</li>
</ul>
</li>
<li>그 후 모든 옷을 입지 않는 경우를 빼기위해 결과 값에 -1을 하면 원하는 결과를 얻을 수 있다</li>
</ul>