<p><a href="https://www.acmicpc.net/problem/2910">https://www.acmicpc.net/problem/2910</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;map&gt;
#include &lt;vector&gt;
#include &lt;algorithm&gt;
using namespace std;

int n, c, temp;
map&lt;int, int&gt; m, m2;
vector&lt;pair&lt;int, int&gt;&gt; v;

bool com(pair&lt;int, int&gt; a, pair&lt;int, int&gt; b)
{
    if (a.first == b.first)
        return m2[a.second] &lt; m2[b.second];
    return a.first &gt; b.first;
}

int main()
{
    cin &gt;&gt; n &gt;&gt; c;

    for (int i = 0; i &lt; n; i++)
    {
        cin &gt;&gt; temp;
        m[temp]++;
        if (m2[temp] == 0)
            m2[temp] = i + 1;
    }
    for (pair&lt;int, int&gt; iter : m)
        v.push_back({ iter.second,iter.first });

    sort(v.begin(), v.end(), com);

    for (pair&lt;int, int&gt; iter : v)
        for (int i = 0; i &lt; iter.first; i++)
            cout &lt;&lt; iter.second &lt;&lt; &quot; &quot;;
}</code></pre>
<ul>
<li>정렬을 하는 문제였지만 map과 sort에 대해 아직 이해도가 부족해 문제를 풀지 못했다</li>
<li>일단 map은 sort로 정렬을 하기 위해 map안에있는 값을 vector에 저장해준 뒤 vector로 sort를 해주면 정렬이 된다</li>
<li>또한 sort에서 compare함수를 만들어 오름차순이나 내림차순으로 바꿀 수 있어 이를 이용해 풀면 되는 문제였다</li>
<li>문제를 풀때 temp에 값을 입력해 map에 저장하는데 temp를 키 값으로 같은 키값이 들어왔다면 몇번 들어왔는지 새주기 위해 +1을 누적할 것이다</li>
<li>하지만 문제에서 입력된 횟수가 많은 숫자를 먼저 출력하고 횟수가 같을 경우 먼저 입력받은 순으로 출력을 해야하기 때문에 map 변수를 하나 더 만들어 두번째 map 변수에서도 tmep를 key 값으로 value가 0일때 i+1을 해서 몇번째 입력했을 때 key 값이 들어왔는지 저장해준다</li>
<li>처음 map 변수를 정렬하기 위해 vector로 옮겨줄 것인데 우리는 map의 value를 첫번째로 저장하고 두번째로는 key를 저장할 것이다(value값이 큰 순서대로 정렬을 하기 위해)</li>
<li>이제 sort로 정렬을 하기 전 내림차순으로 정렬을 하기 위해 compare라는 함수를 만들어 함수에 넘겨줄 값은 pair로 vectir안에 저장된 값들을 비교하게 만들것이다</li>
<li>이 함수에선 첫번째 인자의 first와 두번째 인자의 first가 같다면, 즉 두 변수의 입력 횟수가 같다면 들어온 순서를 판단하여 먼저 들어온 것이 더 앞으로 갈 수 있게 하고 두 값이 같지 않다면 first값이 더 큰 값이 true로 리턴하여 가장 많이 입력된 값부터 입력된 횟수가 같다면 먼저 들어온 값으로 정렬을 해주면 되는 문제이다</li>
</ul>