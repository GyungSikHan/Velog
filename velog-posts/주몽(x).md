<p><a href="https://www.acmicpc.net/problem/1940">https://www.acmicpc.net/problem/1940</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;vector&gt;

using namespace std;

int n, m;
vector&lt;int&gt; v;
int sum{};
int main()
{
    cin &gt;&gt; n;
    cin &gt;&gt; m;
    v.resize(n, 0);
    for (int i = 0; i &lt; n; i++)
        cin &gt;&gt; v[i];

    for (int i = 0; i &lt; n; i++)
    {
        for (int j = i+1; j &lt; n; j++)
        {
            if (v[i] + v[j] == m)
                sum++;
        }
    }
    cout &lt;&lt; sum &lt;&lt; endl;
}</code></pre>
<ul>
<li>문제를 완전 잘못읽어 틀렸고 고생했다...</li>
<li>문제를 더욱더 꼼꼼히 읽어야겠다...</li>
</ul>