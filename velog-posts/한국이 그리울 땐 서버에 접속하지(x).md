<p><a href="https://www.acmicpc.net/problem/9996">https://www.acmicpc.net/problem/9996</a></p>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;vector&gt;
using namespace std;

int n{};
string s{}, ori_s, pre, suf;

int main()
{
    cin &gt;&gt; n;
    cin &gt;&gt; ori_s;
    int pos = ori_s.find('*');
    pre = ori_s.substr(0, pos);
    suf = ori_s.substr(pos + 1);

    for (int i = 0; i &lt; n; i++)
    {
        cin &gt;&gt; s;
        if (pre.size() + suf.size() &gt; s.size())
            cout &lt;&lt; &quot;NE&quot; &lt;&lt; endl;
        else
        {
            if (pre == s.substr(0, pre.size()) &amp;&amp; suf == s.substr(s.size() - suf.size()))
                cout &lt;&lt; &quot;DA&quot; &lt;&lt; endl;
            else
                cout &lt;&lt; &quot;NE&quot; &lt;&lt; endl;
        }
    }

}</code></pre>
<ul>
<li>아이디어가 떠오르지 않고 문제가 이해하기 난해했다 해야하나? 그래서 어려웠던 문제이다</li>
<li>오류가 뜨는 패턴이 * 앞뒤에 문자가 들어가는데 파일 이름에 앞 뒤에 그 문자가 들어가 있어야 한다</li>
<li>즉 a*d면 aaslkdjfklasjflksjakldfjlkdasjd 이런식으로 맨 앞은 a, 맨 뒤는 d가 들어가야한다</li>
<li>또한 앞뒤 문자가 문자열로 되어 있을 수 도 있다는 생각을 하고 풀어야 한다</li>
<li>오류 패턴 ori_s를 입력받아 *가 들어가는 위치를 find 함수를 통해 찾아준다</li>
<li>substr() 함수는 첫번째 파라미터 값 부터 두 번째 파라미터 값 전 까지 리턴해주는 함수로 pre 변수에 ori_s의 0번지부터 *이 있는 지점 전까지 저장해준다</li>
<li>마찬가지로 *이 있는 다음 지점부터 끝까지 suf에 저장해주어 앞뒤 문자를 따로 변수로 저장했다</li>
<li>이제 파일 이름을 입력받고 앞뒤 문자열의 사이즈를 더한 값보다 파일이름의 문자열 사이즈가 더 작다면 비교할 필요도 없이 일치하지 않으므로 NE를 출력한다</li>
<li>그렇지 않다면 substr()함수를 사용해서 파일의 0번지부터 앞 문자의 사이즈만큼 뽑아 앞 문자와 비교하고, 파일의 문자열 사이즈와 뒤 문자열의 사이즈를 뺀 값부터 끝까지 파일의 문자열을 뽑아 뒤 문자열과 비교한다</li>
<li>두개다 모두 같다면 파일이 존재한 것이므로 DA를 아니면 NE를 출력하면 된다</li>
</ul>