---
title: UVA-Q133:-The-Dole-Queue
date: 2022-10-25 23:43:25
tags: code
---
只能說我非常的爛==，原本這題實作題還想要用set來處理，然後想反向遍歷set，還好有＠Erichung、@Peterlee兩位大神把我點醒😵‍💫😵‍💫，不然我應該解一整天還是0。
然後我到後面還一度完全輸出不了東西，但用自己的debug函式就可以，原來是因為卡死迴圈，count計數器忘記在刪除兩數時要在多減1，然後debug函式中有flush，因此就把我還在緩衝區的東西先輸出了(實際上死迴圈輸不出東西)，這也是前述兩位大神幫我弄的，我真的好廢，還好的我室友都是電神⚡⚡⚡。

[🔗題目](http://domen111.github.io/UVa-Easy-Viewer/?133)

``` C
#include <bits/stdc++.h>
#define ac ios_base::sync_with_stdio(false);cin.tie(0);
#define mem(a, val) memset(a, val, sizeof(a))
#define pb push_back
#define int long long
#define F first
#define S second
#define maxn 1e8
const double EPS = 1e-7;
using namespace std;
void debug_out() { cerr << "]\n"
                        << flush; }
template <typename Head, typename... Tail>
void debug_out(Head H, Tail... T)
{
    cerr << H;
    if (sizeof...(T))
        cerr << ", ";
    debug_out(T...);
}
#define debug(...)                                                     \
    cerr << "LINE(" << __LINE__ << ") : [" << #__VA_ARGS__ << "] = ["; \
    debug_out(__VA_ARGS__)

signed main(void)
{
    int n, k, m;
    while (cin >> n >> k >> m && n != 0)
    {
        
        int arr[25];
        mem(arr, 0);
        int pick1, pick2;
        int count = n;
        int nowa = 0, nowb = n - 1;
        while (count > 0)
        {

            int kk = k, mm = m;
            while (kk > 0)
            {
                if (arr[nowa] == 0)
                {
                    kk--;
                }
                if (kk != 0)
                    nowa++;
                nowa %= n;
            }

            while (mm > 0)
            {
                if (arr[nowb] == 0)
                {
                    mm--;
                }
                if (mm != 0)
                    nowb--;

                while (nowb < 0)
                    nowb += n;
            }
            if (count > 1&&!(count==2&&nowa!=nowb))
            {
                if (nowa == nowb)
                    cout << setw(3) << nowa + 1 << ',';
                else
                {
                    cout << setw(3) << nowa + 1;
                    cout << setw(3) << nowb + 1 << ',';
                }
            }

            arr[nowa] = 1;
            arr[nowb] = 1;
            if (nowa != nowb){
                count--;
            }
                
            count--;
        }
        if (nowa == nowb)
                    cout << setw(3) << nowa + 1 ;
                else 
                {
                    cout << setw(3) << nowa + 1;
                    cout << setw(3) << nowb + 1 ;
                }
            cout<<'\n';
    }
}

```


