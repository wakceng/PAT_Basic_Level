### 1、是不是素数

```c
bool is_prime(int x)
{
    if (x < 2) return false;
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0)
            return false;
    return true;
}
```

```
不推荐写i*i<=n，因为当n在int的边界的时候，i*i容易溢出；
不推荐用sqrt，因为算起来比较麻烦；
还是写  i <= x / i 是最优的
```



### 2、分解质因数

```
对于每个正整数 a，按照从小到大的顺序输出其分解质因数后，每个质因数的底数和指数，每个底数和指数占一行。
输入：
6
输出：
2 1
3 1
输入：
8
输出
2 3
```

```c
void divide(int x)
{
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0)
        {
            int s = 0;
            while (x % i == 0) x /= i, s ++ ;
            cout << i << ' ' << s << endl;
        }
    if (x > 1) cout << x << ' ' << 1 << endl;
    cout << endl;
}
```

```
这题能用i <= x / i的原因是，一个数最多只有一个大于其根号的质因数。
```



### 3、筛法求素数

```c
//埃式筛法
int primes[N], cnt=0;     // primes[]存储所有素数
bool st[N];  // st[x]存储x是否被筛掉，true表示i不是素数

void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        if (st[i]) continue;
        primes[cnt ++ ] = i;
        for (int j = i + i; j <= n; j += i)
            st[j] = true;
    }
}
```

```c
//线性筛法（比上一个快）
int primes[N], cnt;     // primes[]存储所有素数
bool st[N];         // st[x]存储x是否被筛掉

void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ )
        {
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;//primes[j]一定是i的最小质因子
        }
    }
}
```



### 4、试除法求所有约数

```c
vector<int> get_divisors(int x)
{
    vector<int> res;
    for (int i = 1; i <= x / i; i ++ )
        if (x % i == 0)
        {
            res.push_back(i);
            if (i != x / i) res.push_back(x / i);
        }
    sort(res.begin(), res.end());
    return res;
}
```



### 5、约数个数&约数之和

```
如果一个数N = p1^c1 * p2^c2 * ... *pk^ck分解质因数后有上述结果
那么约数个数： (c1 + 1) * (c2 + 1) * ... * (ck + 1)
那么约数之和： (p1^0 + p1^1 + ... + p1^c1) * ... * (pk^0 + pk^1 + ... + pk^ck)
```



### 6、辗转相除法

```c
int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}
```



### 7、欧拉函数（1-n中与n互质的个数）

```c
//定义法
int phi(int x)
{
    int res = x;
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0)
        {
            res = res / i * (i - 1);
            while (x % i == 0) x /= i;
        }
    if (x > 1) res = res / x * (x - 1);
    return res;
}
```



### 8、高斯消元求多元一次方程组

```c
// a[N][N]是增广矩阵
int gauss()
{
    int c, r;
    for (c = 0, r = 0; c < n; c ++ )
    {
        int t = r;
        for (int i = r; i < n; i ++ )   // 找到绝对值最大的行
            if (fabs(a[i][c]) > fabs(a[t][c]))
                t = i;

        if (fabs(a[t][c]) < eps) continue;
        for (int i = c; i <= n; i ++ ) swap(a[t][i], a[r][i]);
      // 将绝对值最大的行换到最顶端
        for (int i = n; i >= c; i -- ) a[r][i] /= a[r][c];// 将当前行的首位变成1
        for (int i = r + 1; i < n; i ++ )       // 用当前行将下面所有的列消成0
            if (fabs(a[i][c]) > eps)
                for (int j = n; j >= c; j -- )
                    a[i][j] -= a[r][j] * a[i][c];

        r ++ ;
    }

    if (r < n)
    {
        for (int i = r; i < n; i ++ )
            if (fabs(a[i][n]) > eps)
                return 2; // 无解
        return 1; // 有无穷多组解
    }

    for (int i = n - 1; i >= 0; i -- )
        for (int j = i + 1; j < n; j ++ )
            a[i][n] -= a[i][j] * a[j][n];

    return 0; // 有唯一解
}
```



### 9、求组合数

```
有一个公式，C[a][b]=C[a-1][b-1] + C[a][b-1];
意思是从b个球中选a个，可以理解为两种选球，第一是选的球中有一个特定的球，第二是选的球中没有一个特定的球，第一种一个球已经是固定的所以方案有b-1个球中选a-1个，第二种没有那个特定的球就是在b-1中选a个球
```

```c
// c[a][b] 表示从a个苹果中选b个的方案数
for (int i = 0; i < N; i ++ )
    for (int j = 0; j <= i; j ++ )
        if (j==0) c[i][j] = 1;//当j是0时
        else c[i][j] = (c[i - 1][j] + c[i - 1][j - 1]) % mod;
//在i个苹果中选j个
```



### 10、卡特兰数

```
给定n个0和n个1，它们按照某种顺序排成长度为2n的序列，满足任意前缀中0的个数都不少于1的个数的序列的数量为： Cat(n) = C(2n, n) / (n + 1)
```

```
00走到66一共有C[12][6]种情况，不超过x=y线的走法有C[12][6]-C[12][5]种
```

