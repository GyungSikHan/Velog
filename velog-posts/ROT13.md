<p><a href="https://www.acmicpc.net/problem/11655">https://www.acmicpc.net/problem/11655</a></p>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std;

string s{};
string Result{};

int main()
{
    getline(cin, s);

    for (int i = 0; i &lt; s.size(); i++)
    {
        int temp = 13;
        if(s[i] &gt;= 'a' &amp;&amp; s[i] &lt;='z')
        {
            if (s[i] + temp &gt; 'z')
            {
                temp = (s[i] + 13) - 'z' - 1;
                s[i] = temp + 'a';
            }
            else
                s[i] += temp;

        }
        else if (s[i] &gt;= 'A' &amp;&amp; s[i] &lt;= 'Z')
        {
            if (s[i] + temp &gt; 'Z')
            {
                temp = (s[i] + 13) - 'Z' - 1;
                s[i] = temp + 'A';
            }
            else
                s[i] += temp;
        }
    }

    cout &lt;&lt; s &lt;&lt; endl;
}</code></pre>
<ul>
<li>그냥 생각나는 대로 풀다보니 시간이 좀 오래 걸렸다</li>
<li>getline(cin, 변수)를 사용하면 띄어쓰기도 문자열 안에 입력이 가능하다</li>
<li>입력 받은 string의 문자 하나하나 비교하면서 대소문자 알파벳일 때 13을 더해준다</li>
<li>이때 z나 Z값을 벗어나면 벗어난 만큼 a부터 다시 count해 나오는 결과 값을 저장해주면 된다</li>
</ul>