<p><a href="https://www.acmicpc.net/problem/2828">https://www.acmicpc.net/problem/2828</a></p>
<pre><code class="language-C++">#include &lt;iostream&gt;

using namespace std;

int n, m;
int j;
int start;
int length;
int apple;
int result;

int  main()
{
    cin &gt;&gt; n &gt;&gt; m;
    cin &gt;&gt; j;

    start = 1;

    for (int i = 0; i &lt; j; i++)
    {
        length = start + m - 1;
        cin &gt;&gt; apple;


        if (apple &lt; start)
        {
            result += (start - apple);
            start = apple;
        }
        else if (apple &gt; length)
        {
            start += apple - length;
            result += apple - length;
        }

    }

    cout &lt;&lt; result &lt;&lt; endl;
}</code></pre>
<ul>
<li>너무 쉬운 문젠대 너무 어렵게 풀려해서 못풀고 정답을 봐버렸다...</li>
<li>1~n까지 위치에서 사과가 떨어진다 했을 때 바구니의 크기를 배열로 받아 풀려했었다 </li>
<li>하지만 만만치 않았고, 문제 해설을 보니 바구니가 시작하는 위치와 바구니의 끝거리를 구해 그 안에서 사과가 떨어지면 된다는것을 알게되었다</li>
<li>이를 그림으로 표현해보면 밑에처럼 될 수 있다
<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/7a1fdf60-40c4-4fac-a016-fc754aef0829/image.png" /></li>
<li>바구니는 어짜피 1지점에서 무조건 시작하므로 바구니의 첫 시작 위치를 1로하고 입력받은 바구니의 크기 m으로 입력받아 움직인다 했을 때 첫 시작 위치와 바구니의 크기는 설정이 됐지만 바구니가 움직이고나서 바구니의 끝 위치가 사과가 떨어지는 위치를 벗어난지 안벗어난지 확인도 안될 뿐더러 앞뒤 어디로 움직여야될지도 표현하는게 어려웠다</li>
<li>그래서 length라는 바구니의 길이를 따로 계산을 해주기 위해 s와 m을 더해줬지만 그렇게 되면 우리가 생각한 바구니보다 커지므로 -1까지 해줘 바구니의 길이를 만들어준다</li>
<li>다시 말하지만 왜 m으로 바구니의 길이를 하지않고 번거롭게 length를 계산해 사용하냐면 m은 말그대로 바구니의 크기이고 움직였을 때 현재 바구니가 걸처있는 위치를 나타내기 위해 s와 length를 사용한 것이다</li>
<li>이제 apple이 떨어지는 위치와 s를 비교해 s가 더 크다면 왼쪽으로 움직이고, apple이 떨어지는 위치보다 length가 작다면 오른쪽으로 움직여 사과를 받을 것이다</li>
<li>각각 if문을 통해 구현하는데 전자같은 경우는 현 위치에서 사과가 있는 곳까지 움직여야하므로 s - apple을 하여 얼마나 움직일지 계산 후 result에 누적해 더해준다음 s에 apple을 저장해 위치를 조정해준다</li>
<li>후자는 result에 apple - length를 한 값을 더해 오른쪽으로 이동한 횟수를 구해주고 이동을 했으니 s의 위치를 바꿔주기 위해 apple - length를 저장해주면 된다</li>
<li>이처럼 쉬운 문제를 못풀다니 더욱더 노력해야겠다는 생각만 든다</li>
</ul>