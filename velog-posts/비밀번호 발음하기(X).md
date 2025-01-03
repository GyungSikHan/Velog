<p><a href="https://www.acmicpc.net/problem/4659">https://www.acmicpc.net/problem/4659</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;string&gt;
using namespace std;

string s;

bool Check(char c)
{
    return (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u');
}

int main()
{
    while (true)
    {
        cin &gt;&gt; s;
        if (s == &quot;end&quot;)
            break;
        int same{}, same2{};
        bool bResult{}, bTemp{};
        char temp{};

        for (int i = 0; i &lt; s.size(); i++)
        {
            if(Check(s[i]) == true)
            {
                same++;
                same2 = 0;
                bTemp = true;
            }
            else
            {
                same2++;
                same = 0;
            }
            if (same == 3 || same2 == 3)
                bResult = true;
            if (i &gt;= 1 &amp;&amp; temp == s[i] &amp;&amp; (s[i] != 'e' &amp;&amp; s[i] != 'o'))
                bResult = true;

            temp = s[i];
        }

        if (bTemp == false)
            bResult = true;
        if (bResult == false)
            cout &lt;&lt; &quot;&lt;&quot; &lt;&lt; s &lt;&lt; &quot;&gt;&quot; &lt;&lt; &quot; is acceptable.&quot; &lt;&lt; endl;
        else
            cout &lt;&lt; &quot;&lt;&quot; &lt;&lt; s &lt;&lt; &quot;&gt;&quot; &lt;&lt; &quot; is not acceptable.&quot; &lt;&lt; endl;
    }
}</code></pre>
<ul>
<li>너무 복잡하고 지저분하게 풀어서 문제가 어디인지 파악하기 힘들어 다시 푼 문제이다</li>
<li>일단 조건에서 모음이 하나라도 들어가야 하므로 bTemp 변수를 통해 모음이 하나라도 존재하면 true로 바꿔줄 것이고, 모음이나 자음이 연속으로 3번이상 들어오면 안되므로 각각 숫자를 새어줄 변수도 만들어주고, 결과를 바꿔줄 bool 형 변수 bResult도 만들어준다</li>
<li>string 안에있는 값을 하나하나 비교할 것인데 먼저 Check 함수를 통해 현재 단어가 모음인지 판단해 모음이 맞다면 bTemp를 true로 바꿔 모음이 들어갔다는 것을 알려주고, same을 ++ 하여 모음이 연속적으로 나온 횟수를 늘려줌과 동시에 자음의 연속 횟수인 same2 = 0으로 만들어준다</li>
<li>Check가 flase여서 else로 갈 경우에는 자음이란 소리이므로 same2을 ++해주고 same2를 0으로 만들어준다</li>
<li>이때 same이나 same2가 3이면 bResult를 true로 바꿔주어 연속으로 자음, 모음중 하나가 3번이상 나와 틀렸다는 것을 표시해준다</li>
<li>또한 i &gt;= 1일때 즉 string의 크기가 1보다 클때 temp와 s[i]를 비교해 같은 글자면 ee, oo 와 같은 글자인지를 판단해 아니라면 같은 알파벳이 연속해 등장한 것이므로 bResult를 true로 바꿔준다</li>
<li>이렇게 string을 모두 탐색한뒤 bTemp가 false면 모음이 안들어간 경우이므로 bResult를 true로 바꿔주고 결과에 맞는 값을 출력해주면 된다</li>
</ul>