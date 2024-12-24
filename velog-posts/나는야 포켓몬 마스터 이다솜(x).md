<p><a href="https://www.acmicpc.net/problem/1620">https://www.acmicpc.net/problem/1620</a></p>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;map&gt;
#include &lt;string&gt;

using namespace std;

int n, m;
map&lt;string, int&gt; m1;
map&lt;int, string&gt; m2;
string s;

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);

    cin &gt;&gt; n &gt;&gt; m;

    for (int i = 1; i &lt;= n; i++)
    {
        cin &gt;&gt; s;
        m1.insert({ s,i });
        m2.insert({ i,s });
    }

    for (int i = 0; i &lt; m; i++)
    {
        cin &gt;&gt; s;
        int a = atoi(s.c_str());
        if (atoi(s.c_str()) == 0)
            cout &lt;&lt; m1[s] &lt;&lt; &quot;\n&quot;;
        else
            cout &lt;&lt; m2[atoi(s.c_str())] &lt;&lt; &quot;\n&quot;;
    }
}
</code></pre>
<ul>
<li><p>map을 통해 구하면 되는 문제이다</p>
</li>
<li><p>map으로 string을 키로 int를 저장하는 변수, int를 key로 string 을 저장하는 변수 두개를 만든 뒤 입력받은 s를 현재 i값과 혼용해 저장해준다</p>
</li>
<li><p>문제의 갯수만큼 반복하면서 string 값을 입력받아 atoi 함수를 통해 s 값을 int로 바꿔줄 것인데 int형으로 바꾸지 못하면 0을 return 하는 것을 이용하여 0이 return되면 string을 키로하는 map 변수에 s를 key로 저장한 값을 출력하고 그렇지 않다면 int를 key로 저장한 값을 출력하면 된다</p>
</li>
<li><p>atoi()</p>
<ul>
<li>string 헤더에 구현된 atoi() 함수는 char * const 변수를 int형으로 교체해주는 함수이다</li>
<li>따라서 string 변수를 넣으려면 c_str()로 넣어줘야 한다</li>
<li>문자가 int형으로 변하면 int형 그대로 리턴되지만 변환되지 않으면 0이 리턴된다</li>
</ul>
</li>
</ul>