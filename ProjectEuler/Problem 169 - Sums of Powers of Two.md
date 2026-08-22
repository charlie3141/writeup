# Project Euler - Problem 169

### Description:

Define $f(0) = 1$ and $f(n)$ to be the number of different ways $n$ can be expressed as a sum of integer powers of $2$ using each power no more than twice.

For example, $f(10) = 5$ since there are five different ways to express $10$:

$$
\begin{aligned}
& 1 + 1 + 8 \\
& 1 + 1 + 4 + 4 \\
& 1 + 1 + 2 + 2 + 4 \\
& 2 + 4 + 4 \\
& 2 + 8
\end{aligned}
$$

What is $f(10^{25})$?

## Solution

Our first approach to this problem is to convert `n` to binary since binary numbers are already expressed as sum of integer powers of $2$ `1010`

Every number can be used twice so we can split powers of $2$ into two of the previous powers. For example `8 = 4 + 4`, `2 = 1 + 1`, we can't split 2^0 since we're using integers. So another way to express sums of integers powers of $2$ using each power no more than twice is 
```text
Example of a split:
Power of 2:
    8 | 4 | 2 | 1 

Ex: 1 | 0 | 0 | 0
    0 | 0 | 0 | 0

--->0 | 1 | 0 | 0 
    0 | 1 | 0 | 0


Binary of 10: 1010
Power of 2:
    8 | 4 | 2 | 1 

1.  1 | 0 | 1 | 0
    0 | 0 | 0 | 0
--->8      +2       =10


2.  1 | 0 | 0 | 1
    0 | 0 | 0 | 1
--->8         +1+1  =10


3.  0 | 1 | 0 | 1
    0 | 1 | 0 | 1
--->   4+4    +1+1  =10


4.  0 | 1 | 1 | 1
    0 | 0 | 1 | 1
--->    4 +2+2+1+1  =10


5.  0 | 1 | 1 | 0
    0 | 1 | 0 | 0
--->   4+4 +2       =10
```
Then, I wrote a simple brute force code to find patterns in the number and the result using this observation:

If we can split the sums into two lines of binary like above, we can convert those two lines back to decimal numbers and express the number `n` as a sum of two decimal numbers

We call the two numbers `a` and `b` `(a>=b)`. Since we can exchange number positions in sums we prioritize the power of $2$ to appear in `a` first, so `b` can only have powers of $2$ that `a` has. Now we run `a = (n+1)/2 to n` and `b = n - a`

```cpp
ull n=1;
while (n<=100000000){
    ull tong=0;

    FOR(a,(n+1)/2,n){
        ull b=n-a;
        ull i=a;
        bool no=true;
        while (b!=0){
            if (b%2==1&&i%2==0)
            {
                no=false;
                break;
            }
            b/=2;
            i/=2;
        }
        if (no==true) tong++;
    }
    string s="";
    ull bi=n;
    while (bi!=0){
        s=to_string(bi%2)+s;
        bi/=2;
    }
    cout<<n<<' '<<tong<<endl;
    cout<<s<<endl;

    n*=2;
    tc=tong;
}
```
Then I found that there will be a pattern if we append `0` or `1` at the right of the binary number (or `*2`, `*2+1` in decimal number)

If we append `1`:

```text
Power of 2:
    8 | 4 | 2 | 1 

1.  x | x | 0 | 1
    x | x | 0 | 0
(This situation wouldn't derive from any other than appending to the number 0, if the number 'split' until the last power of two, it would either be one or two number 1 like below)

2.  x | x | 1 | 1
    x | x | 0 | 0

3.  x | x | 1 | 1
    x | x | 1 | 0
```
We can see in none of the situation can we 'split' and get another solution from the previous number, so we can conclude `f(n) = f(2n+1)`

If we append `0`:
```text
Power of 2:
    8 | 4 | 2 | 1 

1.  x | x | 0 | 0
    x | x | 0 | 0



2.  x | x | 1 | 0
    x | x | 0 | 0

--->x | x | 0 | 1
    x | x | 0 | 1



3.  x | x | 1 | 0
    x | x | 1 | 0

--->x | x | 1 | 1
    x | x | 0 | 1
```
We can see that it makes room for another set of solution:

-When we does not 'split' to the last power, `set 1 = f(n)`

-When we 'split' to the last power, we can add the solution of `set 2 = f(n-1)` to our total. We can see that after adding `0` and 'split' to fill the last power of two, the second to last power of two opens up one slot, it is `f(n-1)`

So we can conclude that `f(n) + f(n-1) = f(2n)`

With those two rules, we can calculate the total from left to right using the binary form of `n` and only two variables to keep track of `f(n)` and `f(n-1)`
```cpp
ull p=1;
ull ans=1;
string s="00001000101100101010001011000010100000000010100100001001010000000000000000000000000";
for(auto u:s){
    if (u=='1'){
        p+=ans;
    } else{
        ans+=p;
    }
}
cout<<ans;
```
We convert 10^25 to binary, remove the first `1` and calculate it ourselves to make it easier to code and set `ans=1`, `p=1` whereas `f(n) = ans` and `f(n-1) = p`

The simpler binary number to explain is number `0`, because we can simply use the formula we made earlier `ans = ans + p`

About the number `1`, we have to maintain the `p = f(n-1)` instead of `f(n)` now. We call our new `u = n-1`, `p = f(u)`. Our `n` is odd, so `u` is even; therefore, we can use the formula `f(t) + f(t-1) = f(u)` (`t` is `u/2`). Since no variables were modified, `f(t) = ans`, and `f(t-1) = p`. 

To sum up, our code to append `1` is `p = p + ans`

Full code:
```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define ull  long long
#define fi first
#define se second
#define re resize
#define FOR(i,a,b) for(ull (i)=(a);(i)<=(b);(i)++)
#define FORR(u,a) for(auto (u):(a))
#define ALL(a) (a).begin(),(a).end()
#define el '\n'
#define db(x) cout << (#x) << ": " << x << endl
#define dba(x) FORR(v,x) cout<< (#x) <<": "<<v<<endl
#define sz(a) (int)(a).size()
#define V(a) vector<a>
#define tstart auto _start = chrono::high_resolution_clock::now();
#define tend auto _end = chrono::high_resolution_clock::now(); \
                 cout << "\n[Time: " << chrono::duration<double, milli>(_end - _start).count() << " ms]\n";

using pii=pair<int,int>;
const ll inf=(ll)9e18;
const int mo=1e9+7;
const ull mono=(1e9+7)*10;
int timer=0;
bool fin=false;
int n,m,q;
vector<vector<int>>adj;
vector<ll>par,seg,ao,bit,nex,pre;
vector<bool>vis;
ull ma=0;
ull mi=inf;


int main(){
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    tstart;

    ull p=1;
    ull ans=1;
    string s="00001000101100101010001011000010100000000010100100001001010000000000000000000000000";
    for(auto u:s){
        if (u=='1'){
            p+=ans;
        } else{
            ans+=p;
        }
    }
    cout<<ans;
    tend;
    return 0;
}
```
### Answer
178653872807