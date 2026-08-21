# Project Euler - Problem 156

### Description:
Starting from zero the natural numbers are written down in base $10$ like this:

$$0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 \cdots$$

Consider the digit $d=1$. After we write down each number $n$, we will update the number of ones that have occurred and call this number $f(n,1)$. The first values for $f(n,1)$, then, are as follows:

| $n$ | $f(n, 1)$ |
| :---: | :---: |
| 0 | 0 |
| 1 | 1 |
| 2 | 1 |
| 3 | 1 |
| 4 | 1 |
| 5 | 1 |
| 6 | 1 |
| 7 | 1 |
| 8 | 1 |
| 9 | 1 |
| 10 | 2 |
| 11 | 4 |
| 12 | 5 |

Note that $f(n,1)$ never equals $3$.

So the first two solutions of the equation $f(n,1)=n$ are $n=0$ and $n=1$. The next solution is $n=199981$.

In the same manner the function $f(n,d)$ gives the total number of digits $d$ that have been written down after the number $n$ has been written.

In fact, for every digit $d \neq 0$, $0$ is the first solution of the equation $f(n,d)=n$.

Let $s(d)$ be the sum of all the solutions for which $f(n,d)=n$.

You are given that $s(1)=22786974071$.

Find $\sum s(d)$ for $1 \le d \le 9$.

**Note:** If, for some $n$, $f(n,d)=n$ for more than one value of $d$, this value of $n$ is counted again for every value of $d$ for which $f(n,d)=n$.

## Solution
We call `f(n,d)` the number of times digit `d` appeared throughout the numbers in the range `[0,n]`

To make it simple, we'll use `d=1` first 

With a simple brute force code, we can see that from 0 to 9, 99, 999, 9999, 99999, the f(n,d) is 1, 20, 300, 4000, 50000 respectively.

```cpp
ull tong=0;

FOR(i,1,99999) {
    ull k=i;
    while (k!=0){
        if (k%10==1) tong++;
        k/=10;
    }
}
cout<<tong;
```
We can then prove this easily.

First `f(9,1)=1`, when we're at `f(99,d)`, `f(9,d)` repeats 10 times from 0-9 as in 01, 11, 21,... then the number one in the tens repeats another 10 times from 10-19. With that observation, we can conclude that at `f(999,d)`, the result is also `10*f(99,d)+10^2`; hence, it proves our observation

Using that formula, we can see that `f(n,d)<n` when `n` is 9, 99, 999,... up to 10^9-1 and `f(n,d)` is 1, 20, 300,... 9*10^8. The time when `f(n,d)` starts to break the trend and get bigger than `n` is at 10^10-1, `f(n,d)` will be 10^10 at any `d`. But if `d>1`, the next `n` is a solution, so the safe limit is at `n=10^11`, which is appoximately `f(n,d)=1.1*10^11`, which creates a safe difference of around 10^10

But then the brute force solutions would take days at 10^11, we'll have to use `Divide and Conquer` in this code to get our solution

Any of `d` would have the upper limit at 10^11 so I will simplify the function `f(n,d)` to `f(n)` that would apply the same rules to any `d`

Every time we're doing calculations on `[A,B]`, the value of `f(x)` with `x` in `[A,B]` of `f` would be in `[f(A),f(B)]` since the result never decreases. The solutions that we're finding are the times that `[A,B]` and `[f(A),f(B)]` intersect. So if `B<f(A)` or `f(B)<A` which makes the two sets never intersect:

....[A...B]......[f(A)...f(B)]....

....[f(A)...f(B)]......[A...B]....

If that condition happens, we can skip `[A,B]` completely because there would be no solution in `[A,B]`. Next, if we repeatedly halve `[A,B]` from the original `[1,10^11]`, which can allow us to skip large intervals of [A,B]

Our first task is to code a function that calculate `f(n)` in $\mathcal{O}(\log_{10}n)$ time because we want to check the condition very fast. We can reconstruct each digit from 0 to `A`, digit by digit. For example, we would calculate from right to left:

```bash
    <-----
A = 817234
```

We call the digit we're at `c` and I'll use the number above with `c=2` to explain it more visually. At 234, the loop 0-99 repeated twice and then go again from 0-34 but it would have been calculated earlier because it was the smaller digit. Because 0-99 repeated 2 times, we add `20` to the result `c` times. Next, if `d < c` (for example `d=1`) then `d` has repeated 100 times, if `d = c` then `d` repeated 34 times, if `d > c` then `d` repeated 0 times as the digit in the hundreds row. Our final result `f(n)` is the sum of those two calculations

```cpp
ull f(ull a){
    ull sum=0;
    int power=0;
    ull zeros=1;
    ull remaindr=0;
    while (a!=0){
        int c=a%10;
        sum+=power*(zeros/10)*c;
        if (c==d) sum+=remaindr+1; else if (c>d) sum+=zeros;
        remaindr+=c*zeros;
        power++;
        a/=10;
        zeros*=10;
    }
    return sum;
}
```

We initiate 4 variables	`sum`, `power`, `zeros` and `remaindr`:

sum : the total times `d` appear from 0 to `A`

power : the length of the number we're slowly calculating from 0 back to `A`

zeros : used to track where the number is

remaindr : for when `d = c`

Then we make a `query` function that will skip the chunk if the condition is met, or will break down the chunk if not. This will run in $\mathcal{O}(K \log_2 N)$
```cpp
void query(ull l,ull r){
    if (l==r) if (f(l)==l) {
        ans+=l;
        return;
    }
    if (f(l)>r||f(r)<l) return;
    ull mid=(l+r)/2;
    query(l,mid);
    query(mid+1,r);
}
```
The full code is below with an additional function to calculate the execution time 

[Time: 34.8492 ms]
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define ull unsigned long long
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
ull ans=0;
ull ma=0;
ull mi=inf;
vector<int> db4(10),daf(10);
int d=1;

ull f(ull a){
    ull sum=0;
    int power=0;
    ull zeros=1;
    ull remaindr=0;
    while (a!=0){
        int c=a%10;
        sum+=power*(zeros/10)*c;
        if (c==d) sum+=remaindr+1; else if (c>d) sum+=zeros;
        remaindr+=c*zeros;
        power++;
        a/=10;
        zeros*=10;
    }
    return sum;
}

ull lim=99999999999;

void query(ull l,ull r){
    if (l==r) if (f(l)==l) {
        ans+=l;
        return;
    }
    if (f(l)>r||f(r)<l) return;
    ull mid=(l+r)/2;
    query(l,mid);
    query(mid+1,r);
}

int main(){
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    tstart;
    while (d<10)
    {
    query(1,lim);
    d++;
    }
    tend;
    cout<<ans<<endl;
}
```
### Answer
21295121502550