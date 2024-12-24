<p><a href="https://www.acmicpc.net/problem/1213">https://www.acmicpc.net/problem/1213</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;

using namespace std;

string s, ret;
int arr[200];
char temp;
int flag{};

int main()
{
    cin &gt;&gt; s;
    for (char a : s)
        arr[a]++;

    for (int i = 'Z'; i &gt;= 'A'; i--)
    {
        if (arr[i] != 0)
        {
            if(arr[i] % 2 == 1)
            {
                temp = (char)(i);
                flag++;
                arr[i]--;
            }
            if(flag &gt;= 2)
                break;
            for (int j = 0; j &lt; arr[i]; j+=2)
            {
                ret = (char)(i) + ret;
                ret += (char)(i);
            }
        }
    }

    if (temp != '\0')
        ret.insert(ret.begin() + ret.size() / 2, temp);

    if (flag &gt;= 2)
        cout &lt;&lt; &quot;I'm Sorry Hansoo&quot; &lt;&lt; endl;
    else
        cout &lt;&lt; ret &lt;&lt; endl;
}</code></pre>
<ul>
<li>펠린드롬은 앞뒤로 읽어도 같은 문자를 말한다</li>
<li>안될 경우를 생각해 봐야 하는데 홀수가 2개 이상일 때 불가능 할 것이다</li>
<li>생각보다 많이 쉬운 문제였지만 뇌가 굳었는지 왜 못 풀고 틀렸을까..ㅠ</li>
<li>일단 arr배열에 string 변수 s를 하나하나 가져와 그것을 index로 알파벳의 갯수를 저장해준다</li>
<li>오름차순으로 정렬을 해야하기 때문에 i = Z부터 A가 될 때 까지 for문을 돌것이다</li>
<li>이때 arr[i]가 0이면 연산을 하지 않아도 된다</li>
<li>arr[i]가 홀수일 때 펠린트롬의 중간에 arr[i]의 알파벳을 넣어주기 위해 char 변수 temp에 저장한 뒤 flag를 증가시켜 홀수의 갯수를 판단해준다</li>
<li>arr[i]의 갯수를 하나 감소시켜 사용했다는 것을 표현해준다</li>
<li>if문을 탈출하고 flag 값이 2보다 크거나 같으면 펠린트롬이 안되므로 반복문을 그만두기 위해 break를 사용해준다</li>
<li>이것도 탈출하게 되면 반복문을 통해 j = 0부터 arr[i]보다 작을경우 j+=2를 하여 j를 두개씩 늘려주는 반복문을 만들어준다</li>
<li>j를 +2하는 이유는 반복문 안에있는데 일단 오름차순으로 펠린트롬을 만들어야 하므로 ret 변수에 i를 char로 캐스팅한 값과 현재 ret을 더해 저장해준다</li>
<li>그 후 이번엔 ret에 i를 char로 캐스팅 한 값을 ret뒤에 더해 펠린트롬을 완성한다</li>
<li>이처럼 arr[i]에 있는 알파벳을 2개씩 사용하기 때문에 j+=2를 통해 j를 2개씩 올려준 것이다</li>
<li>모든 연산이 끝나고 temp가 \0(널문자)가 아닌 경우 중간 값이 있단 소리이므로 ret의 중간을 찾아 temp를 넣어준다</li>
<li>이제 flag가 2보다 크거나 같으면 I'm Sorry Hansoo를 출력해 실패를 출력하고 그렇지 않다면 ret을 출력해 만든 펠린트롬을 출력해준다</li>
</ul>