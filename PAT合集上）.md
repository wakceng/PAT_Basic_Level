# [PAT练习](https://pintia.cn/problem-sets/994805260223102976/exam/problems/type/7)

## 1001-1010

### PAT_1001害死人不偿命的(3n+1)猜想

```c
/*卡拉兹(Callatz)猜想：
 对任何一个正整数n，如果它是偶数，那么把它砍掉一半；如果它是奇数，那么把(3n+1)砍掉一半。这样一直反复砍下去，最后一定在某一步得到 n=1。卡拉兹在1950年的世界数学家大会上公布了这个猜想，传说当时耶鲁大学师生齐动员，拼命想证明这个貌似很傻很天真的命题，结果闹得学生们无心学业，一心只证 (3n+1)，以至于有人说这是一个阴谋，卡拉兹是在蓄意延缓美国数学界教学与科研的进展……
 我们今天的题目不是证明卡拉兹猜想，而是对给定的任一不超过 1000 的正整数 n，简单地数一下，需要多少步（砍几下）才能得到 n=1？
 输入格式：
 每个测试输入包含 1 个测试用例，即给出正整数 n 的值。
 输出格式：
 输出从 n 计算到 1 需要的步数。
 输入样例：
 3
 输出样例：
 5
 */

#include<stdio.h>

int main(){
    int step=0,n=0;
    scanf("%d",&n);
    while(n!=1){
        if(n%2==0) {
            n=n/2;
            step++;
        }
        else{
            n=(3*n+1)/2;
            step++;
        }
    }
    printf("%d\n",step);
    return 0;
}
```



### PAT_1002写出这个数

```c
/*读入一个正整数 n，计算其各位数字之和，用汉语拼音写出和的每一位数字。
 输入格式：
 每个测试输入包含 1 个测试用例，即给出自然数 n 的值。这里保证 n 小于 10^100。
 输出格式：
 在一行内输出 n 的各位数字之和的每一位，拼音数字间有 1 空格，但一行中最后一个拼音数字后没有空格。
 输入样例：
 1234567890987654321123456789
 输出样例：
 yi san wu
 */

#include<stdio.h>
#include<string.h>

int main(){
    char num[105]={0};
    int s[10]={0};
    int sum=0,i=0;
    gets(num);
    for(int i=0;i<strlen(num);i++){
        sum=sum+(num[i]-'0');
    }
//    printf("%d\n",sum);
    while(sum>=10){
        s[i++]=sum%10;
        sum=sum/10;
    }
    s[i++]=sum;
    for(int j=(i-1);j>0;j--){
        switch(s[j]){
            case 0:printf("ling");break;
            case 1:printf("yi");break;
            case 2:printf("er");break;
            case 3:printf("san");break;
            case 4:printf("si");break;
            case 5:printf("wu");break;
            case 6:printf("liu");break;
            case 7:printf("qi");break;
            case 8:printf("ba");break;
            case 9:printf("jiu");break;
        }
        printf(" ");
    }
    switch(s[0]){
        case 0:printf("ling");break;
        case 1:printf("yi");break;
        case 2:printf("er");break;
        case 3:printf("san");break;
        case 4:printf("si");break;
        case 5:printf("wu");break;
        case 6:printf("liu");break;
        case 7:printf("qi");break;
        case 8:printf("ba");break;
        case 9:printf("jiu");break;
    }
    printf("\n");
    return 0;
}
```



### PAT_1003我要通过

```c
/*“答案正确”是自动判题系统给出的最令人欢喜的回复。本题属于PAT的“答案正确”大派送——只要读入的字符串满足下列条件，系统就输出“答案正确”，否则输出“答案错误”。得到“答案正确”的条件是：字符串中必须仅有P、A、T这三种字符，不可以包含其它字符；任意形如 xPATx 的字符串都可以获得“答案正确”，其中 x 或者是空字符串，或者是仅由字母 A 组成的字符串；如果 aPbTc 是正确的，那么 aPbATca 也是正确的，其中 a、 b、 c均或者是空字符串，或者是仅由字母 A 组成的字符串。现在就请你为 PAT 写一个自动裁判程序，判定哪些字符串是可以获得“答案正确”的。
输入格式：
每个测试输入包含1个测试用例。第1行给出一个正整数n(≤10)，是需要检测的字符串个数。接下来每个字符串占一行，字符串长度不超过 100，且不包含空格。
 输出格式：
 每个字符串的检测结果占一行，如果该字符串可以获得“答案正确”，则输出 YES，否则输出 NO。
 输入样例：
 10
 PAT
 PAAT
 AAPATAA
 AAPAATAAAA
 xPATx
 PT
 Whatever
 APAAATAA
 APT
 APATTAA
 输出样例：
 YES
 YES
 YES
 YES
 NO
 NO
 NO
 NO
 NO
 NO*/

#include<stdio.h>
#include<string.h>

int main(){
    int n=0,i,j;
    int count_p,count_t,count_a,pos_p,pos_t;
    char c[200];
    scanf("%d\n",&n);
    for(i=0;i<n;i++){
        gets(c);
        count_p=0;count_a=0;count_t=0;pos_t=-1;pos_p=-1;
        for(j=0;j<strlen(c);j++){
            if(c[j]=='P'){
                count_p++;
                pos_p=j;
            }
            else if (c[j]=='T'){
                count_t++;
                pos_t=j;
            }
            else if (c[j]=='A'){
                count_a++;
            }

        }
        if( count_p+count_a+count_t!=strlen(c) )  printf("NO\n");
        else if( pos_t-pos_p<=1 ) printf("NO\n");
        else if( count_p>1 ) printf("NO\n");
        else if( count_t>1 ) printf("NO\n");
        else if( pos_p*(pos_t-pos_p-1)!=strlen(c)-pos_t-1) printf("NO\n");
        else printf("YES\n");
    }
    return 0;
}
```



### PAT_1004成绩排名

```c
/*读入 n（>0）名学生的姓名、学号、成绩，分别输出成绩最高和成绩最低学生的姓名和学号。
 输入格式：
 每个测试输入包含 1 个测试用例，格式为
 第 1 行：正整数 n
 第 2 行：第 1 个学生的姓名 学号 成绩
 第 3 行：第 2 个学生的姓名 学号 成绩
   ... ... ...
 第 n+1 行：第 n 个学生的姓名 学号 成绩
 其中姓名和学号均为不超过10个字符的字符串，成绩为0到100之间的一个整数，这里保证在一组测试用例中没有两个学生的成绩是相同的。
 输出格式：
 对每个测试用例输出 2 行，第 1 行是成绩最高学生的姓名和学号，第2行是成绩最低学生的姓名和学号，字符串间有1空格。
 输入样例：
 3
 Joe Math990112 89
 Mike CS991301 100
 Mary EE990830 95
 输出样例：

 Mike CS991301
 Joe Math990112
 */

#include<stdio.h>

int main(){
    int n,i,max=0,min=0;
    struct stu{
        char name[15];
        char no[15];
        int grade;
    }students[200];
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%s %s %d",students[i].name,students[i].no,&students[i].grade);
        if(students[i].grade>students[max].grade) max=i;
        if(students[i].grade<students[min].grade) min=i;
    }
    printf("%s %s\n",students[max].name,students[max].no);
    printf("%s %s\n",students[min].name,students[min].no);
    return 0;
}
```



### PAT_1005继续(3n+1)猜想

```c
/*卡拉兹(Callatz)猜想已经在1001中给出了描述。在这个题目里，情况稍微有些复杂。
 当我们验证卡拉兹猜想的时候，为了避免重复计算，可以记录下递推过程中遇到的每一个数。例如对n=3进行验证的时候，我需要计算3、5、8、4、2、1，则当我们对n=5、8、4、2进行验证的时候，就可以直接判定卡拉兹猜想的真伪，而不需要重复计算，因为这 4个数已经在验证3的时候遇到过了，我们称5、8、4、2是被3“覆盖”的数。我们称一个数列中的某个数 n 为“关键数”，如果 n 不能被数列中的其他数字所覆盖。
 现在给定一系列待验证的数字，我们只需要验证其中的几个关键数，就可以不必再重复验证余下的数字。你的任务就是找出这些关键数字，并按从大到小的顺序输出它们。
 输入格式：
 每个测试输入包含 1 个测试用例，第 1 行给出一个正整数 K (<100)，第 2 行给出 K 个互不相同的待验证的正整数 n (1<n≤100)的值，数字间用空格隔开。
 输出格式：
 每个测试用例的输出占一行，按从大到小的顺序输出关键数字。数字间用 1 个空格隔开，但一行中最后一个数字后没有空格。
 输入样例：
 6
 3 5 6 7 8 11
 输出样例：

 7 6
 */

#include<stdio.h>

int main(){
    int k,i,n[5000]={0},t=0,flag[5000]={0},m[150]={0};
    scanf("%d",&k);
    for(i=0;i<k;i++){
        scanf("%d",&n[i]);
        flag[n[i]]=1;
    }
    //对每一个n【i】进行判断
    for(i=0;i<k;i++){
        while(n[i]!=1){
            if(n[i]%2==0) n[i]=n[i]/2;
            else n[i]=(3*n[i]+1)/2;
            flag[n[i]]=0;
        }
    }
    flag[1]=0;
    
   //输出
    for(i=150;i>=0;i--){
        if(flag[i]==1){
            m[t++]=i;
        }
    }
    for(i=0;i<t-1;i++){
        printf("%d ",m[i]);
    }
    printf("%d\n",m[t-1]);
    
    return 0;
}
```

```
思路：flag[n[i]]=1;每一个出现的数字的flag赋值为1；然后对每一个出现的数字进行对半操作，并将每次对半的值的flag赋值为0；然后查看flag是1的数，表示没有被其他数对半操作到；然后将这个flag是1的数放到m中输出。
```



### PAT_1006换个格式输出整数

```c
/*让我们用字母B来表示“百”、字母S表示“十”，用12...n来表示不为零的个位数字n（<10），换个格式来输出任一个不超过 3 位的正整数。例如 234 应该被输出为 BBSSS1234，因为它有2个“百”、3 个“十”、以及个位的 4。
 输入格式：
 每个测试输入包含 1 个测试用例，给出正整数 n（<1000）。
 输出格式：
 每个测试用例的输出占一行，用规定的格式输出 n。
 输入样例 1：
 234
 输出样例 1：
 BBSSS1234
 输入样例 2：
 23
 输出样例 2：
 SS123
 */

#include <stdio.h>

int main(){
    int n,num[10]={0},i,t=0;
    scanf("%d",&n);
    while(n>=10){
        num[t++]=n%10;
        n=n/10;
    }
    num[t]=n;
    for(i=0;i<num[2];i++){printf("B");}
    for(i=0;i<num[1];i++){printf("S");}
    for(i=1;i<=num[0];i++) printf("%d",i);

    printf("\n");
    return 0;
}
```



### PAT_1007素数对猜想

```c
/*让我们定义dn为：dn=pn+1 −pn，其中pi是第i个素数。显然有d1=1，且对于n>1有dn是偶数。“素数对猜想”认为“存在无穷多对相邻且差为2的素数”。
 现给定任意正整数N(<105)，请计算不超过N的满足猜想的素数对的个数。
 输入格式:
 输入在一行给出正整数N。
 输出格式:
 在一行中输出不超过N的满足猜想的素数对的个数。
 输入样例:
 20
 输出样例:
 4
 */

#include<stdio.h>
#include<math.h>

int is_su(int x);//判断是否是素数的函数

int main(){
    int n,i,su[10000]={2,0},t=1,all=0;//100000内只有9500+个素数
    scanf("%d",&n);
    for(i=3;i<=n;i++){
        if(!is_su(i)) su[t++]=i;//如果是素数就把数据放在素数数组中
//        printf("t=%d,i=%d\n",t,i);
    }
    for(i=0;i<t;i++){
        if(su[i+1]-su[i]==2) all++;
    }
    printf("%d\n",all);
    return 0;
}

int is_su(int x){
    int i,flag=0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) flag++;
    }
    return flag;
}
```



### PAT_1008数组元素循环右移问题

```
上下两个答案提交都是全部正确的，特别要注意的是因为没有限定m的范围所以一定要加m=m%n;说要移动次数尽量少其实和左移还是右移没有关系。
```

```c
/*一个数组A中存有N（>0）个整数，在不允许使用另外数组的前提下，将每个整数循环向右移M（≥0）个位置，即将A中的数据由（A0A1⋯AN−1）变换为（AN−M⋯AN−1A0A1⋯AN−M−1）（最后M个数循环移至最前面的M个位置）。如果需要考虑程序移动数据的次数尽量少，要如何设计移动的方法？
 输入格式:
 每个输入包含一个测试用例，第1行输入N（1≤N≤100）和M（≥0）；第2行输入N个整数，之间用空格分隔。
 输出格式:
 在一行中输出循环右移M位以后的整数序列，之间用空格分隔，序列结尾不能有多余空格。
 输入样例:
 6 2
 1 2 3 4 5 6
 输出样例:
 5 6 1 2 3 4
 */

//要移动的次数尽量少，一定条件左移
//移动次数最少应该用直接赋值到另一个数组

#include<stdio.h>

int main(){
    int n,m,i,j,num[100]={0},t;
    scanf("%d%d",&n,&m);//n是整数个数。m是移动次数。
    m=m%n;
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
    }
    //yiwei
    //此时往右移
    if(n>2*m){
        while(m--){
            t=num[n-1];
            for(i=0;i<n-1;i++){
                num[n-1-i]=num[n-2-i];
            }
            num[0]=t;
        }
    }
    //此时左移
    else{
        m=n-m;
        while(m--){
            t=num[0];
            for(i=0;i<n-1;i++){
                num[i]=num[i+1];
            }
            num[n-1]=t;
        }
    }
    //shuchu
    for(i=0;i<n-1;i++){
        printf("%d ",num[i]);
    }
    printf("%d\n",num[n-1]);
    return 0;
}
```

```c
#include<stdio.h>

int main(){
    int n,m,i,num[300]={0};
    scanf("%d%d",&n,&m);//n是整数个数。m是移动次数。
    m=m%n;
    for(i=m;i<n+m;i++){
        scanf("%d",&num[i]);
    }
    for(i=0;i<m;i++){
        num[i]=num[i+n];
    }

    for(i=0;i<n-1;i++){
        printf("%d ",num[i]);
    }
    printf("%d\n",num[n-1]);
    return 0;
}
```



### PAT_1009说反话

```c
/*给定一句英语，要求你编写程序，将句中所有单词的顺序颠倒输出。
 输入格式：
 测试输入包含一个测试用例，在一行内给出总长度不超过80的字符串。字符串由若干单词和若干空格组成，其中单词是由英文(大小写有区分）组成的字符串，单词之间用 1 个空格分开，输入保证句子末尾没有多余的空格。
 输出格式：
 每个测试用例的输出占一行，输出倒序后的句子。
 输入样例：
 Hello World Here I Come
 输出样例：
 Come I Here World Hello
 */

#include<stdio.h>
#include<string.h>

int main(){
    char s[100][100]={0},c;
    int i=0,j=0;
    while(1){
        scanf("%c",&c);
        if(c=='\n') {break;}
        else{
            if(c==' ')  {i++;j=0;}
            else {s[i][j]=c;j++;}
        }
    }
    for(;i>0;i--){
        printf("%s ",s[i]);
    }
    printf("%s\n",s[0]);
    return 0;
}
```



### PAT_1010一元多项式求导

```c
/*一元多项式求导
 输入格式:
 以指数递降方式输入多项式非零项系数和指数（绝对值均为不超过 1000 的整数）。数字间以空格分隔。
 输出格式:
 以与输入相同的格式输出导数多项式非零项的系数和指数。数字间以空格分隔，但结尾不能有多余空格。注意“零多项式”的指数和系数都是 0，但是表示为 0 0。
 输入样例:
 3 4 -5 2 6 1 -2 0
 输出样例:
 12 3 -10 1 6 0
 */

#include<stdio.h>

int main(){
    struct data{
        int xi;
        int zhi;
    }da[1000];
    int a,n,i=0,j;
    while(1){
        scanf("%d%d",&a,&n);
        if( n!=0 && a!=0 ){
            da[i].xi=a*n;
            da[i].zhi=n-1;
            i++;
        }
        if(getchar()=='\n') break;
    }
    for(j=0;j<i-1;j++) printf("%d %d ",da[j].xi,da[j].zhi);
    printf("%d %d\n",da[j].xi,da[j].zhi);
    return 0;
}
```



## 1011-1020

### PAT_1011A+B 和 C

```c
/*给定区间 [−231,231] 内的 3 个整数 A、B 和 C，请判断 A+B 是否大于 C。输入格式：
 输入第 1 行给出正整数 T (≤10)，是测试用例的个数。随后给出 T 组测试用例，每组占一行，顺序给出 A、B 和 C。整数间以空格分隔。
 输出格式：
 对每组测试用例，在一行中输出 Case #X: true 如果 A+B>C，否则输出 Case #X: false，其中 X 是测试用例的编号（从 1 开始）。
 输入样例：
 4
 1 2 3
 2 3 4
 2147483647 0 2147483646
 0 -2147483648 -2147483647
 输出样例：

 Case #1: false
 Case #2: true
 Case #3: true
 Case #4: false
 */

#include<stdio.h>

int main(){
    struct data{
        long A;
        long B;
        long C;
    }da[15];
    int n,i;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%ld%ld%ld",&da[i].A,&da[i].B,&da[i].C);
    }
    for(i=0;i<n;i++){
        if(da[i].A+da[i].B>da[i].C) printf("Case #%d: true\n",i+1);
        else printf("Case #%d: false\n",i+1);
    }
    return 0;
}
```



### PAT_1012数字分类

```c
/*
 给定一系列正整数，请按要求对数字进行分类，并输出以下 5 个数字：
 A1= 能被 5 整除的数字中所有偶数的和；
 A2= 将被 5 除后余 1 的数字按给出顺序进行交错求和，即计算 n1−n2+n3−n4⋯；
 A3= 被 5 除后余 2 的数字的个数；
 A4= 被 5 除后余 3 的数字的平均数，精确到小数点后 1 位；
 A5= 被 5 除后余 4 的数字中最大数字。
 输入格式：
 每个输入包含1个测试用例。每个测试用例先给出一个不超过1000的正整数N，随后给出N个不超过1000的待分类的正整数。数字间以空格分隔。
 输出格式：
 对给定的 N 个正整数，按题目要求计算 A1~A5并在一行中顺序输出。数字间以空格分隔，但行末不得有多余空格。
 若分类之后某一类不存在数字，则在相应位置输出 N。
 输入样例 1：
 13 1 2 3 4 5 6 7 8 9 10 20 16 18
 输出样例 1：
 30 11 2 9.7 9
 输入样例 2：
 8 1 2 4 5 6 7 9 16
 输出样例 2：
 N 11 2 N 9
 */

#include<stdio.h>

int main(){
    int a1=0,a2=0,a3=0,a4=0,a5=0,i=0,n,f=1,num_a4=0,flag_a2=0;
    int num[1500]={0};
    scanf("%d",&n);
    
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
        if(num[i]%10==0){a1=a1+num[i];}
        else if(num[i]%5==1){a2=a2+f*num[i];f*=-1;flag_a2++;}
        else if(num[i]%5==2){a3++;}
        else if(num[i]%5==3){num_a4++;a4=a4+num[i];}
        else if(num[i]%5==4){if(num[i]>a5) a5=num[i];}
    }
    
    if(a1==0) printf("N ");
    else printf("%d ",a1);
    if(flag_a2==0) printf("N ");
    else printf("%d ",a2);
    if(a3==0) printf("N ");
    else printf("%d ",a3);
    if(num_a4==0) printf("N ");
    else printf("%.1f ",1.0*a4/num_a4);
    if(a5==0) printf("N\n");
    else printf("%d\n",a5);

    return 0;
}
```



### PAT_1013数素数

```c
/*
 令 Pi表示第 i 个素数。现任给两个正整数 M≤N≤104，请输出 PM到 PN的所有素数。
 输入格式：
 输入在一行中给出 M 和 N，其间以空格分隔。
 输出格式：
 输出从 P M 到 P N
的所有素数，每 10 个数字占 1 行，其间以空格分隔，但行末不得有多余空格。
 输入样例：
 5 27
 输出样例：
 11 13 17 19 23 29 31 37 41 43
 47 53 59 61 67 71 73 79 83 89
 97 101 103
*/
/*
 5  4  3  2  1
 11 7  5  3  2
 */
#include<stdio.h>
#include<math.h>

int is_su(int x);

int main(){
    int m,n,i=3,t=2,j,su[10005]={0,2,0};
    int all,h,g;
    while(1){
        if(is_su(i)==0) su[t++]=i;
        if(t>10000) break;
        i++;
    }
    scanf("%d%d",&m,&n);
    
    all = n-m+1;
    h=all/10;
    g=all%10;
    for(i=0;i<h;i++){
        for(j=0;j<10-1;j++){
            printf("%d ",su[m++]);
        }
        printf("%d\n",su[m++]);
    }
    for(j=0;j<g-1;j++){
        printf("%d ",su[m++]);
    }
    if(g!=0) printf("%d\n",su[n]);
    return 0;
}

int is_su(int x){
    int i,flag=0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) flag++;
    }
    return flag;
}
```



### PAT_1014福尔摩斯的约会

```c
//星期只有七天，所以是A-G，范围不要错写成A-Z；

/*大侦探福尔摩斯接到一张奇怪的字条：
 我们约会吧！
 3485djDkxh4hhGE
 2984akDfkkkkggEdsb
 s&hgsfdk
 d&Hyscvnm
 大侦探很快就明白了，字条上奇怪的乱码实际上就是约会的时间星期四 14:04，因为前面两字符串中第 1 对相同的大写英文字母（大小写有区分）是第 4 个字母 D，代表星期四；第 2 对相同的字符是 E ，那是第 5 个英文字母，代表一天里的第 14 个钟头（于是一天的 0 点到 23 点由数字 0 到 9、以及大写字母 A 到 N 表示）；后面两字符串第 1 对相同的英文字母 s 出现在第 4 个位置（从 0 开始计数）上，代表第 4 分钟。现给定两对字符串，请帮助福尔摩斯解码得到约会的时间。
 输入格式：
 输入在 4 行中分别给出 4 个非空、不包含空格、且长度不超过 60 的字符串。
 输出格式：
 在一行中输出约会的时间，格式为 DAY HH:MM，其中 DAY 是某星期的 3 字符缩写，即 MON 表示星期一，TUE 表示星期二，WED 表示星期三，THU 表示星期四，FRI 表示星期五，SAT 表示星期六，SUN 表示星期日。题目输入保证每个测试存在唯一解。
 输入样例：
 3485djDkxh4hhGE
 2984akDfkkkkggEdsb
 s&hgsfdk
 d&Hyscvnm
 输出样例：
 THU 14:04
 */

#include<stdio.h>
#include<string.h>

int main(){
    char s1[100]={0},s2[100]={0},s3[100]={0},s4[100]={0},c[5]={0};
    int i,j,t=0,f,len,xingqi,hour;
    gets(s1);gets(s2);gets(s3);gets(s4);
    len=strlen(s1)>strlen(s2)? strlen(s2):strlen(s1);
    for(i=0;i<len;i++){
        if(s1[i]==s2[i]){
            if('A'<=s1[i]&&s1[i]<='G'&&t==0){c[t++]=s1[i];}
            else if('A'<=s1[i]&&s1[i]<='N'&&t==1){c[t++]=s1[i];}
            else if('0'<=s1[i]&&s1[i]<='9'&&t==1){c[t++]=s1[i];}
            }
        
    }
    len=strlen(s3)>strlen(s4)? strlen(s4):strlen(s3);
    for(i=0;i<len;i++){
        if(s3[i]==s4[i]){
            if(('A'<=s3[i]&&s3[i]<='Z')||('a'<=s3[i]&&s3[i]<='z')) break;
        }
    }
    f=i;
    
//    printf("%c %c %d\n",c[0],c[1],f);
    
    //shuchu
    xingqi=c[0]-'A'+1;
    switch(xingqi){
        case 1:printf("MON ");break;
        case 2:printf("TUE ");break;
        case 3:printf("WED ");break;
        case 4:printf("THU ");break;
        case 5:printf("FRI ");break;
        case 6:printf("SAT ");break;
        case 7:printf("SUN ");break;
    }
    hour = c[1]-'0';
    if(hour>9) {
        hour = c[1]-'A'+10;
        printf("%d:",hour);
    }
    else printf("0%d:",hour);
    
    if(f>9) printf("%d\n",f);
    else printf("0%d\n",f);
    return 0;
}
```



### PAT_1015德才论

```
用冒泡排序会有运行超时的问题，这个Qsort是快速排序，还未完全完成。
```

```c
/*宋代史学家司马光在《资治通鉴》中有一段著名的“德才论”：“是故才德全尽谓之圣人，才德兼亡谓之愚人，德胜才谓之君子，才胜德谓之小人。凡取人之术，苟不得圣人，君子而与之，与其得小人，不若得愚人。”现给出一批考生的德才分数，请根据司马光的理论给出录取排名。
 输入格式：
 输入第一行给出 3 个正整数，分别为：N（≤105），即考生总数；L（≥60），为录取最低分数线，即德分和才分均不低于 L 的考生才有资格被考虑录取；H（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到优先录取线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线 L 的考生也按总分排序，但排在第三类考生之后。
 随后 N 行，每行给出一位考生的信息，包括：准考证号 德分 才分，其中准考证号为 8 位整数，德才分为区间 [0, 100] 内的整数。数字间以空格分隔。
 输出格式：
 输出第一行首先给出达到最低分数线的考生人数 M，随后 M 行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。
 输入样例：
 14 60 80
 10000001 64 90
 10000002 90 60
 10000011 85 80
 10000003 85 80
 10000004 80 85
 10000005 82 77
 10000006 83 76
 10000007 90 78
 10000008 75 79
 10000009 59 90
 10000010 88 45
 10000012 80 100
 10000013 90 99
 10000014 66 60
 输出样例：
 12
 10000013 90 99
 10000012 80 100
 10000003 85 80
 10000011 85 80
 10000004 80 85
 10000007 90 78
 10000006 83 76
 10000005 82 77
 10000002 90 60
 10000014 66 60
 10000008 75 79
 10000001 64 90
 */
/*
 flag=0表示yi个没到最低线
 flag=1表示两个都过了>=最高要求是第一类考生 总分从高到低排序
 flag=2表示才分不到 但德分到优先录取线 属于“德胜才” 按总分排序
 flag=3表示德才分均低于H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者 按总分排序
 flag=4表示两个分达到最低线 L 的考生  也按总分排序
 */
#include<stdio.h>
#include<stdlib.h>
#define MAX 25000

typedef struct
{
    int id,vir,tal;
    int total;
}student;

void sort(student stu[],int N);
void Qsort(student stu[],int L,int R);

int main()
{
    int N,L,H;
    int i,A,B,C,D,sum=0;
    student s,*stu1,*stu2,*stu3,*stu4;
    stu1=(student*)malloc(MAX*sizeof(student));//开辟四个结构体数组，存储学生信息
    stu2=(student*)malloc(MAX*sizeof(student));
    stu3=(student*)malloc(MAX*sizeof(student));
    stu4=(student*)malloc(MAX*sizeof(student));
    A=B=C=D=0;
    scanf("%d %d %d",&N,&L,&H);//输入考生总数，德分和才分
    for(i=0;i<N;i++)
    {
        scanf("%d %d %d",&s.id,&s.vir,&s.tal);//单个输入学生信息
        s.total=s.vir+s.tal;//记录学生总分
        if(s.vir>=L&&s.tal>=L)//判断可录用的学生
        {
            sum++;//记录合格考生人数
            if(s.vir>=H&&s.tal>=H)        //"才德全尽"，存入第一个数组
                stu1[A++]=s;
            else if(s.vir>=H&&s.tal<H)    //"德胜才"，存入第二个数组
                stu2[B++]=s;
            else if(s.vir>=s.tal)        //"才德兼亡"尚有"德胜才"，存入第三个数组
                stu3[C++]=s;
            else                        //其他，存入第四个数组
                stu4[D++]=s;
        }//A，B，C，D分别记录了四种考生的人数
    }
    sort(stu1,A);//分别对四种考生进行排序
    sort(stu2,B);
    sort(stu3,C);
    sort(stu4,D);
//    Qsort(stu1, 1, A);
//    Qsort(stu2, 1, B);
//    Qsort(stu3, 1, C);
//    Qsort(stu4, 1, D);
    printf("%d\n",sum);
    for(i=0;i<A;i++)
        printf("%d %d %d\n",stu1[i].id,stu1[i].vir,stu1[i].tal);
    for(i=0;i<B;i++)
        printf("%d %d %d\n",stu2[i].id,stu2[i].vir,stu2[i].tal);
    for(i=0;i<C;i++)
        printf("%d %d %d\n",stu3[i].id,stu3[i].vir,stu3[i].tal);
    for(i=0;i<D;i++)
        printf("%d %d %d\n",stu4[i].id,stu4[i].vir,stu4[i].tal);
    return 0;
}

void sort(student stu[],int N)//冒泡排序
{
    student temp;
    for(int i=0;i<N;i++){
        for(int j=0;j<N-i-1;j++)
        {
            if(stu[j].total<stu[j+1].total)//总分排序
            {
                temp=stu[j];
                stu[j]=stu[j+1];
                stu[j+1]=temp;
            }
            else
                if(stu[j].total==stu[j+1].total)//前后考生总分相等
                {
                    if(stu[j].vir<stu[j+1].vir)//德分排序
                    {
                        temp=stu[j];
                        stu[j]=stu[j+1];
                        stu[j+1]=temp;
                    }
                    else
                        if(stu[j].vir==stu[j+1].vir&&stu[j].id>stu[j+1].id)//学号排序
                        {
                            temp=stu[j];
                            stu[j]=stu[j+1];
                            stu[j+1]=temp;
                        }
                }
        }
    }
}

void Qsort(student stu[],int L,int R){
    if(L>=R) return;
    student temp;
    int key,i=L,j=R;
    key=stu[L].total;
    while(i<j){
        while(i<j && stu[j].total>key) j--;
        while(i<j && stu[i].total<=key) i++;
        if(i<j){temp=stu[j];stu[j]=stu[i];stu[i]=temp;}
    }
    {temp=stu[L];stu[L]=stu[i];stu[i]=temp;}
    Qsort(stu, L, i-1);
    Qsort(stu, i+1, R);
}
```



### PAT_1016部分A+B

```c
/*正整数 A 的“DA（为 1 位整数）部分”定义为由 A 中所有 DA组成的新整数 PA。例如：给定 A=3862767，DA=6，则 A 的“6 部分”PA是 66，因为 A 中有 2 个 6。现给定 A、DA、B、DB，请编写程序计算 PA+PB。
 输入格式：
 输入在一行中依次给出 A、DA、B、DB，中间以空格分隔，其中 0<A,B<109。
 输出格式：
 在一行中输出 PA+PB的值。
 输入样例 1：
 3862767 6 13530293 3
 输出样例 1：
 399
 输入样例 2：
 3862767 1 13530293 8
 出样例 2：
 0
 */

#include<stdio.h>
#include<string.h>

int main(){
    char A[20]={0},B[20]={0},c;
    int Da,Db,Pa=0,Pb=0,i,num_a=0,num_b=0;
    scanf("%s %d %s %d",A,&Da,B,&Db);
    c='0'+Da;
    for(i=0;i<strlen(A);i++){
        if(A[i]==c) num_a++;
    }
    c='0'+Db;
    for(i=0;i<strlen(B);i++){
        if(B[i]==c) num_b++;
    }
    
    for(i=0;i<num_a;i++){
        Pa=Pa*10+Da;
    }
    for(i=0;i<num_b;i++){
        Pb=Pb*10+Db;
    }
    
    printf("%d\n",Pa+Pb);
    return 0;
}
```



### PAT_1017A除以B

```c
/*本题要求计算 A/B，其中 A 是不超过 1000 位的正整数，B 是 1 位正整数。你需要输出商数 Q 和余数 R，使得 A=B×Q+R 成立。
 输入格式：
 输入在一行中依次给出 A 和 B，中间以 1 空格分隔。
 输出格式：
 一行中依次输出 Q 和 R，中间以 1 空格分隔。
 输入样例：
 123456789050987654321 7
 输出样例：
 17636684150141093474 3
 */

#include<stdio.h>
#include<string.h>

int main(){
    char A[1005]={0};
    int B,R,Q[1005]={0};
    int i,t=0,y=0,x=0,xq=0;
    scanf("%s %d",A,&B);
    if(strlen(A)==1){
        x=A[0]-'0';
        printf("%d %d\n",x/B,x%B);
        return 0;
    }
    
    for(i=0;i<strlen(A);i++){
        x=A[i]-'0';
        if( y==0 && (x/B)>0 ){
            Q[t++]= x/B;
            y= x%B;
        }
        else if(y==0 && (x/B)==0){
            Q[t++]=0;
            i++;
            if (i==strlen(A)){
                y=A[i-1]-'0';
                break;
            }
            xq=x;
            x=A[i]-'0';
            Q[t++]= (xq*10+x)/B;
            y=(xq*10+x)%B;
        }
        else{
            Q[t++]= (y*10+x)/B;
            y=(y*10+x)%B;
        }
    }
    R=y;
    if(Q[0]==0 && t==1) printf("0");
    else if(Q[0]==0 && t>1)for(i=1;i<t;i++) printf("%d",Q[i]);
    else for(i=0;i<t;i++) printf("%d",Q[i]);
    
    printf(" %d\n",R);
    
    return 0;
}
```



### PAT_1018锤子剪刀布

```c
/*现给出两人的交锋记录，请统计双方的胜、平、负次数，并且给出双方分别出什么手势的胜算最大。
 输入格式：
 输入第1行给出正整数N（≤105），即双方交锋的次数。随后N行，每行给出一次交锋的信息，即甲、乙双方同时给出的的手势。C 代表“锤子”、J 代表“剪刀”、B 代表“布”，第 1 个字母代表甲方，第 2 个代表乙方，中间有 1 个空格。
 输格式：
 输出第1、2行分别给出甲、乙的胜、平、负次数，数字间以1空格分隔。第3行给出两个字母，分别代表甲、乙获胜次数最多的手势，中间有 1 个空格。如果解不唯一，则输出按字母序最小的解。
 输入样例：
10
C J
J B
C B
B B
B C
C C
C B
J B
B C
J J
 输出样例：
 5 3 2
 2 3 5
 B B
 */
#include<stdio.h>
#include<string.h>

int main(){
    int n,i,j,winj_c=0,winj_j=0,winj_b=0;
    int winy_c=0,winy_j=0,winy_b=0,ping=0;
    char s[5];
    scanf("%d",&n);
    for(i=0;i<=n;i++){
        gets(s);
        if(strcmp(s,"C J")==0) {winj_c++;}
        else if(strcmp(s,"C B")==0) {winy_b++;}
        else if(strcmp(s,"C C")==0) {ping++;}
        else if(strcmp(s,"J J")==0) {ping++;}
        else if(strcmp(s,"J B")==0) {winj_j++;}
        else if(strcmp(s,"J C")==0) {winy_c++;}
        else if(strcmp(s,"B J")==0) {winy_j++;}
        else if(strcmp(s,"B B")==0) {ping++;}
        else if(strcmp(s,"B C")==0) {winj_b++;}
    }
    printf("%d %d %d\n",winj_c+winj_b+winj_j,ping,winy_b+winy_c+winy_j);
    printf("%d %d %d\n",winy_b+winy_c+winy_j,ping,winj_c+winj_b+winj_j);
    
    if(winj_b>=winj_c && winj_b>=winj_j) printf("B ");
    else if(winj_c>winj_b && winj_c>=winj_j) printf("C ");
    else if(winj_j>winj_b && winj_j>winj_c) printf("J ");
    
    if(winy_b>=winy_c && winy_b>=winy_j) printf("B\n");
    else if(winy_c>winy_b && winy_c>=winy_j) printf("C\n");
    else if(winy_j>winy_b && winy_j>winy_c) printf("J\n");
    return 0;
}
```



### PAT_1019数字黑洞

```c
/*给定任一个各位数字不完全相同的 4 位正整数，如果我们先把 4 个数字按非递增排序，再按非递减排序，然后用第 1 个数字减第 2 个数字，将得到一个新的数字。一直重复这样做，我们很快会停在有“数字黑洞”之称的 6174，这个神奇的数字也叫 Kaprekar 常数。
 例如，我们从6767开始，将得到
 7766 - 6677 = 1089
 9810 - 0189 = 9621
 9621 - 1269 = 8352
 8532 - 2358 = 6174
 7641 - 1467 = 6174
 ... ...
 现给定任意 4 位正整数，请编写程序演示到达黑洞的过程。
 输入格式：
输入给出一个 (0,104) 区间内的正整数 N。
 输出格式：
 如果 N 的 4 位数字全相等，则在一行内输出 N - N = 0000；否则将计算的每一步在一行内输出，直到 6174 作为差出现，输出格式见样例。注意每个数字按 4 位数格式输出。
 输入样例 1：
 6767
 输出样例 1：
 7766 - 6677 = 1089
 9810 - 0189 = 9621
 9621 - 1269 = 8352
 8532 - 2358 = 6174
 输入样例 2：
 2222
 输出样例 2：
 2222 - 2222 = 0000*/

#include<stdio.h>

int change(int n,int a[],int b[]);
void Sort(int c[],int n);

int main(){
    int n,m,temp=0;
    int num[5]={0},num2[5]={0},t[5]={0};
    scanf("%d",&n);
    if(n%1111==0) {printf("%d - %d = 0000\n",n,n); return 0;}
    else if(n==0) {printf("0000 - 0000 = 0000\n"); return 0;}
    while(temp!=6174){
        m=change(n,num,num2);
        n=1000*num[0]+ 100*num[1]+ 10*num[2]+ num[3];
        temp=n-m;
        t[0]=temp/1000;
        t[1]=(temp/100)%10;
        t[2]=(temp/10)%10;
        t[3]=temp%10;
        printf("%d%d%d%d - %d%d%d%d = %d%d%d%d\n",num[0],num[1],num[2],num[3],num2[0],num2[1],num2[2],num2[3],t[0],t[1],t[2],t[3]);
        n=temp;
    }
    
    return 0;
}

int change(int n,int a[],int b[]){
    int n2;
    a[0]=n/1000;
    a[1]=(n/100)%10;
    a[2]=(n/10)%10;
    a[3]=n%10;
    Sort(a, 4);
    b[3]=a[0];b[2]=a[1];b[1]=a[2];b[0]=a[3];
    n2 = 1000*a[3]+ 100*a[2]+ 10*a[1]+ a[0];
    return n2;
}

void Sort(int c[],int n){
    int i,j,t;
    for(i=0;i<n;i++){
        for(j=0;j<n-i-1;j++){
            if(c[j]<c[j+1]){
                t=c[j];c[j]=c[j+1];c[j+1]=t;
            }
        }
    }
    
}
```



### PAT_1020月饼

```c
/*月饼是中国人在中秋佳节时吃的一种传统食品，不同地区有许多不同风味的月饼。现给定所有种类月饼的库存量、总售价、以及市场的最大需求量，请你计算可以获得的最大收益是多少。
 注意：销售时允许取出一部分库存。样例给出的情形是这样的：假如我们有 3 种月饼，其库存量分别为 18、15、10 万吨，总售价分别为 75、72、45 亿元。如果市场的最大需求量只有 20 万吨，那么我们最大收益策略应该是卖出全部 15 万吨第 2 种月饼、以及 5 万吨第 3 种月饼，获得 72 + 45/2 = 94.5（亿元）。
 输入格式：
 每个输入包含一个测试用例。每个测试用例先给出一个不超过 1000 的正整数 N 表示月饼的种类数、以及不超过 500（以万吨为单位）的正整数 D 表示市场最大需求量。随后一行给出 N 个正数表示每种月饼的库存量（以万吨为单位）；最后一行给出 N 个正数表示每种月饼的总售价（以亿元为单位）。数字间以空格分隔。
 输出格式：
 对每组测试用例，在一行中输出最大收益，以亿元为单位并精确到小数点后 2 位。
 输入样例：
 3 20
 18 15 10
 75 72 45
 输出样例：

 94.50
 */

#include<stdio.h>

struct yue{
    double t;
    double v;
    double dj;
};

void Qsort(struct yue a[],int L,int R);

int main(){
    int n,i;
    double d,all=0;
    scanf("%d %lf",&n,&d);
    struct yue bing[1005];
    for(i=0;i<n;i++){
        scanf("%lf",&bing[i].t);
    }
    for(i=0;i<n;i++){
        scanf("%lf",&bing[i].v);
    }
    for(i=0;i<n;i++){
        bing[i].dj=1.0*bing[i].v/bing[i].t;
    }
    
    Qsort(bing, 0, n-1);
    for(i=0;i<n;i++){
        if(d<=bing[i].t){all=all+d*bing[i].dj;break;}
        else{d=d-bing[i].t;all=all+bing[i].v;}
    }
    
    printf("%.2lf\n",all);
    return 0;
}

void Qsort(struct yue a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    struct yue temp;
    double key=a[L].dj;
    while(i<j){
        while(i<j && a[j].dj<key) j--;
        while(i<j && a[i].dj>=key)i++;
        if(i<j){temp=a[i];a[i]=a[j];a[j]=temp;}
    }
    temp=a[i];a[i]=a[L];a[L]=temp;
    Qsort(a, L, i-1);
    Qsort(a, i+1, R);
}
```



## 1021-1030

### PAT_1021个位数统计

```c
/*
 给定一个 k 位整数 N
 请编写程序统计每种不同的个位数字出现的次数。例如：给定 N=100311，则有 2 个 0，3 个 1，和 1 个 3。
 输入格式：
 每个输入包含 1 个测试用例，即一个不超过 1000 位的正整数 N。
 输出格式：
 对 N 中每一种不同的个位数字，以 D:M 的格式在一行中输出该位数字 D 及其在 N 中出现的次数 M。要求按 D 的升序输出。
 输入样例：
 100311
 输出样例：
 0:2
 1:3
 3:1
 */

#include<stdio.h>
#include<string.h>

int main(){
    char num[1005],c;
    int n[10]={0},len,i,j;
    gets(num);
    len=strlen(num);
    for(i=0;i<len;i++)
    {
        for(j=0;j<=9;j++){
            c='0'+j;
            if(c==num[i]) n[j]++;
        }
    }
    for(i=0;i<=9;i++){
        if(n[i]>0) printf("%d:%d\n",i,n[i]);
    }
    
    return 0;
}
```



### PAT_1022D进制的A+B

```c
/*输入两个非负 10 进制整数 A 和 B (≤230−1)，输出 A+B 的 D (1<D≤10)进制数。
 输入格式：
 输入在一行中依次给出 3 个整数 A、B 和 D。
 输出格式：
 输出 A+B 的 D 进制数。
 输入样例：
 123 456 8
 输出样例：
 1103
 */
#include<stdio.h>

int main(){
    long a,b,c;
    int d,n[1000],i=0,t=0;
    scanf("%ld%ld%d",&a,&b,&d);
    if(d==10){printf("%ld\n",a+b); return 0;}
    c=a+b;
    while(c/d>0){
        n[t++]=c%d;
        c=c/d;
    }
    n[t]=c;
    for(i=t;i>=0;i--){
        printf("%d",n[i]);
    }
    printf("\n");
    return 0;
}
```



### PAT_1023组个最小数

```c
/*给定数字 0-9 各若干个。你可以以任意顺序排列这些数字，但必须全部使用。目标是使得最后得到的数尽可能小（注意 0 不能做首位）。例如：给定两个 0，两个 1，三个 5，一个 8，我们得到的最小的数就是 10015558。
 现给定数字，请编写程序输出能够组成的最小的数。
 输入格式：
 输入在一行中给出 10 个非负整数，顺序表示我们拥有数字 0、数字 1、……数字 9 的个数。整数间用一个空格分隔。10 个数字的总个数不超过 50，且至少拥有 1 个非 0 的数字。
 输出格式：
 在一行中输出能够组成的最小的数。
 输入样例：
 2 2 0 0 0 3 0 0 1 0
 输出样例：
 10015558
 */

#include<stdio.h>

int main(){
    int n[10]={0},i;
    for(i=0;i<=9;i++){
        scanf("%d",&n[i]);
    }
    for(i=1;i<=9;i++){
        if(n[i]>0){printf("%d",i);n[i]--;break;}
    }
    for(i=0;i<=9;i++){
        while(n[i]){printf("%d",i);n[i]--;}
    }
    printf("\n");
    return 0;
}
```



### PAT_1024科学计数法

```c
/*科学计数法是科学家用来表示很大或很小的数字的一种方便的方法，其满足正则表达式 [+-][1-9].[0-9]+E[+-][0-9]+，即数字的整数部分只有 1 位，小数部分至少有 1 位，该数字及其指数部分的正负号即使对正数也必定明确给出。
 现以科学计数法的格式给出实数 A，请编写程序按普通数字表示法输出 A，并保证所有有效位都被保留。
 输入格式：
 每个输入包含 1 个测试用例，即一个以科学计数法表示的实数 A。该数字的存储长度不超过 9999 字节，且其指数的绝对值不超过 9999。
出格式：
 对每个测试用例，在一行中按普通数字表示法输出 A，并保证所有有效位都被保留，包括末尾的 0。
 输入样例 1：
 +1.23400E-03
 输出样例 1：
 0.00123400
 输入样例 2：
 -1.2E+10
 输出样例 2：
 -12000000000
 */

#include<stdio.h>

int main(){
    char n1[10000]={0},n2[10000]={0};
    int i,t=0,u=0,y=0,tt;
    //两个while把数据存下来，两个字符串的长度分别的t-1和u-1
    while(1){
        scanf("%c",&n1[t++]);
        if(n1[t-1]=='E') break;
    }
    tt=t;
    while(1){
        scanf("%c",&n2[u++]);
        if(n2[u-1]=='\n')break;
    }
    //tt是前面半个字符串的长度，但是把最后的0不算
    for(i=t-2;i>=3;i--){
        if(n1[i]=='0') tt--;
        else break;
    }
    //y是10的y次方，比如乘以y个十，或除y个十
    for(i=1;i<u-1;i++){
        y=y*10+(n2[i]-'0');
    }
//    printf("y=%d\n",y);
//    printf("t=%d\n",t);
//    printf("tt=%d\n",tt);
    
    
    if(n2[0]=='-'){//直接在前面加零的情况
        if(n1[0]=='-') printf("-");
        printf("0.");
        for(i=1;i<y;i++) printf("0");
        printf("%c",n1[1]);
        for(i=3;i<t-1;i++) printf("%c",n1[i]);
    }
    else{
        if(n1[0]=='-') printf("-");
        printf("%c",n1[1]);
        if(y>=tt-4 && y>=t-4){
            for(i=3;i<tt-1;i++) printf("%c",n1[i]);
            for(i=0;i<(y-tt+4);i++) printf("0");
        }
        else if(y<t-4){//后面有0多，还得加小数点后面添0
            for(i=3;i<3+y;i++) printf("%c",n1[i]);
            printf(".");
            for(i=3+y;i<t-1;i++) printf("%c",n1[i]);
        }
        else{
            for(i=3;i<3+y;i++) printf("%c",n1[i]);
            printf(".");
            for(i=3+y;i<t-1;i++)printf("%c",n1[i]);
        }
        
    }
    printf("\n");
    return 0;
}
```



### PAT_1025反转链表

```
四、测试数据
输入样例1：
00100 6 4
00000 4 99999
00100 1 12309
68237 6 -1
33218 3 00000
99999 5 68237
12309 2 33218
输出样例1：
00000 4 33218
33218 3 12309
12309 2 00100
00100 1 99999
99999 5 68237
68237 6 -1
输入样例2：（当结点集合的开头和中间有无效结点时能否正确处理）（测试点6）
00001 6 3
00009 9 -1
00001 1 00002
00002 2 00003
00003 3 00004
00008 8 -1
00004 4 -1
输出样例2：
00003 3 00002
00002 2 00001
00001 1 00004
00004 4 -1
输入样例3：（当出现结点地址为空地址时无效结点时能否正确处理）
00001 5 3
-1 -1 -1
00001 1 00002
00002 2 00003
00003 3 00004
00004 4 -1
输出样例3：
（很多人说这种情况下-1为当前地址的元素不应该输出，并说这个是测试点6过不去的原因，但是我之前试了很多次，发现把这个改好还是过不了测试点6，最后没管这个，转而去实现样例2倒是能过去，所以至少到目前为止，样例3这种情况输出当前地址为-1的元素也没事，后面会不会加这种情况的测试数据就不知道了，不过反正也好改，你在接收数据的时候接收到当前地址为-1的元素时用后面元素将其覆盖就好，即在接收的循环里加这句if(link[i].cur[0]==‘-’){ n–;i–; }，我测试过了，也是正确的）
00003 3 00002
00002 2 00001
00001 1 00004
00004 4 -1
-1 -1 -1
输入样例4：（当出现无效结点时能否正确处理）
00001 5 3
00001 1 00002
00008 8 00009
00002 2 00003
00003 3 00004
00004 4 -1
输出样例4：
00003 3 00002
00002 2 00001
00001 1 00004
00004 4 -1
————————————————
版权声明：本文为CSDN博主「扶酒劝斜阳」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_59586512/article/details/127522788
```

```c
/*给定一个常数 K 以及一个单链表 L，请编写程序将 L 中每 K 个结点反转。例如：给定 L 为 1→2→3→4→5→6，K 为 3，则输出应该为 3→2→1→6→5→4；如果 K 为 4，则输出应该为 4→3→2→1→5→6，即最后不到 K 个元素不反转。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例第 1 行给出第 1 个结点的地址、结点总个数正整数 N (≤10
 5)、以及正整数 K (≤N)，即要求反转的子链结点的个数。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。
 接下来有 N 行，每行格式为：
 Address Data Next
 其中 Address 是结点地址，Data 是该结点保存的整数数据，Next 是下一结点的地址。
 输出格式：
 对每个测试用例，顺序输出反转后的链表，其上每个结点占一行，格式与输入相同。
 输入样例：       \输出样例:
 00100 6 4      \00000 4 33218
 00000 4 99999  \33218 3 12309
 00100 1 12309  \12309 2 00100
 68237 6 -1     \00100 1 99999
 33218 3 00000  \99999 5 68237
 99999 5 68237  \68237 6 -1
 12309 2 33218  \
*/
#include<stdio.h>
#include<string.h>

struct add{
    char address[6];
    int data;
    char next[6];
    int rank;
};

void Qsort(struct add b[],int L,int R);

int main(){
    int n,k;
    char dz[6];
    int i,t=0,b=0,flag=0,c=0;
    scanf("%s %d %d",dz,&n,&k);
    struct add a[n];
    for(i=0;i<n;i++){
        scanf("%s %d %s",a[i].address,&a[i].data,a[i].next);
    }
    for(i=0;i<n;i++){
        if(!strcmp("-1", a[i].next)){a[i].rank=200000;b++;}//有b个点的next是-1
        else a[i].rank=200001;
    }
    b=b-1;//在b个-1的点中，有b个是真没有用的
    while(t+b<n){
        for(i=0;i<n;i++){
            if(!strcmp(dz, a[i].address)){
                a[i].rank=t++;
                strcpy(dz,a[i].next);
                if(!strcmp("-1", a[i].next)){flag=1;break;}//如果找到了最后一个，就跳出来
            }
        }
        if(flag) break;
    }
//共n个数据，实际上有效的只有t个
//    printf("b=%d\nn=%d\nt=%d\n",b,n,t);
    
    Qsort(a,0,n-1);
//    for(i=0;i<n;i++){
//        printf("%s %d %s %d\n",a[i].address,a[i].data,a[i].next,a[i].rank);
//    }
    for(i=k-1;i>=0;i--) {a[i].rank=c++;}
    for(i=k;i<t;i++) {a[i].rank=c++;}
    Qsort(a,0,n-1);
    for(i=0;i<t-1;i++){
        strcpy(a[i].next,a[i+1].address);
    }
    strcpy(a[t-1].next,"-1");
    for(i=0;i<t;i++){
        printf("%s %d %s\n",a[i].address,a[i].data,a[i].next);
    }
        
    return 0;
}


void Qsort(struct add b[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    struct add temp;
    int key=b[L].rank;
    while(i<j){
        while(i<j && b[j].rank>key) j--;
        while(i<j && b[i].rank<=key)i++;
        if(i<j){temp=b[i];b[i]=b[j];b[j]=temp;}
    }
    temp=b[i];b[i]=b[L];b[L]=temp;
    Qsort(b, L, i-1);
    Qsort(b, i+1, R);
}
```

```c
/*给定一个常数 K 以及一个单链表 L，请编写程序将 L 中每 K 个结点反转。例如：给定 L 为 1→2→3→4→5→6，K 为 3，则输出应该为 3→2→1→6→5→4；如果 K 为 4，则输出应该为 4→3→2→1→5→6，即最后不到 K 个元素不反转。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例第 1 行给出第 1 个结点的地址、结点总个数正整数 N (≤105  )、以及正整数 K (≤N)，即要求反转的子链结点的个数。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。
 接下来有 N 行，每行格式为：
 Address Data Next
 其中 Address 是结点地址，Data 是该结点保存的整数数据，Next 是下一结点的地址。
 输出格式：
 对每个测试用例，顺序输出反转后的链表，其上每个结点占一行，格式与输入相同。
 输入样例：
00100 6 4
00000 4 99999
00100 1 12309
68237 6 -1
33218 3 00000
99999 5 68237
12309 2 33218
 输出样例：
 00000 4 33218
 33218 3 12309
 12309 2 00100
 00100 1 99999
 99999 5 68237
 68237 6 -1
*/
/*
00100 6 3
00000 4 99999
00100 1 12309
68237 6 -1
33218 3 00000
99999 5 68237
12309 2 33218
 */

#include<stdio.h>

typedef struct Node{
    int addr;
    int data;
    int next;
}Node;

int main(){
    int firstaddr,n,k;
    int i,address,da,nex;
    scanf("%d%d%d",&firstaddr,&n,&k);
    Node nodeScanf[100005];
    Node node1[n];Node node2[n];
    for(i=0;i<n;i++){
        scanf("%d%d%d",&address,&da,&nex);
        nodeScanf[address].addr=address;
        nodeScanf[address].data=da;
        nodeScanf[address].next=nex;
    }
    
    node1[0].addr=firstaddr;
    node1[0].data=nodeScanf[firstaddr].data;
    node1[0].next=nodeScanf[firstaddr].next;
    address=node1[0].next;
    
    for(i=1;i<n;i++){
        if(node1[i-1].next!=-1)
        {
            node1[i].addr=address;
            node1[i].data=nodeScanf[address].data;
            node1[i].next=nodeScanf[address].next;
            address=node1[i].next;
        }
        else break;
    }
    n=i;//一个个找下去，直到找到-1，说明已经到头了，实际上能用的个数只有i个
//    for(i=0;i<n;i++){
//        printf("%05d %d %05d\n",node1[i].addr,node1[i].data,node1[i].next);
//    }
    int index=0,zu=n/k;
    for(int j=0;j<zu;j++){
        for(i=k-1;i>=0;i--){
            node2[index++]=node1[j*k+i];
        }
    }
    for(i=k*zu;i<n;i++){
        node2[index++]=node1[i];
    }
    
    
    node2[n-1].next=-1;
    for(i=0;i<n-1;i++){
        node2[i].next=node2[i+1].addr;
        printf("%05d %d %05d\n",node2[i].addr,node2[i].data,node2[i].next);
    }
    printf("%05d %d %d\n",node2[i].addr,node2[i].data,node2[i].next);
    return 0;
}
```



### PAT_1026程序运行时间

```c
/*要获得一个 C 语言程序的运行时间，常用的方法是调用头文件 time.h，其中提供了 clock() 函数，可以捕捉从程序开始运行到 clock() 被调用时所耗费的时间。这个时间单位是 clock tick，即“时钟打点”。同时还有一个常数 CLK_TCK，给出了机器时钟每秒所走的时钟打点数。于是为了获得一个函数 f 的运行时间，我们只要在调用 f 之前先调用 clock()，获得一个时钟打点数 C1；在 f 执行完成后再调用 clock()，获得另一个时钟打点数 C2；两次获得的时钟打点数之差 (C2-C1) 就是 f 运行所消耗的时钟打点数，再除以常数 CLK_TCK，就得到了以秒为单位的运行时间。
 这里不妨简单假设常数 CLK_TCK 为 100。现给定被测函数前后两次获得的时钟打点数，请你给出被测函数运行的时间。
 输入格式：
 输入在一行中顺序给出 2 个整数 C1 和 C2。注意两次获得的时钟打点数肯定不相同，即 C1 < C2，并且取值在 [0,107]。
 输出格式：
 在一行中输出被测函数运行的时间。运行时间必须按照 hh:mm:ss（即2位的 时:分:秒）格式输出；不足 1 秒的时间四舍五入到秒。
 输入样例：
 123 4577973
 输出样例：
 12:42:59
 */

#include<stdio.h>
#define CLK_TCK 100

int main(){
    long c1,c2,c,flag=0;
    int h,m,s;
    scanf("%ld %ld",&c1,&c2);
    c=c2-c1;
//    printf("%ld\n",c);
    if(c%CLK_TCK>=50) flag=1;
    c=c/100;
    if(flag) c++;
    s=c%60;
    c=c/60;
    m=c%60;
    h=c/60;
    printf("%02d:%02d:%02d\n",h,m,s);
    
    return 0;
}
```



### PAT_1027打印沙漏

```c
/*
 本题要求你写个程序把给定的符号打印成沙漏的形状。例如给定17个“*”，要求按下列格式打印
 *****
  ***
   *
  ***
 *****
 所谓“沙漏形状”，是指每行输出奇数个符号；各行符号中心对齐；相邻两行符号数差2；符号数先从大到小顺序递减到1，再从小到大顺序递增；首尾符号数相等。
 给定任意N个符号，不一定能正好组成一个沙漏。要求打印出的沙漏能用掉尽可能多的符号。
 输入格式:
 输入在一行给出1个正整数N（≤1000）和一个符号，中间以空格分隔。
 输出格式:
 首先打印出由给定符号组成的最大的沙漏形状，最后在一行中输出剩下没用掉的符号数。
 输入样例:
 19 *
 输出样例:

 *****
  ***
   *
  ***
 *****
 2
 */

#include<stdio.h>
#include<math.h>

int main(){
    int n,m,h,i,j;
    char c;
    scanf("%d %c",&n,&c);
    m=(n+1)/2;
    h=sqrt(m);
    m=0;
    for(i=h;i>=1;i--){
        for(j=0;j<(h-i);j++) printf(" ");
        for(j=0;j<2*i-1;j++){
            printf("%c",c);m++;
        }
        printf("\n");
    }
    for(i=2;i<=h;i++){
        for(j=0;j<(h-i);j++) printf(" ");
        for(j=0;j<2*i-1;j++){
            printf("%c",c);m++;
        }
        printf("\n");
    }
    printf("%d\n",n-m);
    
    return 0;
}
```



### PAT_1028人口普查

```c
/*
 某城镇进行人口普查，得到了全体居民的生日。现请你写个程序，找出镇上最年长和最年轻的人。
 这里确保每个输入的日期都是合法的，但不一定是合理的——假设已知镇上没有超过 200 岁的老人，而今天是 2014 年 9 月 6 日，所以超过 200 岁的生日和未出生的生日都是不合理的，应该被过滤掉。
 输入格式：
 输入在第一行给出正整数N，取值(0,105]；随后N行，每行给出1个人的姓名（由不超过5个英文字母组成的字符串）、以及按 yyyy/mm/dd（即年/月/日）格式给出的生日。题目保证最年长和最年轻的人没有并列。
 输出格式：
 在一行中顺序输出有效生日的个数、最年长人和最年轻人的姓名，其间以空格分隔。
 输入样例：
 5
 John 2001/05/12
 Tom 1814/09/06
 Ann 2121/01/30
 James 1814/09/05
 Steve 1967/11/20
 输出样例
 3 Tom John
 */

#include<stdio.h>

struct man{
    char name[7];
    int y,m,d;
    int isLive;
};

int IsLived(int yy,int mm,int dd);

int main(){
    int n,i,man_live=0,max=0,min=0;
    scanf("%d",&n);
    struct man a[n];
    for(i=0;i<n;i++){
        scanf("%s %d/%d/%d",a[i].name,&a[i].y,&a[i].m,&a[i].d);
    }
    for(i=0;i<n;i++){
        a[i].isLive=IsLived(a[i].y,a[i].m,a[i].d);
//        printf("%s islive=%d\n",a[i].name,a[i].isLive);
        if(a[i].isLive==1) {
        man_live++;
        }
    }
    for(i=0;i<n;i++){if(a[i].isLive==1) {max=i;min=i;break;}}
    
    for(i=0;i<n;i++){
        if(a[i].isLive==1){
            if(a[i].y<a[max].y) {max=i;}
            else if(a[i].y==a[max].y && a[i].m<a[max].m) {max=i;}
            else if(a[i].y==a[max].y && a[i].m==a[max].m && a[i].d<a[max].d) {max=i;}
                
            else if(a[i].y>a[min].y) {min=i;}
            else if(a[i].y==a[min].y && a[i].m>a[min].m) {min=i;}
            else if(a[i].y==a[min].y && a[i].m==a[min].m && a[i].d>a[min].d) {min=i;}
        }
    }
    
    printf("%d",man_live);
    if(man_live>0){
        printf(" %s ",a[max].name);
        printf("%s\n",a[min].name);
    }
    else printf("\n");
    return 0;
}

int IsLived(int yy,int mm,int dd){
    if(yy>2014) return 0;
    else if(yy==2014 && mm>9) return 0;
    else if(yy==2014 && mm==9 && dd>6) return 0;
    else if(yy<2014-200) return -1;
    else if(yy==2014-200 && mm<9) return -1;
    else if(yy==2014-200 && mm==9 && dd<6) return -1;
    else return 1;
}
```



### PAT_1029旧键盘

```c
/*旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及实际被输入的文字，请你列出肯定坏掉的那些键。
 输入格式：
 输入在 2 行中分别给出应该输入的文字、以及实际被输入的文字。每段文字是不超过 80 个字符的串，由字母 A-Z（包括大、小写）、数字 0-9、以及下划线 _（代表空格）组成。题目保证 2 个字符串均非空。
 输出格式：
 按照发现顺序，在一行中输出坏掉的键。其中英文字母只输出大写，每个坏键只输出一次。题目保证至少有 1 个坏键。
 输入样例：
 7_This_is_a_test
 _hs_s_a_es
 输出样例：
 7TI
 */
//注释掉的while有问题，可能会把正常的键也放进去。
#include<stdio.h>
#include<string.h>


int main(){
    char s1[100]={0},s2[100]={0},s3[100]={0},s4[100]={0};
    int i=0,j=0,t=0,flag=0;
    gets(s1);gets(s2);
//    while(i<strlen(s1) && j<strlen(s2)){
//        if(s1[i]==s2[j]){
//            i++;j++;
//        }
//        else{
//            if('a'<=s1[i]&&s1[i]<='z') s1[i]=s1[i]+'A'-'a';
//            s3[t++]=s1[i];
//            i++;
//        }
//    }
    for(i=0;i<strlen(s1);i++){
        flag=0;
        for(j=0;j<strlen(s2);j++){
            if(s1[i]==s2[j]) {flag=1;break;}
        }
        if(flag) continue;
        else{
            if('a'<=s1[i]&&s1[i]<='z') s1[i]=s1[i]+'A'-'a';
            s3[t++]=s1[i];
        }
    }
    t=0;
//    puts(s3);
    for(i=0;i<strlen(s3);i++){
        flag=1;
        for(j=0;j<i;j++){
            if(s3[j]==s3[i]) {flag=0;break;}
        }
        if(flag) s4[t++]=s3[i];
    }
    if(strlen(s4)>0) puts(s4);
    return 0;
}
```



### PAT_1030完美数列

```
p 是 double 的
因为count是完美数列的最大长度，如果当i向后移动，则没必要再判断小于count长度的数列是否符合完美数列，即j=i+count。
```

```c
/*给定一个正整数数列，和正整数 p，设这个数列中的最大值是 M，最小值是 m，如果 M≤mp，则称这个数列是完美数列。
 现在给定参数 p 和一些正整数，请你从中选择尽可能多的数构成一个完美数列。
 输入格式：
 输入第一行给出两个正整数 N 和 p，其中 N（≤10 5）是输入的正整数的个数，p（≤109  ）是给定的参数。第二行给出 N 个正整数，每个数不超过 10 9  。
 输出格式：
 在一行中输出最多可以选择多少个数可以用它们组成一个完美数列。
 输入样例：
 10 8
 2 3 20 4 5 1 6 7 8 9
 输出样例：
 8
*/

#include<stdio.h>

void Qsort(int num[],int L,int R);

int main(){
    int n,i,j,count=0;
    double p;
    scanf("%d%lf",&n,&p);
    int num[100000]={0};
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
    }
    Qsort(num, 0, n-1);
//    for(i=0;i<n;i++){
//        printf("%d ",num[i]);
//    }
    for(i=0;i<n;i++)
        for(j=i+count;j<n;j++)
        {
            if(num[j]>num[i]*p)
                break;
            count++;
        }
    printf("%d\n",count);
    
    return 0;
}

void Qsort(int a[],int L,int R)//快速排序
{
    if(L>=R) return;
    int i=L;
    int j=R;
    int temp;
    int key=a[L];
    while(i<j){
        while(i<j && a[j]>key) j--;
        while(i<j && a[i]<=key)i++;
        if(i<j){temp = a[i]; a[i]=a[j];a[j]=temp;}
    }
    temp = a[i]; a[i]=a[L];a[L]=temp;
    Qsort(a,L,i-1);
    Qsort(a,i+1,R);
}
```



## 1031-1040

### PAT_1031查验身份证

```c
/*一个合法的身份证号码由17位地区、日期编号和顺序编号加1位校验码组成。校验码的计算规则如下：
 首先对前17位数字加权求和，权重分配为：{7，9，10，5，8，4，2，1，6，3，7，9，10，5，8，4，2}；然后将计算的和对11取模得到值Z；最后按照以下关系对应Z值与校验码M的值：
 Z：0 1 2 3 4 5 6 7 8 9 10
 M：1 0 X 9 8 7 6 5 4 3 2
 现在给定一些身份证号码，请你验证校验码的有效性，并输出有问题的号码。
 输入格式：
 输入第一行给出正整数N（≤100）是输入的身份证号码的个数。随后N行，每行给出1个18位身份证号码。
 输出格式：
 按照输入的顺序每行输出1个有问题的身份证号码。这里并不检验前17位是否合理，只检查前17位是否全为数字且最后1位校验码计算准确。如果所有号码都正常，则输出All passed。
 输入样例1：
 4
 320124198808240056
 12010X198901011234
 110108196711301866
 37070419881216001X
 输出样例1：
 12010X198901011234
 110108196711301866
 37070419881216001X
 输入样例2：
 2
 320124198808240056
 110108196711301862
 输出样例2：
 All passed
 */

#include<stdio.h>

int main(){
    int p[17]={7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
    int n,i,j,count=0,sum,flag[10000]={0},z;
    char m[]={'1','0' ,'X' ,'9' ,'8' ,'7','6' ,'5' ,'4' ,'3' ,'2'};
    scanf("%d",&n);
    char id[10000][19]={0};
    for(i=0;i<n;i++){
        scanf("%s",id[i]);
    }
    for(i=0;i<n;i++){
        sum=0;
        for(j=0;j<17;j++){
            sum=sum+(id[i][j]-'0')*p[j];
        }
        z=sum%11;
        if(m[z]==id[i][17]) {flag[i]=1;count++;}
        
    }
    if(count==n) printf("All passed\n");
    else {
        for(i=0;i<n;i++){
            if(flag[i]==0) printf("%s\n",id[i]);
        }
    }
    return 0;
}
```



### PAT_1032挖掘机技术哪家强

```c
/*为了用事实说明挖掘机技术到底哪家强，PAT 组织了一场挖掘机技能大赛。现请你根据比赛结果统计出技术最强的那个学校。
 输入格式：
 输入在第 1 行给出不超过 105
   的正整数 N，即参赛人数。随后 N 行，每行给出一位参赛者的信息和成绩，包括其所代表的学校的编号（从 1 开始连续编号）、及其比赛成绩（百分制），中间以空格分隔。
 输出格式：
 在一行中给出总得分最高的学校的编号、及其总分，中间以空格分隔。题目保证答案唯一，没有并列。
 输入样例：
 6
 3 65
 2 80
 1 100
 2 70
 3 40
 3 0
 输出样例：
 2 150
 */

#include<stdio.h>

int main(){
    int i,n,a,b,max;
    int grade[100001];
    scanf("%d",&n);
    for(i=0;i<=n;i++) grade[i]=0;
    for(i=0;i<n;i++){
        scanf("%d%d",&a,&b);
        grade[a]+=b;
    }
    max=0;
    for(i=1;i<=n;i++){//注意这个for循环的开始和结束
        if(grade[i]>=grade[max]) max=i;
    }
    printf("%d %d\n",max,grade[max]);
    
    return 0;
}
```



### PAT_1033旧键盘打字

```c
//若出现“+”，则不能输出大写字母，但是不影响“+”本身的输出
//此题中，在for循环中用strlen会超时。

/*旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及坏掉的那些键，打出的结果文字会是怎样？
 输入格式：
 输入在2行中分别给出坏掉的那些键、以及应该输入的文字。其中对应英文字母的坏键以大写给出；每段文字是不超过105个字符的串。可用的字符包括[a-z,A-Z]、数字0-9、以及下划线_（代表空格）、,、.、-、+（代表上档键）。题目保证第 2 行输入的文字串非空。
 注意：如果上档键坏掉了，那么大写的英文字母无法被打出。
 输出格式：
 在一行中输出能够被打出的结果文字。如果没有一个字符能被打出，则输出空行。
 输入样例：
 7+IE.
 7_This_is_a_test.
 输出样例：
 _hs_s_a_tst
 */
//

#include<stdio.h>
#include<string.h>

int main(){
    char s1[200000],s2[200000];
    int i,flag_dx=0,j,FlagCanUse,len1,len2;
    gets(s1);
    gets(s2);
    len1=strlen(s1);
    len2=strlen(s2);
    for(i=0;i<len1;i++){
        if(s1[i]=='+'){flag_dx=1;break;}
    }
    for(i=0;i<len2;i++){
        FlagCanUse=1;//能打印出来
        for(j=0;j<strlen(s1);j++){
            if(s2[i]==s1[j]) {FlagCanUse=0;break;}
            else if('a'<=s2[i] && s2[i]<='z' && s2[i]==s1[j]+'a'-'A') {FlagCanUse=0;break;}
        }
        if(FlagCanUse){
            if(flag_dx && 'A'<=s2[i] && s2[i]<='Z') continue;
            else printf("%c",s2[i]);
        }
        if(s2[i]=='+') printf("+");
    }
    printf("\n");
    return 0;
}
```



PAT_1034有理数四则运算

```c
/*本题要求编写程序，计算 2 个有理数的和、差、积、商。
 输入格式：
 输入在一行中按照 a1/b1 a2/b2 的格式给出两个分数形式的有理数，其中分子和分母全是整型范围内的整数，负号只可能出现在分子前，分母不为 0。
 输出格式：
 分别在 4 行中按照 有理数1 运算符 有理数2 = 结果 的格式顺序输出 2 个有理数的和、差、积、商。注意输出的每个有理数必须是该有理数的最简形式 k a/b，其中 k 是整数部分，a/b 是最简分数部分；若为负数，则须加括号；若除法分母为 0，则输出 Inf。题目保证正确的输出中没有超过整型范围的整数。
 输入样例 1：
 2/3 -4/2
 输出样例 1：
2/3 + (-2) = (-1 1/3)
 2/3 - (-2) = 2 2/3
 2/3 * (-2) = (-1 1/3)
 2/3 / (-2) = (-1/3)
 输入样例 2：
 5/3 0/6
 输出样例 2：
 1 2/3 + 0 = 1 2/3
 1 2/3 - 0 = 1 2/3
 1 2/3 * 0 = 0
 1 2/3 / 0 = Inf
 */


#include<stdio.h>
#include<math.h>
#include<stdlib.h>

//辗转相除法 求最大公约数
long long int gcd(long long a, long long b){
    if(b==0) return a;  //可以用条件表达式表达 return b==0?a:gcd(b,a%b)
    return gcd(b,a%b);

}

void print(long long a, long long b){
    long long c = 0; //带分数前面的整数部分，默认是0
    if(a > 0){ //正数
        if(b == 1){ //形如3/1
            printf("%lld", a);
        }
        else if(a > b){ //形如5/3
            c = a / b;
            a -= b * c;
            printf("%lld %lld/%lld", c, a, b);
        }
        else{ //真分数 形如3/5
            printf("%lld/%lld", a, b);
        }
    }
    else if(a == 0){ //形如0/3
        printf("%c", '0');
    }
    else{ //负数
        if(b == 1){ //形如-3/1
            printf("(%lld)", a);
        }
        else if(-1 * a > b){ //形如-5/3
            c = a / b;
            a = (-1 * a) % b;
            printf("(%lld %lld/%lld)", c, a, b);
        }
        else{ //真分数
            printf("(%lld/%lld)", a, b);
        }
    }
}

void add(long long a1, long long b1, long long a2, long long b2){
    print(a1, b1);
    printf(" + ");
    print(a2, b2);
    printf(" = ");
    long long a3 = a1 * b2 + a2 * b1;
    long long b3 = b1 * b2;
    //化简到最简形式，非带分数形式
    long long gcd3 = llabs(gcd(a3, b3));
    a3 /= gcd3;
    b3 /= gcd3;
    print(a3, b3);
    printf("\n");
}

void subtract(long long a1, long long b1, long long a2, long long b2){
    print(a1, b1);
    printf(" - ");
    print(a2, b2);
    printf(" = ");
    long long a3 = a1 * b2 - a2 * b1;
    long long b3 = b1 * b2;
    //化简到最简形式，非带分数形式
    long long gcd3 = llabs(gcd(a3, b3));
    a3 /= gcd3;
    b3 /= gcd3;
    print(a3, b3);
    printf("\n");
}

void multiply(long long a1, long long b1, long long a2, long long b2){
    print(a1, b1);
    printf(" * ");
    print(a2, b2);
    printf(" = ");
    long long a3 = a1 * a2;
    long long b3 = b1 * b2;
    //化简到最简形式，非带分数形式
    long long gcd3 = llabs(gcd(a3, b3));
    a3 /= gcd3;
    b3 /= gcd3;
    print(a3, b3);
    printf("\n");
}

void divide(long long a1, long long b1, long long a2, long long b2){
    print(a1, b1);
    printf(" / ");
    print(a2, b2);
    printf(" = ");
    if(a2 == 0){
        printf("Inf");
    }
    else if(a2 < 0){
        long long a3 = -1 * a1 * b2;
        long long b3 = -1 * b1 * a2;
        //化简到最简形式，非带分数形式
        long long gcd3 = llabs(gcd(a3, b3));
        a3 /= gcd3;
        b3 /= gcd3;
        print(a3, b3);
    }
    else{
        long long a3 = a1 * b2;
        long long b3 = b1 * a2;
        //化简到最简形式，非带分数形式
        long long gcd3 = llabs(gcd(a3, b3));
        a3 /= gcd3;
        b3 /= gcd3;
        print(a3, b3);
    }
    printf("\n");
}

int main(){
    long long a1, b1, a2, b2;
    scanf("%lld/%lld %lld/%lld", &a1, &b1, &a2, &b2);
    //先化简到最简形式，非带分数形式
    long long gcd1 = llabs(gcd(a1, b1));//abs绝对值
    a1 /= gcd1;
    b1 /= gcd1;
    long long gcd2 = llabs(gcd(a2, b2));
    a2 /= gcd2;
    b2 /= gcd2;
    //统一用最简形式参与运算
    add(a1, b1, a2, b2);
    subtract(a1, b1, a2, b2);
    multiply(a1, b1, a2, b2);
    divide(a1, b1, a2, b2);
    return 0;
}
```



### PAT_1035插入与归并

```c
/*插入排序是迭代算法，逐一获得输入数据，逐步产生有序的输出序列。每步迭代中，算法从输入序列中取出一元素，将之插入有序序列中正确的位置。如此迭代直到全部元素有序。
 归并排序进行如下迭代操作：首先将原始序列看成N个只包含1个元素的有序子序列，然后每次迭代归并两个相邻的有序子序列，直到最后只剩下 1 个有序的序列。
 现给定原始序列和由某排序算法产生的中间序列，请你判断该算法究竟是哪种排序算法？
 输入格式：
 输入在第一行给出正整数 N (≤100)；随后一行给出原始序列的 N 个整数；最后一行给出由某排序算法产生的中间序列。这里假设排序的目标序列是升序。数字间以空格分隔。
 输出格式：
 首先在第 1 行中输出Insertion Sort表示插入排序、或Merge Sort表示归并排序；然后在第 2 行中输出用该排序算法再迭代一轮的结果序列。题目保证每组测试的结果是唯一的。数字间以空格分隔，且行首尾不得有多余空格。
 输入样例 1：
 10
 3 1 2 8 7 5 9 4 6 0
 1 2 3 7 8 5 9 4 6 0
 输出样例 1：
 Insertion Sort
 1 2 3 5 7 8 9 4 6 0
 输入样例 2：
 10
 3 1 2 8 7 5 9 4 0 6
 1 3 2 8 5 7 4 9 0 6
 输出样例 2：
 Merge Sort
 1 2 3 8 4 5 7 9 0 6
 */

#include<stdio.h>
#include <stdbool.h>

int num[110] = {0};
int goal[110] = {0};

void Qsort(int a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    int key=a[L],temp;
    while(i<j){
        while(i<j && a[j]>key) j--;
        while(i<j && a[i]<=key)i++;
        if(i<j){temp=a[i];a[i]=a[j];a[j]=temp;}
    }
    temp=a[i];a[i]=a[L];a[L]=temp;
    Qsort(a, L, i-1);
    Qsort(a, i+1, R);
}

void InsertSort(int N, int t){
    printf("Insertion Sort\n");
    Qsort(num, 0, t+1);
    for(int i=0;i<N;i++){
        printf("%d",num[i]);
        if(i<N-1) printf(" ");
    }
}

void MergeSort(int N){
    printf("Merge Sort\n");
    for(int len=2;len<N;len*=2){
        bool flag2 = true;
        for(int left=0;left<N;left+=len){
            int right = left+len;
            if(right>=N) right = N;     //控制右边界的范围
            Qsort(num, left, right-1);//每次排序序列的长度为len
            if(right==N) break;    //已经到达序列末端，不再排序
        }
        for(int i=0;i<N;i++){
            if(num[i]!=goal[i]){
                flag2 = false;    //表示当前len与输入得到的结果不一致，需要继续将len进行乘以2
                break;
            }
        }
        if(flag2){     //说明当前len，就与中间的序列吻合，此时输出下一次迭代的结果即可
            len *= 2;
            for(int left=0;left<N;left+=len){
                int right = left+len;
                if(right>=N) right = N;
                Qsort(num, left, right-1);
                if(right==N) break;
            }
            for(int i=0;i<N;i++){
                printf("%d",num[i]);
                if(i<N-1) printf(" ");
            }
            return ;
        }
    }
}
int main(){
    int N;
    scanf("%d",&N);
    for(int i=0;i<N;i++){
        scanf("%d",&num[i]);
    }
    for(int i=0;i<N;i++){
        scanf("%d",&goal[i]);
    }
    int t = 0;
    bool flag1 = false;
    for(int i=0;i<N-1;i++){    //找到第一个无序的数，若之后的数序列和初始相同，说明是插入排序
        if(goal[i]>goal[i+1]){
            t = i;
            break;
        }
    }
    for(int i=t+1;i<N;i++){
        if(goal[i]!=num[i]){
            flag1 = true;    //有序序列后的无序序列与初始不同，故不是插入排序
            break;
        }
    }
    if(!flag1)    InsertSort(N,t);
    else    MergeSort(N);
    return 0;
}
```



### PAT_1036跟奥巴马一起编程

```
有个四舍五入不错
```

```c
/*
 美国总统奥巴马不仅呼吁所有人都学习编程，甚至以身作则编写代码，成为美国历史上首位编写计算机代码的总统。2014 年底，为庆祝“计算机科学教育周”正式启动，奥巴马编写了很简单的计算机代码：在屏幕上画一个正方形。现在你也跟他一起画吧！
 输入格式：
 
 输入在一行中给出正方形边长 N（3≤N≤20）和组成正方形边的某种字符 C，间隔一个空格。
 输出格式：
 
 输出由给定字符 C 画出的正方形。但是注意到行间距比列间距大，所以为了让结果看上去更像正方形，我们输出的行数实际上是列数的 50%（四舍五入取整）。
 输入样例：
 
 10 a
 输出样例：

 aaaaaaaaaa
 a        a
 a        a
 a        a
 aaaaaaaaaa
 */

#include<stdio.h>

int main(){
    int n,h,i,j;
    char c;
    scanf("%d %c",&n,&c);
    h=(1.0*n/2+0.5);
    for(i=1;i<=h;i++){
        if(i==1||i==h){
            for(j=1;j<=n;j++) printf("%c",c);
        }
        else{
            printf("%c",c);
            for(j=2;j<=n-1;j++) printf(" ");
            printf("%c",c);
        }
        printf("\n");
    }
    
    return 0;
}
```



### PAT_1037在霍格沃茨找零钱

```c
/*如果你是哈利·波特迷，你会知道魔法世界有它自己的货币系统 —— 就如海格告诉哈利的：“十七个银西可(Sickle)兑一个加隆(Galleon)，二十九个纳特(Knut)兑一个西可，很容易。”现在，给定哈利应付的价钱 P 和他实付的钱 A，你的任务是写一个程序来计算他应该被找的零钱。
 输入格式：
 输入在 1 行中分别给出 P 和 A，格式为 Galleon.Sickle.Knut，其间用 1 个空格分隔。这里 Galleon 是 [0, 10
 7] 区间内的整数，Sickle 是 [0, 17) 区间内的整数，Knut 是 [0, 29) 区间内的整数。
 输出格式：
 在一行中用与输入同样的格式输出哈利应该被找的零钱。如果他没带够钱，那么输出的应该是负数。
 输入样例 1：
 10.16.27 14.1.28
 输出样例 1：
 3.2.1
 输入样例 2：
 14.1.28 10.16.27
 输出样例 2：
 -3.2.1
 */

#include<stdio.h>
#include<stdlib.h>
#include<math.h>

void print(long all);

int main(){
    int a1,b1,c1,a2,b2,c2;
    long all1=0,all2=0;
    scanf("%d.%d.%d %d.%d.%d",&a1,&b1,&c1,&a2,&b2,&c2);
    all1=a1;all1=all1*17+b1;all1=all1*29+c1;
    all2=a2;all2=all2*17+b2;all2=all2*29+c2;
    print(all2-all1);
    return 0;
}

void print(long all){
    int a,b,c,flag=1;
    if(all<0) {all=labs(all);flag=-1;}
    c=all%29;
    b=all/29;
    a=b/17;
    b=b%17;
    if(flag==-1) printf("-");
    printf("%d.%d.%d\n",a,b,c);
}
```



### PAT_1038统计同成绩学生

```c
/*本题要求读入 N 名学生的成绩，将获得某一给定分数的学生人数输出。
 输入格式：
 输入在第1行给出不超过105的正整数N，即学生总人数。随后一行给出N名学生的百分制整数成绩，中间以空格分隔。最后一行给出要查询的分数个数 K（不超过 N 的正整数），随后是 K 个分数，中间以空格分隔。
 输出格式：
 在一行中按查询顺序给出得分等于指定分数的学生人数，中间以空格分隔，但行末不得有多余空格。
 输样例：
 10
 60 75 90 55 75 99 82 90 75 50
 3 75 90 88
 输出样例：
 3 2 0
 */
//
//#include<stdio.h>
//
//int main(){
//    int i,j,n,k,num[100000],find[100000],count;
//    scanf("%d",&n);
//    for(i=0;i<n;i++){
//        scanf("%d",&num[i]);
//    }
//    scanf("%d",&k);
//    for(i=0;i<k;i++){
//        scanf("%d",&find[i]);
//    }
//    for(i=0;i<k-1;i++){
//        count=0;
//        for(j=0;j<n;j++){
//            if(num[j]==find[i]) count++;
//        }
//        printf("%d ",count);
//    }
//    count=0;
//    for(j=0;j<n;j++){
//        if(num[j]==find[i]) count++;
//    }
//    printf("%d\n",count);
//    return 0;
//}

#include<stdio.h>

int main(){
    int i,n,k,num[101],f;
    scanf("%d",&n);
    for(i=0;i<=100;i++) num[i]=0;
    for(i=0;i<n;i++){
        scanf("%d",&f);
        num[f]++;
    }
    scanf("%d",&k);
    for(i=0;i<k-1;i++){
        scanf("%d",&f);
        printf("%d ",num[f]);
    }
    scanf("%d",&f);
    printf("%d\n",num[f]);
    
    return 0;
}
```



### PAT_1039到底买不买

```c
/*
 小红想买些珠子做一串自己喜欢的珠串。卖珠子的摊主有很多串五颜六色的珠串，但是不肯把任何一串拆散了卖。于是小红要你帮忙判断一下，某串珠子里是否包含了全部自己想要的珠子？如果是，那么告诉她有多少多余的珠子；如果不是，那么告诉她缺了多少珠子。为方便起见，我们用[0-9]、[a-z][A-Z]范围内的字符来表示颜色。例如在图1中，第3串是小红想做的珠串；那么第1串可以买，因为包含了全部她想要的珠子，还多了8颗不需要的珠子；第2串不能买，因为没有黑色珠子，并且少了一颗红色的珠子。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例分别在 2 行中先后给出摊主的珠串和小红想做的珠串，两串都不超过 1000 个珠子。
 输出格式：
 如果可以买，则在一行中输出 Yes 以及有多少多余的珠子；如果不可以买，则在一行中输出 No 以及缺了多少珠子。其间以 1 个空格分隔。
 输入样例 1：
 ppRYYGrrYBR2258
 YrR8RrY
 输出样例 1：
 Yes 8
 输入样例 2：
 ppRYYGrrYB225
 YrR8RrY
 输出样例 2：
 No 2
 */

#include<stdio.h>
#include<string.h>

int main(){
    char s1[1005],s2[1005];
    int i,j,count=0,len1,len2;
    scanf("%s%s",s1,s2);
    len1=strlen(s1);len2=strlen(s2);
    for(j=0;j<len2;j++){
//        flag=0;
        for(i=0;i<len1;i++){
            if(s1[i]==s2[j]){
//                flag=1;
                count++;
                s1[i]='-';
                break;
            }
        }
    }
    if(count==len2){
        printf("Yes ");
        printf("%d\n",len1-len2);
    }
    else{
        printf("No ");
        printf("%d\n",len2-count);
    }
    
    return 0;
}
```



### PAT_1040有几个PAT

```
注意，方法a会运行超时，所以需要改变思路，从后面开始统计。
```

```
/*字符串 APPAPT 中包含了两个单词 PAT，其中第一个 PAT 是第 2 位(P)，第 4 位(A)，第 6 位(T)；第二个 PAT 是第 3 位(P)，第 4 位(A)，第 6 位(T)。
 现给定字符串，问一共可以形成多少个 PAT？
 输入格式：
 输入只有一行，包含一个字符串，长度不超过105，只包含 P、A、T 三种字母。
 输出格式：
 在一行中输出给定字符串中包含多少个 PAT。由于结果可能比较大，只输出对 1000000007 取余数的结果。
 输入样例：
 APPAPT
 输出样例：
 2*/

#include<stdio.h>
#include<string.h>

int a(){
    char s[1000005];
    int i,j,k,len;
    long count=0;
    scanf("%s",s);
    len=strlen(s);
    for(i=0;i<len;i++){
        if(s[i]=='P'){
            for(j=i+1;j<len;j++){
                if(s[j]=='A'){
                    for(k=j+1;k<len;k++){
                        if(s[k]=='T') {count++;}
                    }
                }
            }
        }
    }
    printf("%ld\n",count%1000000007);
    return 0;
}

int main(){
    char s[1000005];
    int i,j,k,len;
    long long sum=0,num_T=0,num_A=0;
    scanf("%s",s);
    len=strlen(s);
    for(i=len-1;i>=0;i--){
        if(s[i]=='T'){
            num_T++;
        }
        else if(s[i]=='A'){
            num_A=num_A+num_T;
        }
        else if(s[i]=='P'){
            sum=sum+num_A;
        }
    }
    printf("%lld\n",sum%1000000007);
    
}
```



## 1041-1050

### PAT_1041考试座位号

```c
/*
 每个 PAT 考生在参加考试时都会被分配两个座位号，一个是试机座位，一个是考试座位。正常情况下，考生在入场时先得到试机座位号码，入座进入试机状态后，系统会显示该考生的考试座位号码，考试时考生需要换到考试座位就座。但有些考生迟到了，试机已经结束，他们只能拿着领到的试机座位号码求助于你，从后台查出他们的考试座位号码。
 输入格式：
 输入第一行给出一个正整数 N（≤1000），随后 N 行，每行给出一个考生的信息：准考证号 试机座位号 考试座位号。其中准考证号由 16 位数字组成，座位从 1 到 N 编号。输入保证每个人的准考证号都不同，并且任何时候都不会把两个人分配到同一个座位上。
 考生信息之后，给出一个正整数 M（≤N），随后一行中给出 M 个待查询的试机座位号码，以空格分隔。
 输出格式：
 对应每个需要查询的试机座位号码，在一行中输出对应考生的准考证号和考试座位号码，中间用 1 个空格分隔。
 准考证号 试机座位号 考试座位号
 输入样例：
 4
 3310120150912233 2 4
 3310120150912119 4 1
 3310120150912126 1 3
 3310120150912002 3 2
 2
 3 4
 输出样例：
 3310120150912002 2
 3310120150912119 1
 */

#include<stdio.h>

struct kao{
    long long int id;
    int a,b;
};

void Qsort(struct kao a[],int L,int R);

int main(){
    int n,m,i,t;
    scanf("%d",&n);
    struct kao man[n];
    for(i=0;i<n;i++){
        scanf("%lld %d %d",&man[i].id,&man[i].a,&man[i].b);
    }
    scanf("%d",&m);
    Qsort(man, 0, n-1);
    for(i=0;i<m;i++){
        scanf("%d",&t);
        printf("%lld %d\n",man[t-1].id,man[t-1].b);
    }
    return 0;
}

void Qsort(struct kao a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    struct kao temp;
    int key=a[L].a;
    while(i<j){
        while(i<j && a[j].a>key) j--;
        while(i<j && a[i].a<=key)i++;
        if(i<j){temp=a[i];a[i]=a[j];a[j]=temp;}
    }
    temp=a[i];a[i]=a[L];a[L]=temp;
    Qsort(a, L, i-1);
    Qsort(a, i+1, R);
}
```



### PAT_1042字符统计

```c
/*请编写程序，找出一段给定文字中出现最频繁的那个英文字母。
 输入格式：
 输入在一行中给出一个长度不超过 1000 的字符串。字符串由 ASCII 码表中任意可见字符及空格组成，至少包含 1 个英文字母，以回车结束（回车不算在内）。
 输出格式：
 在一行中输出出现频率最高的那个英文字母及其出现次数，其间以空格分隔。如果有并列，则输出按字母序最小的那个字母。统计时不区分大小写，输出小写字母。
 输入样例：
 This is a simple TEST.  There ARE numbers and other symbols 1&2&3...........
 输出样例：
 e 7
 */

#include<stdio.h>
#include<string.h>

int main(){
    int i,len,num[27],n=0;
    char s[1005];
    gets(s);
    len=strlen(s);
    for(i=0;i<27;i++){
        num[i]=0;
    }
    for(i=0;i<len;i++){
        if('a'<=s[i] && s[i]<='z') {n=s[i]-'a';num[n]++;}
        else if('A'<=s[i] && s[i]<='Z') {n=s[i]-'A';num[n]++;}
    }
    for(i=26;i>=0;i--){//巧妙解决：如果有并列，则输出按字母序最小的那个字母。
        if(num[i]>=num[n]) n=i;
    }
    printf("%c %d\n",n+'a',num[n]);
    return 0;
}
```



### PAT_1043输出PATest

```c
/*给定一个长度不超过 104的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 PATestPATest.... 这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 PATest 的顺序打印，直到所有字符都被输出。
 输入格式：
 输入在一行中给出一个长度不超过 104的、仅由英文字母构成的非空字符串。
 输出格式：
 在一行中按题目要求输出排序后的字符串。题目保证输出非空。
 输入样例：
 redlesPayBestPATTopTeePHPereatitAPPT
 输出样例：
 PATestPATestPTetPTePePee
 */

#include<stdio.h>
#include<string.h>

int main(){
    int i,len,Pcount=0,Acount=0,Tcount=0,ecount=0,scount=0,tcount=0,flag;
    char s[10004];
    scanf("%s",s);
    len=strlen(s);
    for(i=0;i<len;i++){
        if(s[i]=='P') Pcount++;
        else if(s[i]=='A') Acount++;
        else if(s[i]=='T') Tcount++;
        else if(s[i]=='e') ecount++;
        else if(s[i]=='s') scount++;
        else if(s[i]=='t') tcount++;
    }
//    printf("P=%d A=%d T=%d e=%d s=%d t=%d\n",Pcount,Acount,Tcount,ecount,scount,tcount);
    flag=Pcount+Acount+Tcount+ecount+scount+tcount;
    while(flag>0){
        if(Pcount>0) {printf("P");Pcount--;flag--;}
        if(Acount>0) {printf("A");Acount--;flag--;}
        if(Tcount>0) {printf("T");Tcount--;flag--;}
        if(ecount>0) {printf("e");ecount--;flag--;}
        if(scount>0) {printf("s");scount--;flag--;}
        if(tcount>0) {printf("t");tcount--;flag--;}
    }
    
    return 0;
}
```



### PAT_1044火星数字（❌两个）

```c
/*
 火星人是以 13 进制计数的：
 地球人的 0 被火星人称为 tret。
 地球人数字 1 到 12 的火星文分别为：jan, feb, mar, apr, may, jun, jly, aug, sep, oct, nov, dec。
 火星人将进位以后的 12 个高位数字分别称为：tam, hel, maa, huh, tou, kes, hei, elo, syy, lok, mer, jou。
 例如地球人的数字 29 翻译成火星文就是 hel mar；而火星文 elo nov 对应地球数字 115。为了方便交流，请你编写程序实现地球和火星数字之间的互译。
 输入格式：
 输入第一行给出一个正整数 N（<100），随后 N 行，每行给出一个 [0, 169) 区间内的数字 —— 或者是地球文，或者是火星文。
 输出格式：
 对应输入的每一行，在一行中输出翻译后的另一种语言的数字。
 输入样例：
 4
 29
 5
 elo nov
 tam
 输出样例：
 hel mar
 may
 115
 13
 */

#include<stdio.h>
#include<string.h>

void dq_hx(char s[]);
void hx_dq(char s[]);
int cmp(char x[],char y[]);

char hx_d[13][5]={"tret","jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};
char hx_g[13][5]={"","tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};

int main(){
    int n,i;
    char s[10],num[5];
//    scanf("%d",&n);
    gets(num);
    if(strlen(num)==2) n=10*(num[0]-'0')+(num[1]-'0');
    else if(strlen(num)==1) n=(num[0]-'0');
    for(i=0;i<n;i++){
//        scanf("%s\n",s[i]);
        gets(s);
        if('0'<=s[0] && s[0]<='9') dq_hx(s);
        else hx_dq(s);
    }
    return 0;
}

void dq_hx(char s[]){
    int n_dq;
    if(strlen(s)==1) n_dq=s[0]-'0';
    else if(strlen(s)==2) n_dq=10*(s[0]-'0')+s[1]-'0';
    else if(strlen(s)==3) n_dq=100+10*(s[1]-'0')+s[2]-'0';
    if(n_dq<=12) printf("%s\n",hx_d[n_dq]);
    else if(n_dq%13==0) printf("%s\n",hx_g[n_dq/13]);
    else printf("%s %s\n",hx_g[n_dq/13],hx_d[n_dq%13]);
}

void hx_dq(char s[]){
    int hx2=0,hx1=0;
    char s2[5],s1[5];
    int i;
    if(strlen(s)<4){
        for(i=0;i<14;i++){
            if(cmp(s, hx_d[i])==1){hx1=i;}
        }
        for(i=0;i<14;i++){
            if(cmp(s, hx_g[i])==1){hx2=i;}
        }
    }
    else{
        for(i=0;i<3;i++) s2[i]=s[i];
        for(i=4;i<7;i++) s1[i-4]=s[i];
        s1[3]='\0';s2[3]='\0';
//        puts(s1);puts(s2);
        for(i=0;i<14;i++){
            if(cmp(s1, hx_d[i])==1){hx1=i;}
        }
        for(i=0;i<14;i++){
            if(cmp(s2, hx_g[i])==1){hx2=i;}
        }
    }
    printf("%d\n",hx2*13+hx1);
}

int cmp(char x[],char y[]){
    int i;
//    if (strlen(x)!=strlen(y)) return 0;
    for (i=0;i<strlen(x);i++){
        if (x[i]!=y[i]) return 0;
    }
    return 1;
}
```





### PAT_1045快速排序（超时）

```c
/*著名的快速排序算法里有一个经典的划分过程：我们通常采用某种方法取一个元素作为主元，通过交换，把比主元小的元素放到它的左边，比主元大的元素放到它的右边。 给定划分后的 N 个互不相同的正整数的排列，请问有多少个元素可能是划分前选取的主元？
 例如给定 N=5, 排列是1、3、2、4、5。则：
 1 的左边没有元素，右边的元素都比它大，所以它可能是主元；
 尽管 3 的左边元素都比它小，但其右边的 2 比它小，所以它不能是主元；
 尽管 2 的右边元素都比它大，但其左边的 3 比它大，所以它不能是主元；
 类似原因，4 和 5 都可能是主元。
 因此，有 3 个元素可能是主元。
 输入格式：
 输入在第 1 行中给出一个正整数 N（≤10 5）； 第 2 行是空格分隔的 N 个不同的正整数，每个数不超过 109
 输出格式：
 在第 1 行中输出有可能是主元的元素个数；在第 2 行中按递增顺序输出这些元素，其间以 1 个空格分隔，行首尾不得有多余空格。
 输入样例：
 5
 1 3 2 4 5
 输出样例：
 3
 1 4 5
 */

#include<stdio.h>

void Qsort(int a[],int L,int R);

int main(){
    int n,i,t=0;
    int num[100005],num_sort[100005],num_p[100005],max;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
        num_sort[i]=num[i];
    }
    Qsort(num_sort, 0, n-1);
    max = num[0];
    for(i=0;i<n;i++){
        if(num[i]>max) max=num[i];
        if(num[i]==num_sort[i] && max==num[i]) {num_p[t++]=num[i];}
    }
    printf("%d\n",t);
    if(t==0){printf("\n");return 0;}
    for(i=0;i<t-1;i++){
        printf("%d ",num_p[i]);
    }
    printf("%d\n",num_p[i]);
    
    return 0;
}

void Qsort(int a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    int temp,key=a[L];
    while(i<j){
        while(i<j && a[j]>key) j--;
        while(i<j && a[i]<=key)i++;
        if(i<j){temp=a[i];a[i]=a[j];a[j]=temp;}
    }
    temp=a[i];a[i]=a[L];a[L]=temp;
    Qsort(a, L, i-1);
    Qsort(a, i+1, R);
}
```



### PAT_1046划拳

```c
/*划拳是古老中国酒文化的一个有趣的组成部分。酒桌上两人划拳的方法为：每人口中喊出一个数字，同时用手比划出一个数字。如果谁比划出的数字正好等于两人喊出的数字之和，谁就赢了，输家罚一杯酒。两人同赢或两人同输则继续下一轮，直到唯一的赢家出现。
 下面给出甲、乙两人的划拳记录，请你统计他们最后分别喝了多少杯酒。
 输入格式：
 输入第一行先给出一个正整数 N（≤100），随后 N 行，每行给出一轮划拳的记录，格式为：
 甲喊 甲划 乙喊 乙划
 其中喊是喊出的数字，划是划出的数字，均为不超过 100 的正整数（两只手一起划）。
 输出格式：
 在一行中先后输出甲、乙两人喝酒的杯数，其间以一个空格分隔。
 输入样例：
 5
 8 10 9 12
 5 10 5 10
 3 8 5 12
 12 18 1 13
 4 16 12 15
 输出样例：
 1 2
 */
#include<stdio.h>

int main(){
    int i,n,jhan,jhua,yhan,yhua,jcup=0,ycup=0;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d%d%d%d",&jhua,&jhan,&yhua,&yhan);
        if(jhua+yhua == jhan && jhua+yhua == yhan) continue;
        else if(jhua+yhua == jhan) ycup++;
        else if(jhua+yhua == yhan) jcup++;
    }
    printf("%d %d\n",jcup,ycup);
    
    return 0;
}
```



### PAT_1047编程团体赛

```c
/*编程团体赛的规则为：每个参赛队由若干队员组成；所有队员独立比赛；参赛队的成绩为所有队员的成绩和；成绩最高的队获胜。
 现给定所有队员的比赛成绩，请你编写程序找出冠军队。
 输入格式：
 输入第一行给出一个正整数 N（≤104），即所有参赛队员总数。随后 N 行，每行给出一位队员的成绩，格式为：队伍编号-队员编号 成绩，其中队伍编号为 1 到 1000 的正整数，队员编号为 1 到 10 的正整数，成绩为 0 到 100 的整数。
 输出格式：
 在一行中输出冠军队的编号和总成绩，其间以一个空格分隔。注意：题目保证冠军队是唯一的。
 输入样例：
 6
 3-10 99
 11-5 87
 102-1 0
 102-3 100
 11-9 89
 3-2 61
 输出样例：
 11 176
*/

#include<stdio.h>

int main(){
    int i,n,grade[10004],id,f,a,max=0,max_id=-1;
    for(i=0;i<10004;i++) grade[i]=0;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d-%d %d",&id,&a,&f);
        grade[id]+=f;
    }
    for(i=0;i<10004;i++){
        if(grade[i]>max) {max=grade[i];max_id=i;}
    }
    printf("%d %d\n",max_id,max);
    return 0;
}
```



### PAT_1048数字加密❌

```c
/*本题要求实现一种数字加密方法。首先固定一个加密用正整数 A，对任一正整数 B，将其每 1 位数字与 A 的对应位置上的数字进行以下运算：对奇数位，对应位的数字相加后对 13 取余——这里用 J 代表 10、Q 代表 11、K 代表 12；对偶数位，用 B 的数字减去 A 的数字，若结果为负数，则再加 10。
 
 这里令个位为第 1 位。
 输入格式：
 输入在一行中依次给出 A 和 B，均为不超过 100 位的正整数，其间以空格分隔。
 输出格式：
 在一行中输出加密后的结果。
 输入样例：
 1234567 368782971
 输出样例：
 3695Q8118
 */

#include<stdio.h>
#include<string.h>

int main(){
    char s[300],a[105],b[105];
    int i,len_a,len_b,len,j=0,t;
    scanf("%s %s",a,b);
    len_a=strlen(a);
    len_b=strlen(b);
    len=len_a>len_b? len_a:len_b;
    if(len_a>len_b){
        for(i=len_b+len_a-len_b;i>=len_a-len_b;i--) b[i]=b[i-len_a+len_b];
        for(i=0;i<len_a-len_b;i++) b[i]='0';
    }
    else if(len_a<len_b){
        for(i=len_a+len_b-len_a;i>=len_b-len_a;i--) a[i]=a[i-len_b+len_a];
        for(i=0;i<len_b-len_a;i++) a[i]='0';
    }
//    puts(a);puts(b);
    for(i=0;i<len;i++){
        if(i%2==1){//ou
            t=b[i]-'0'-(a[i]-'0');
            if(t<0) t+=10;
            s[j++]=t+'0';
        }
        else if(i%2==0){//ji
            t=(b[i]-'0'+(a[i]-'0'))%13;
            if(t==10) s[j++]='J';
            else if(t==11) s[j++]='Q';
            else if(t==12) s[j++]='K';
            else s[j++]=t+'0';
        }
    }
    s[j] = '\0';
    printf("%s",s);
    return 0;
}
```



### PAT_1049数列的片段和

```c
/*给定一个正数数列，我们可以从中截取任意的连续的几个数，称为片段。例如，给定数列 { 0.1, 0.2, 0.3, 0.4 }，我们有 (0.1) (0.1, 0.2) (0.1, 0.2, 0.3) (0.1, 0.2, 0.3, 0.4) (0.2) (0.2, 0.3) (0.2, 0.3, 0.4) (0.3) (0.3, 0.4) (0.4) 这 10 个片段。
 给定正整数数列，求出全部片段包含的所有的数之和。如本例中 10 个片段总和是 0.1 + 0.3 + 0.6 + 1.0 + 0.2 + 0.5 + 0.9 + 0.3 + 0.7 + 0.4 = 5.0。
 输入格式：
 输入第一行给出一个不超过 105的正整数 N，表示数列中数的个数，第二行给出 N 个不超过 1.0 的正数，是数列中的数，其间以一个空格分隔。
 出格式：
 在一行中输出该序列所有片段包含的数之和，精确到小数点后 2 位。
 输入样例：
 4
 0.1 0.2 0.3 0.4
 输出样例：
 5.00
 */
#include <stdio.h>
 
int main()
{
    int i, N;
    long double sum = 0.0;    //改用long double提高精度
    double temp;
    
    scanf("%d", &N);
    for(i = 0; i < N; ++i){
        scanf("%lf", &temp);
        sum += (N-i)*temp*(1+i);
    }
    printf("%.2f", (double)sum);    //注意这里的输出
    return 0;
}
```



### PAT_1050螺旋矩阵

```c
/*本题要求将给定的 N 个正整数按非递增的顺序，填入“螺旋矩阵”。所谓“螺旋矩阵”，是指从左上角第 1 个格子开始，按顺时针螺旋方向填充。要求矩阵的规模为 m 行 n 列，满足条件：m×n 等于 N；m≥n；且 m−n 取所有可能值中的最小值。
 输入格式：
 输入在第 1 行中给出一个正整数 N，第 2 行给出 N 个待填充的正整数。所有数字不超过 104
  ，相邻数字以空格分隔。
 输出格式：
 输出螺旋矩阵。每行 n 个数字，共 m 行。相邻数字以 1 个空格分隔，行末不得有多余空格。
 输入样例：
 12
 37 76 20 98 76 42 53 95 60 81 58 93
 输出样例：
 98 95 93
 42 37 81
 53 20 76
 58 60 76
*/

#include<stdio.h>
#include<math.h>


int get_row(int N);
void Qsort(int a[],int L,int R);


int main(){
    int N,a[100005],r,c,circle,i,j,k=0;
    scanf("%d",&N);
    r = get_row(N);//行数
    c = N/r;//列数
    circle = c/2;
    int b[r][c];
    if (c%2==1) circle++;
    for (i=0;i<N;i++) scanf("%d",&a[i]);
    Qsort(a, 0, N-1);
    for (i=0;i<circle;i++)//圈数
        {
            for (j=i;j<(c-i) && k<N;j++)//上面的行，从左边到右边，列变行不变
                b[i][j] = a[k++];
            for (j=i+1;j<(r-i) && k<N;j++)//右边的列，从上面到下面，行变列不变
                b[j][c-1-i] = a[k++];
            for (j=c-2-i;j>=i && k<N;j--)//下面的行，从右边到左边，列变行不变
                b[r-1-i][j] = a[k++];
            for (j=r-2-i;j>i && k<N;j--)//左边的列，从下面到上面，行变列不变
                b[j][i] = a[k++];
        }
        for (i=0;i<r;i++)
        {
            for (j=0;j<c;j++)
            {
                if (j!=0)
                    printf(" ");
                printf("%d",b[i][j]);
            }
            printf("\n");
        }
    
    return 0;
}


int get_row(int N){
    int i;
    i = sqrt(N);
    if (N==(i*i)) return i;
    for (i=sqrt(N)+1;i<=N;i++)
    {
        if (N%i==0) return i;
    }
    return -1;
}

void Qsort(int a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    int key=a[L];
    int temp;
    while(i<j){
        while(i<j && a[j]<key) j--;
        while(i<j && a[i]>=key) i++;
        if(i<j){temp=a[i];a[i]=a[j];a[j]=temp;}
    }
    temp=a[i];a[i]=a[L];a[L]=temp;
    Qsort(a, L, i-1);
    Qsort(a, i+1, R);
}
```



## 1051-1060

### PAT_1051复数乘法

```c
/*复数可以写成 (A+Bi) 的常规形式，其中 A 是实部，B 是虚部，i 是虚数单位，满足 i2=−1；也可以写成极坐标下的指数形式 (R×e(Pi))，其中 R 是复数模，P 是辐角，i 是虚数单位，其等价于三角形式 R(cos(P)+isin(P))。
 现给定两个复数的 R 和 P，要求输出两数乘积的常规形式。
 输入格式：
 输入在一行中依次给出两个复数的 R1, P1, R2, P2，数字间以空格分隔。
 输出格式：
 在一行中按照 A+Bi 的格式输出两数乘积的常规形式，实部和虚部均保留 2 位小数。注意：如果 B 是负数，则应该写成 A-|B|i 的形式。
 输入样例：
 2.3 3.5 5.2 0.4
 输出样例：

 -8.68-8.23i
 */
//printf("%.2f")是保留两位小数，0.005就是0.01，0.0049就是0.00，这很正常
//但是负数就不行了，-0.005是-0.01，-0.0049是-0.00，按理来说不能有-0，就答案错误了，
//所以应该当实部和虚部的绝对值小于0.005时，直接赋值为0，就不会出现保留后出现-0的情况
//如果绝对值大于等于0.005，就不用管了，交给printf("%.2f")就行了
//float精度不够的，用double能解决。

#include<stdio.h>
#include<math.h>

int main(){
    double r1,r2,r,p1,p2,p,a,b;
    scanf("%lf%lf%lf%lf",&r1,&p1,&r2,&p2);
    r=r1*r2;
    p=p1+p2;
    a=r*cosf(p);
    b=r*sinf(p);
    if(fabs(a)<0.005) a=0;
    if(fabs(b)<0.005) b=0;
    if(b<0) printf("%.2f%.2fi\n",a,b);
    else printf("%.2f+%.2fi\n",a,b);
    
    return 0;
}
```



### PAT_1052卖个萌

```
这一题必须用string输入，用字符数组存储的话，就会出现无法识别的字符然后直接被识别为'\0' ， 然后就无法进行后续的处理了，至于小细节，有 \ 的输出，注意 用 \\ 进行转义，其他的倒没啥，还有，自己测试的时候，有的字符无法输出，那个位置显示为空是正常现象，保证所有的能显示的字符是正确的就行
当后续输入<=0也是are u kidding...
```

```c
/*萌萌哒表情符号通常由“手”、“眼”、“口”三个主要部分组成。简单起见，我们假设一个表情符号是按下列格式输出的：
 [左手]([左眼][口][右眼])[右手]
 现给出可选用的符号集合，请你按用户的要求输出表情。
 输入格式：
 输入首先在前三行顺序对应给出手、眼、口的可选符号集。每个符号括在一对方括号 []内。题目保证每个集合都至少有一个符号，并不超过 10 个符号；每个符号包含 1 到 4 个非空字符。
 之后一行给出一个正整数 K，为用户请求的个数。随后 K 行，每行给出一个用户的符号选择，顺序为左手、左眼、口、右眼、右手——这里只给出符号在相应集合中的序号（从 1 开始），数字间以空格分隔。
 输出格式：
 对每个用户请求，在一行中输出生成的表情。若用户选择的序号不存在，则输出 Are you kidding me? @\/@。
 输入样例：
 [╮][╭][o][~\][/~]  [<][>]
  [╯][╰][^][-][=][>][<][@][⊙]
 [Д][▽][_][ε][^]  ...
 4
 1 1 2 2 2
 6 8 1 5 5
 3 3 4 3 3
 2 10 3 9 3
 输出样例：
 ╮(╯▽╰)╭
 <(@Д=)/~
 o(^ε^)o
 Are you kidding me? @\/@
 */

#include<stdio.h>
#include<string.h>

int main(){
    char s1[100],s2[100],s3[100];
    char shou[15][10],yan[15][10],kou[15][10];
    int n,i,t=-1,len_shou=0,len_yan=0,len_kou=0;
    int a,b,c,d,e;
    gets(s1);gets(s2);gets(s3);
    
    for(i=0;i<strlen(s1);i++){
        if(s1[i]=='[') t=0;
        else if(s1[i]==']') {shou[len_shou][t]='\0';len_shou++;t=-1;}
        else{
            if(t>-1) shou[len_shou][t++]=s1[i];
        }
    }
    
    for(i=0;i<strlen(s2);i++){
        if(s2[i]=='[') t=0;
        else if(s2[i]==']') {yan[len_yan][t]='\0';len_yan++;t=-1;}
        else{
            if(t>-1) yan[len_yan][t++]=s2[i];
        }
    }
    for(i=0;i<strlen(s3);i++){
        if(s3[i]=='[') t=0;
        else if(s3[i]==']') {kou[len_kou][t]='\0';len_kou++;t=-1;}
        else{
            if(t>-1) kou[len_kou][t++]=s3[i];
        }
    }
    
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d%d%d%d%d",&a,&b,&c,&d,&e);
        if(a>len_shou||b>len_yan||c>len_kou||d>len_yan||e>len_shou||a<=0||b<=0||c<=0||d<=0||e<=0)
            printf("Are you kidding me? @\\/@\n");
        else{
            printf("%s(%s%s%s)%s\n",shou[a-1],yan[b-1],kou[c-1],yan[d-1],shou[e-1]);
        }
    }
    return 0;
}
```



### PAT_1053住房空置率

```c
/*在不打扰居民的前提下，统计住房空置率的一种方法是根据每户用电量的连续变化规律进行判断。判断方法如下：
 在观察期内，若存在超过一半的日子用电量低于某给定的阈值 e，则该住房为“可能空置”；
 若观察期超过某给定阈值 D 天，且满足上一个条件，则该住房为“空置”。
 现给定某居民区的住户用电量数据，请你统计“可能空置”的比率和“空置”比率，即以上两种状态的住房占居民区住房总套数的百分比。
 输入格式：
 输入第一行给出正整数 N（≤1000），为居民区住房总套数；正实数 e，即低电量阈值；正整数 D，即观察期阈值。随后 N 行，每行按以下格式给出一套住房的用电量数据 K E1E2 ... EK
 其中 K 为观察的天数，E i为第 i 天的用电量。
 输出格式：
 在一行中输出“可能空置”的比率和“空置”比率的百分比值，其间以一个空格分隔，保留小数点后 1 位。
 输入样例：
 5 0.5 10
 6 0.3 0.4 0.5 0.2 0.8 0.6
 10 0.0 0.1 0.2 0.3 0.0 0.8 0.6 0.7 0.0 0.5
 5 0.4 0.3 0.5 0.1 0.7
 11 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1 0.1
 11 2 2 2 1 1 0.1 1 0.1 0.1 0.1 0.1
 输出样例：
 40.0% 20.0%
 */

#include<stdio.h>

int main(){
    int n,d,i,j,k;
    double e,ed;
    int knkz=0,kz=0,ad;
    scanf("%d%lf%d",&n,&e,&d);
    for(i=0;i<n;i++){
        scanf("%d",&k);
        ad=0;
        for(j=0;j<k;j++){
            scanf("%lf",&ed);
            if(ed<e) ad++;
        }
        if(k>d && ad>k/2) kz++;
        else if(ad>k/2) knkz++;
    }
    printf("%.1lf%% %.1lf%%\n",100.0*knkz/n,100.0*kz/n);
    
    return 0;
}
```



### PAT_1054求平均值

```c
/*本题的基本要求非常简单：给定 N个实数，计算它们的平均值。但复杂的是有些输入数据可能是非法的。一个“合法”的输入是 [−1000,1000] 区间内的实数，并且最多精确到小数点后 2 位。当你计算平均值的时候，不能把那些非法的数据算在内。
 输入格式：
 输入第一行给出正整数 N（≤100）。随后一行给出 N 个实数，数字间以一个空格分隔。
 输出格式：
 对每个非法输入，在一行中输出 ERROR: X is not a legal number，其中 X 是输入。最后在一行中输出结果：The average of K numbers is Y，其中 K 是合法输入的个数，Y 是它们的平均值，精确到小数点后 2 位。如果平均值无法计算，则用 Undefined 替换 Y。如果 K 为 1，则输出 The average of 1 number is Y。
 输入样例 1：
 7
 5 -3.2 aaa 9999 2.3.4 7.123 2.35
 输出样例 1：
 ERROR: aaa is not a legal number
 ERROR: 9999 is not a legal number
 ERROR: 2.3.4 is not a legal number
 ERROR: 7.123 is not a legal number
 The average of 3 numbers is 1.38
 输入样例 2：
 2
 aaa -9999
 输出样例 2：
 ERROR: aaa is not a legal number
 ERROR: -9999 is not a legal number
 The average of 0 numbers is Undefined
 */

#include<stdio.h>
#include<string.h>
#include<math.h>

float is_right(char s[]);//判断这个字符串是不是合法的，如果是合法的就返回其表示的数值，不然就返回1001;

int main(){
    int n,i,count_error=0;
    float num=0,sum=0;
    char s[200];
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%s",s);
        num=is_right(s);
        if(num>1000 || num<-1000){printf("ERROR: %s is not a legal number\n",s);count_error++;}
        else sum+=num;
//        memset(s,0,sizeof(s));//清空字符串
    }
    if(count_error==n){printf("The average of 0 numbers is Undefined\n");}
    else if(n-count_error==1) printf("The average of 1 number is %.2f\n", sum);
    else{
        printf("The average of %d numbers is %.2f\n",n-count_error,1.0*sum/(n-count_error));
    }
    
    return 0;
}

float is_right(char s[]){
    int i,cnt_dian=0,point=-1;
    float num=1001;
    int len = strlen(s);
    
    for(i=0;i<len;i++){//统计小数点的个数
        if(s[i]=='.') {cnt_dian++;point=i;}
    }
    if(cnt_dian>=2) return 1001;//两个以上小数点不符合要求
    else if(point!=-1 && len-point>3) return 1001;//小数点后两位以上不符合要求
    
    if(s[0]=='-'){
        if(len==1) return 1001;
        num=0;i=1;
        while(s[i]!='.' && i<len){
            num=num*10+(s[i]-'0');
            i++;
        }
        i++;
        while(i<len){
            num=num+(s[i]-'0')*(pow(10,point-i));
            i++;
        }
        num=0-num;
        return num;
    }
    
    
    else if('0'<=s[0] && s[0]<='9'){
        num=0;i=0;
        while(s[i]!='.' && i<len){
            num=num*10+s[i]-'0';
            i++;
        }
        i++;
        while(i<len){
            num=num+(s[i]-'0')*(pow(10,point-i));
            i++;
        }
        return num;
    }
    
    else return 1001;
    
    return num;
}
```



### PAT_1055集体照

```c
/*拍集体照时队形很重要，这里对给定的 N 个人 K 排的队形设计排队规则如下：
 每排人数为 N/K（向下取整），多出来的人全部站在最后一排；
 后排所有人的个子都不比前排任何人矮；
 每排中最高者站中间（中间位置为 m/2+1，其中 m 为该排人数，除法向下取整）；
 每排其他人以中间人为轴，按身高非增序，先右后左交替入队站在中间人的两侧（例如5人身高为190、188、186、175、170，则队形为175、188、190、186、170。这里假设你面对拍照者，所以你的左边是中间人的右边）；
 若多人身高相同，则按名字的字典序升序排列。这里保证无重名。
 现给定一组拍照人，请编写程序输出他们的队形。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例第 1 行给出两个正整数 N（≤104，总人数）和 K（≤10，总排数）。随后 N 行，每行给出一个人的名字（不包含空格、长度不超过 8 个英文字母）和身高（[30, 300] 区间内的整数）。
 输出格式：
 输出拍照的队形。即K排人名，其间以空格分隔，行末不得有多余空格。注意：假设你面对拍照者，后排的人输出在上方，前排输出在下方。
 输入样例：
 10 3
 Tom 188
 Mike 170
 Eva 168
 Tim 160
 Joe 190
 Ann 168
 Bob 175
 Nick 186
 Amy 160
 John 159
 输出样例：
 Bob Tom Joe Nick
 Ann Mike Eva
 Tim Amy John
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
typedef struct
{
    char Name[9];
    int H;
}Data;
int cmp(const void * a,const void * b)
{
    if( (*(Data *)a).H != (*(Data *)b).H )
        return (*(Data *)b).H - (*(Data *)a).H;
    else
        return strcmp( (*(Data *)a).Name , (*(Data *)b).Name );
}
int main()
{
    int N,K,mA,mB;
    scanf("%d %d",&N,&K);
    mA=N/K,mB=N/K+N%K;
    Data A[N];
    int B[K][mB];
    for(int i=0 ; i<N ; i++)
        scanf("%s %d",A[i].Name,&A[i].H);
    qsort(A,N,sizeof(Data),cmp);
    for(int i=0,n=0 ; i<K ; i++)
        for(int m= !i ? mB:mA,j=0,pos=m/2,flag=1 ; j<m ; j++,flag*=-1 )
            B[i][ pos+=j*flag ]=n++;
    for(int i=0 ; i<K ; i++)
        for(int j=0,m= !i ? mB:mA ; j<m ; j++ )
            printf("%s%s",A[ B[i][j] ].Name  , j<m-1 ? " " : "\n" );
    
    return 0;
}
```



### PAT_1056组合数的和

```c
/*给定 N 个非 0 的个位数字，用其中任意 2 个数字都可以组合成 1 个 2 位的数字。要求所有可能组合出来的 2 位数字的和。例如给定 2、5、8，则可以组合出：25、28、52、58、82、85，它们的和为330。
 输入格式：
 输入在一行中先给出 N（1 < N < 10），随后给出 N 个不同的非 0 个位数字。数字间以空格分隔。
 输出格式：
 输出所有可能组合出来的2位数字的和。
 输入样例：
 3 2 8 5
 输出样例：
 330
 */
#include<stdio.h>


int main(){
    int n,i,j,num[15],sum=0;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
    }
    for(i=0;i<n;i++){
        for(j=0;j<n;j++)
            if(i==j) continue;
            else{
                sum=sum+10*num[i]+num[j];
            }
    }
    printf("%d\n",sum);
    
    return 0;
}
```



### PAT_1057数零壹

```c
/*给定一串长度不超过 105
   的字符串，本题要求你将其中所有英文字母的序号（字母 a-z 对应序号 1-26，不分大小写）相加，得到整数 N，然后再分析一下 N 的二进制表示中有多少 0、多少 1。例如给定字符串 PAT (Basic)，其字母序号之和为：16+1+20+2+1+19+9+3=71，而 71 的二进制是 1000111，即有 3 个 0、4 个 1。
 输入格式：
 输入在一行中给出长度不超过 10 5、以回车结束的字符串。
 输出格式：
 在一行中先后输出 0 的个数和 1 的个数，其间以空格分隔。注意：若字符串中不存在字母，则视为 N 不存在，也就没有 0 和 1。
 输入样例：
 PAT (Basic)
 输出样例：
 3 4
 */

#include<stdio.h>
#include<string.h>

int main(){
    int n=0,i,len,er[1000007],t=0,cnt0=0,cnt1=0;
    char s[100005];
    gets(s);
    len=strlen(s);
    for(i=0;i<len;i++){
        if('a'<=s[i] && s[i]<='z') n+=s[i]-'a'+1;
        else if('A'<=s[i] && s[i]<='Z') n+=s[i]-'A'+1;
    }
//    printf("%d",n);
    while(n!=0){
        er[t++]=n%2;
        n=n/2;
    }
    for(i=0;i<t;i++){
        if(er[i]==0) cnt0++;
        else if(er[i]==1) cnt1++;
    }
    printf("%d %d\n",cnt0,cnt1);
    
    return 0;
}
```



### PAT_1058选择题

```c
/*输入在第一行给出两个正整数 N（≤ 1000）和 M（≤ 100），分别是学生人数和多选题的个数。随后 M 行，每行顺次给出一道题的满分值（不超过 5 的正整数）、选项个数（不少于 2 且不超过 5 的正整数）、正确选项个数（不超过选项个数的正整数）、所有正确选项。注意每题的选项从小写英文字母 a 开始顺次排列。各项间以 1 个空格分隔。最后 N 行，每行给出一个学生的答题情况，其每题答案格式为 (选中的选项个数选项1……)，按题目顺序给出。注意：题目保证学生的答题情况是合法的，即不存在选中的选项数超过实际选项数的情况。
 输出格式：
 按照输入的顺序给出每个学生的得分，每个分数占一行。注意判题时只有选择全部正确才能得到该题的分数。最后一行输出错得最多的题目的错误次数和编号（题目按照输入的顺序从 1 开始编号）。如果有并列，则按编号递增顺序输出。数字间用空格分隔，行首尾不得有多余空格。如果所有题目都没有人错，则在最后一行输出 Too simple。
 输入样例：
3 4
3 4 2 a c
2 5 1 b
5 3 2 b c
1 5 4 a b d e
(2 a c) (2 b d) (2 a c) (3 a b e)
(2 a c) (1 b) (2 a b) (4 a b d e)
(2 b d) (1 e) (2 b c) (4 a b c d)
 输出样例：
 3
 6
 5
 2 2 3 4
 */

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>

typedef struct {//题目
    int score;//分值
    int right_cnt;//正确选项个数
    char right[6];//所有正确选项
    int wrong;//错误的次数
} question;


int main(){
    int N, M, max_error = 0;//学生人数，多选题个数，最多错误次数
    scanf("%d %d", &N, &M);
    question q[M+1];
    for(int i = 1; i < M + 1; i++) {//读入多选题
        int cnt, j = 0;//选项个数（无用）
        scanf("%d %d %d", &q[i].score, &cnt, &q[i].right_cnt);
        q[i].wrong = 0;//初始化错误的次数
        char c;
        while ((c = getchar()) != '\n') {
            if (isalpha(c)) {//isalpha是一种函数：判断字符ch是否为英文字母，若为英文字母，返回非0（小写字母为2，大写字母为1）。
                q[i].right[j] = c;
                j++;
            }
        }
        q[i].right[j] = '\0';
    }
    for (int i = 0; i < N; i++) {//读入解答
        int grades = 0, cnt, j;//学生得分，选项个数
        for (j = 1; j < M + 1; j++) {
            scanf("(%d", &cnt);
            int k = 0;
            char c, choose[6];
            while ((c = getchar()) != ')') {
                if (isalpha(c)) {
                    choose[k] = c;
                    k++;
                }
            }
            choose[k] = '\0';
            if (cnt == q[j].right_cnt && strcmp(choose, q[j].right) == 0) {//如果正确，加上分数
                grades += q[j].score;
            } else {//错误则统计错误次数
                q[j].wrong++;
            }
            if (max_error < q[j].wrong) {
                max_error = q[j].wrong;
            }
            getchar();//读入回车或空格
        }
        printf("%d\n", grades);
    }
    if (max_error == 0) {//没有错题
        printf("Too simple");
    } else {
        printf("%d", max_error);
        for (int i = 1; i < M + 1; i++) {
            if (q[i].wrong == max_error) {
                printf(" %d", i);
            }
        }
    }
    printf("\n");
    return 0;
}
```



### PAT_1059C语言竞赛

```c
/*
 0、冠军将赢得一份“神秘大奖”（比如很巨大的一本学生研究论文集……）。
 1、排名为素数的学生将赢得最好的奖品 —— 小黄人玩偶！
 2、其他人将得到巧克力。
 给定比赛的最终排名以及一系列参赛者的 ID，你要给出这些参赛者应该获得的奖品。
 输入格式：
 输入第一行给出一个正整数 N（≤104），是参赛者人数。随后 N 行给出最终排名，每行按排名顺序给出一位参赛者的 ID（4 位数字组成）。接下来给出一个正整数 K 以及 K 个需要查询的 ID。
 输出格式：
 对每个要查询的 ID，在一行中输出 ID: 奖品，其中奖品或者是 Mystery Award（神秘大奖）、或者是 Minion（小黄人）、或者是 Chocolate（巧克力）。如果所查 ID 根本不在排名里，打印 Are you kidding?（耍我呢？）。如果该 ID 已经查过了（即奖品已经领过了），打印 ID: Checked（不能多吃多占）。
 输入样例：
6
1111
6666
8888
1234
5555
0001
6
8888
0001
1111
2222
8888
2222
 输出样例：
8888: Minion
0001: Chocolate
1111: Mystery Award
2222: Are you kidding?
8888: Checked
2222: Are you kidding?
 */

#include<stdio.h>
#include<math.h>

int isPrime(int x);

int  main(){
    int rank=1,n,id;
    int haxi[10004]={0};
    scanf("%d",&n);
    while(n--){
        scanf("%d",&id);
        haxi[id]=rank++;
    }
    scanf("%d",&n);
    while(n--){
        scanf("%d",&id);
        if(haxi[id]==-1){
            printf("%04d: Checked\n",id);
        }
        else if(haxi[id]==1) {
            printf("%04d: Mystery Award\n",id);
            haxi[id]=-1;
        }
        else if(haxi[id]==0){
            printf("%04d: Are you kidding?\n",id);
        }
        else if(isPrime(haxi[id])==0) {
            printf("%04d: Minion\n",id);
            haxi[id]=-1;
        }
        else{
            printf("%04d: Chocolate\n",id);
            haxi[id]=-1;
        }
    }
    
    
    return 0;
}

int isPrime(int x){
    int i,flag=0;
    if(x==2 || x==3) return 0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) flag++;
    }
    return flag;
}
```



### PAT_1060爱丁顿数

```c
/*即满足有 E 天骑车超过 E 英里的最大整数 E。据说爱丁顿自己的 E 等于87。
 现给定某人 N 天的骑车距离，请你算出对应的爱丁顿数 E（≤N）。
 输入格式：
 输入第一行给出一个正整数 N (≤10 5)，即连续骑车的天数；第二行给出 N 个非负整数，代表每天的骑车距离。
 输出格式：
 在一行中给出 N 天的爱丁顿数。
 输入样例：
10
6 7 6 9 3 10 8 2 7 8
 输出样例：
 6
 */
//n 9 8 7 6 5 4 3 2 1
//i 0 1 2 3 4 5 6 7 8

#include<stdio.h>
#include<stdlib.h>
#include<math.h>

int cmp(const void* _a,const void* _b);

int main(){
    int E,i,n,nums[100005];
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d",&nums[i]);
    }
    qsort(nums,n,sizeof(int),cmp);//大到小

    for(E=0;E<n && nums[E]>E+1;E++);///////!!!!!!!IMPORTANT
    
    printf("%d\n",E);
    return 0;
}

int cmp(const void* _a,const void* _b){
    int a=*(int*)_a, b=*(int*)_b;
    return b-a;
}
```



## 1061-1070

### PAT_1061判断题

```c
/*判断题的评判很简单，本题就要求你写个简单的程序帮助老师判题并统计学生们判断题的得分。
 输入格式：
 输入在第一行给出两个不超过 100 的正整数 N 和 M，分别是学生人数和判断题数量。第二行给出 M 个不超过 5 的正整数，是每道题的满分值。第三行给出每道题对应的正确答案，0 代表“非”，1 代表“是”。随后 N 行，每行给出一个学生的解答。数字间均以空格分隔。
 输出格式：
 按照输入的顺序输出每个学生的得分，每个分数占一行。
 输入样例：
3 6
2 1 3 3 4 5
0 0 1 0 1 1
0 1 1 0 0 1
1 0 1 0 1 0
1 1 0 0 1 1
 输出样例：
 13
 11
 12
 */

#include<stdio.h>

struct{
    int mark;
    int answer;
}q[105];

int main(){
    int n,m,i,j,sum,da[105];
    scanf("%d%d",&n,&m);
    for(j=0;j<m;j++){
        scanf("%d",&q[j].mark);
    }
    for(j=0;j<m;j++){scanf("%d",&q[j].answer);}
    for(i=0;i<n;i++){
        sum=0;
        for(j=0;j<m;j++){
            scanf("%d",&da[j]);
            if(da[j]==q[j].answer) sum+=q[j].mark;
        }
        printf("%d\n",sum);
    }
    
    return 0;
}
```



### PAT_1062最简分数

```c
/*一个分数一般写成两个整数相除的形式：N/M，其中 M 不为0。最简分数是指分子和分母没有公约数的分数表示形式。
 现给定两个不相等的正分数 N1/M 1 和 N2/M 2，要求你按从小到大的顺序列出它们之间分母为 K 的最简分数。
 输入格式：
 输入在一行中按 N/M 的格式给出两个正分数，随后是一个正整数分母 K，其间以空格分隔。题目保证给出的所有整数都不超过 1000。
 输出格式：
 在一行中按 N/M 的格式列出两个给定分数之间分母为 K 的所有最简分数，按从小到大的顺序，其间以 1 个空格分隔。行首尾不得有多余空格。题目保证至少有 1 个输出。
 输入样例：
 7/18 13/20 12
 输出样例：
 5/12 7/12
*/

#include<stdio.h>

int keyue(int a,int b);

int main(){
    int n1,n2,m1,m2,k;
    scanf("%d/%d %d/%d %d",&n1,&m1,&n2,&m2,&k);
    int index=0,nums[1005],i;
    if(1.0*n1/m1>1.0*n2/m2){
        i=n1;n1=n2;n2=i;
        i=m1;m1=m2;m2=i;
    }
    for(i=1;i<k;i++){
        if(1.0*n1/m1<1.0*i/k && 1.0*i/k<1.0*n2/m2){
            if(keyue(i,k)) nums[index++]=i;
        }
    }
    for(i=0;i<index-1;i++){
        printf("%d/%d ",nums[i],k);
    }
    printf("%d/%d\n",nums[i],k);
    return 0;
}

int keyue(int a,int b){
    //a<b
    int i;
    for(i=2;i<=a;i++){
        if(b%i==0 && a%i==0) return 0;//0表示可以约分
    }
    return 1;
}
```

```
题目没有规定前一个一定会小于后一个
```



### PAT_1063计算谱半径

```c
/*在数学中，矩阵的“谱半径”是指其特征值的模集合的上确界。换言之，对于给定的 n 个复数空间的特征值 { a
 1+b1i,⋯,an+bni }，它们的模为实部与虚部的平方和的开方，而“谱半径”就是最大模。
 现在给定一些复数空间的特征值，请你计算并输出这些特征值的谱半径。
 输入格式：
 输入第一行给出正整数 N（≤ 10 000）是输入的特征值的个数。随后 N 行，每行给出 1 个特征值的实部和虚部，其间以空格分隔。注意：题目保证实部和虚部均为绝对值不超过 1000 的整数。
 输出格式：
 在一行中输出谱半径，四舍五入保留小数点后 2 位。
 输入样例：
5
0 1
2 0
-1 0
3 3
0 -3
 输出样例：
 4.24
 */

#include<stdio.h>
#include<math.h>

struct{
    double a;
    double b;
}z[100005];

int main(){
    int n,i;
    double max=0;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%lf%lf",&z[i].a,&z[i].b);
        max=fmax(z[i].a*z[i].a+z[i].b*z[i].b,max);
    }
    printf("%.2lf\n",sqrt(max));
    return 0;
}
```



### PAT_1064朋友数

```c
/*如果两个整数各位数字的和是一样的，则被称为是“朋友数”，而那个公共的和就是它们的“朋友证号”。例如 123 和 51 就是朋友数，因为 1+2+3 = 5+1 = 6，而 6 就是它们的朋友证号。给定一些整数，要求你统计一下它们中有多少个不同的朋友证号。
 输入格式：
 输入第一行给出正整数 N。随后一行给出 N 个正整数，数字间以空格分隔。题目保证所有数字小于 104
 输出格式：
 首先第一行输出给定数字中不同的朋友证号的个数；随后一行按递增顺序输出这些朋友证号，数字间隔一个空格，且行末不得有多余空格。
 输入样例：
8
123 899 51 998 27 33 36 12
 输出样例：
 4
 3 6 9 26
 */

#include<stdio.h>
#include<stdlib.h>
int get_z(int x);

int main(){
    int i,n,count=0,num,pyz,nums[40],pr[40],index=0;
    scanf("%d",&n);
    for(i=0;i<40;i++) nums[i]=0;
    for(i=0;i<n;i++){
        scanf("%d",&num);
        pyz=get_z(num);
        if(nums[pyz]==0) count++;
        nums[pyz]++;
    }
    printf("%d\n",count);
    for(i=0;i<=36;i++){
        if(nums[i]>0) pr[index++]=i;
    }
    for(i=0;i<index-1;i++){
        printf("%d ",pr[i]);
    }
    if(index!=0)printf("%d\n",pr[i]);
    
    return 0;
}

int get_z(int x){
    int return_num=0;
    while(x>0){
        return_num+=x%10;
        x=x/10;
    }
    return return_num;
}
```



### PAT_1065单身狗

```c
/*本题请你从上万人的大型派对中找出落单的客人，以便给予特殊关爱。
 输入格式：
 输入第一行给出一个正整数 N（≤ 50 000），是已知夫妻/伴侣的对数；随后 N 行，每行给出一对夫妻/伴侣——为方便起见，每人对应一个 ID 号，为 5 位数字（从 00000 到 99999），ID 间以空格分隔；之后给出一个正整数 M（≤ 10 000），为参加派对的总人数；随后一行给出这 M 位客人的 ID，以空格分隔。题目保证无人重婚或脚踩两条船。
 输出格式：
 首先第一行输出落单客人的总人数；随后第二行按 ID 递增顺序列出落单的客人。ID 间用 1 个空格分隔，行的首尾不得有多余空格。
 输入样例：
3
11111 22222
33333 44444
55555 66666
7
55555 44444 10000 88888 22222 11111 23333
 输出样例：
 5
 10000 23333 44444 55555 88888
 */

#include<stdio.h>

int main(){
    int n,m,i,couple[100005],zaichang[100005],a,b,dog[100005],pr[100005],index=0;
    scanf("%d",&n);
    for(i=0;i<=99999;i++) {zaichang[i]=-1;couple[i]=-1;dog[i]=0;}
    for(i=0;i<n;i++){
        scanf("%d %d",&a,&b);
        couple[a]=b;
        couple[b]=a;
    }
    scanf("%d",&m);
    for(i=0;i<m;i++){
        scanf("%d",&a);
        zaichang[a]=1;
    }
    for(i=0;i<=99999;i++){
        if(zaichang[i]==1 && couple[i]==-1) dog[i]=1;
        if(zaichang[i]==1 && zaichang[couple[i]]==-1) dog[i]=1;
    }
    for(i=0;i<=99999;i++){
        if(dog[i]==1) pr[index++]=i;
    }
    printf("%d\n",index);
    for(i=0;i<index-1;i++){
        printf("%05d ",pr[i]);
    }
    if(index!=0)printf("%05d\n",pr[i]);
    
    return 0;
}
```



### PAT_1066图像过滤

```c
/*
 图像过滤是把图像中不重要的像素都染成背景色，使得重要部分被凸显出来。现给定一幅黑白图像，要求你将灰度值位于某指定区间内的所有像素颜色都用一种指定的颜色替换。
 输入格式：
 输入在第一行给出一幅图像的分辨率，即两个正整数 M 和 N（0<M,N≤500），另外是待过滤的灰度值区间端点 A 和 B（0≤A<B≤255）、以及指定的替换灰度值。随后 M 行，每行给出 N 个像素点的灰度值，其间以空格分隔。所有灰度值都在 [0, 255] 区间内。
 输出格式：
 输出按要求过滤后的图像。即输出 M 行，每行 N 个像素灰度值，每个灰度值占 3 位（例如黑色要显示为 000），其间以一个空格分隔。行首尾不得有多余空格。
 输入样例：
3 5 100 150 0
3 189 254 101 119
150 233 151 99 100
88 123 149 0 255
 输出样例：
 003 189 254 000 000
 000 233 151 099 000
 088 000 000 000 255
 */

#include<stdio.h>

int main(){
    int m,n,a,b,k,i,j,temp,xs[505][505];
    scanf("%d%d%d%d%d",&m,&n,&a,&b,&k);
//    if(a>b){temp=a;a=b;b=temp;}
    for(i=0;i<m;i++){
        for(j=0;j<n;j++){
            scanf("%d",&xs[i][j]);
            if(a<=xs[i][j] && xs[i][j]<=b) xs[i][j]=k;
        }
    }
    for(i=0;i<m;i++){
        for(j=0;j<n-1;j++){printf("%03d ",xs[i][j]);}
        printf("%03d\n",xs[i][j]);
    }
    return 0;
}
```



### PAT_1067试密码

```c
/*
 当你试图登录某个系统却忘了密码时，系统一般只会允许你尝试有限多次，当超出允许次数时，账号就会被锁死。本题就请你实现这个小功能。
 输入格式：
 输入在第一行给出一个密码（长度不超过 20 的、不包含空格、Tab、回车的非空字符串）和一个正整数 N（≤ 10），分别是正确的密码和系统允许尝试的次数。随后每行给出一个以回车结束的非空字符串，是用户尝试输入的密码。输入保证至少有一次尝试。当读到一行只有单个 # 字符时，输入结束，并且这一行不是用户的输入。
 输出格式：
 对用户的每个输入，如果是正确的密码且尝试次数不超过 N，则在一行中输出 Welcome in，并结束程序；如果是错误的，则在一行中按格式输出 Wrong password: 用户输入的错误密码；当错误尝试达到 N 次时，再输出一行 Account locked，并结束程序。
 输入样例 1：
Correct%pw 3
correct%pw
Correct@PW
whatisthepassword!
Correct%pw
#
 输出样例 1：
 Wrong password: correct%pw
 Wrong password: Correct@PW
 Wrong password: whatisthepassword!
 Account locked
 输入样例 2：
cool@gplt 3
coolman@gplt
coollady@gplt
cool@gplt
try again
#
 输出样例 2：
 Wrong password: coolman@gplt
 Wrong password: coollady@gplt
 Welcome in
 */


#include<stdio.h>
#include<string.h>

int main(){
    int n;
    char right[50],mi[50];
    scanf("%s %d",right,&n);
    gets(mi);
    while(1){
//        scanf("%s",mi);
        gets(mi);
        if(strlen(mi)==1 && mi[0]=='#') break;
        else if(strcmp(right,mi)!=0){//cuo
            printf("Wrong password: %s\n",mi);
            n--;
            if(n==0) {printf("Account locked\n");return 0;}
        }
        else{
            printf("Welcome in\n");
            return 0;
        }
    }
    return 0;
}
```

```
scanf后用一个gets把缓存区的东西拿干净后再gets密码，因为可能错误的密码会包括空格，所以只能用gets，数组长度可以稍微长一点。
```



### PAT_1068万绿丛中一点红

```c
/*
 对于计算机而言，颜色不过是像素点对应的一个 24 位的数值。现给定一幅分辨率为 M×N 的画，要求你找出万绿丛中的一点红，即有独一无二颜色的那个像素点，并且该点的颜色与其周围 8 个相邻像素的颜色差充分大。
 输入格式：
 输入第一行给出三个正整数，分别是 M 和 N（≤ 1000），即图像的分辨率；以及 TOL，是所求像素点与相邻点的颜色差阈值，色差超过 TOL 的点才被考虑。随后 N 行，每行给出 M 个像素的颜色值，范围在 [0,2 24) 内。所有同行数字间用空格或 TAB 分开。
 输出格式：
 在一行中按照 (x, y): color 的格式输出所求像素点的位置以及颜色值，其中位置 x 和 y 分别是该像素在图像矩阵中的列、行编号（从 1 开始编号）。如果这样的点不唯一，则输出 Not Unique；如果这样的点不存在，则输出 Not Exist。
 输入样例 1：
8 6 200
0      0       0        0        0          0           0        0
65280      65280    65280    16711479 65280    65280    65280    65280
16711479 65280    65280    65280    16711680 65280    65280    65280
65280      65280    65280    65280    65280    65280    165280   165280
65280      65280       16777015 65280    65280    165280   65480    165280
16777215 16777215 16777215 16777215 16777215 16777215 16777215 16777215
 输出样例 1：
 (5, 3): 16711680
 输入样例 2：
4 5 2
0 0 0 0
0 0 3 0
0 0 0 0
0 5 0 0
0 0 0 0
 输出样例 2：
 Not Unique
 输入样例 3：
3 3 5
1 2 3
3 4 5
5 6 7
 输出样例 3：
 Not Exist
 */

#include<stdio.h>
#include<math.h>
#include <stdlib.h>

int m,n,i,temp,j,count_point=0,num[2 << 24]={0},x = 0,y = 0;

int main(){
    int tol,xs[1002][1002]={0};
    scanf("%d%d%d",&m,&n,&tol);
    for(i=1;i<=n;i++){
        for(j=1;j<=m;j++){
            scanf("%d",&temp);
            xs[i][j]=temp;
            num[temp]++;
        }
    }
    
    for(i=1;i<=n;i++){
        for(j=1;j<=m;j++){
            if(num[xs[i][j]]==1 && abs(xs[i-1][j]-xs[i][j])>tol && abs(xs[i-1][j-1]-xs[i][j])>tol && abs(xs[i][j-1]-xs[i][j])>tol && abs(xs[i+1][j]-xs[i][j])>tol && abs(xs[i+1][j+1]-xs[i][j])>tol && abs(xs[i][j+1]-xs[i][j])>tol && abs(xs[i-1][j+1]-xs[i][j])>tol && abs(xs[i+1][j-1]-xs[i][j])>tol)
            {
                count_point++;
                x = j; y = i;
            }
        }
    }
    if(count_point==0)printf("Not Exist\n");
    else if(count_point==1) printf("(%d, %d): %d\n", x, y, xs[y][x]);
    else if(count_point>1) printf("Not Unique\n");
    return 0;
}
```

```
定义的int放到main外面可以通过
```



### PAT_1069微博转发抽奖

```c
/*
 小明 PAT 考了满分，高兴之余决定发起微博转发抽奖活动，从转发的网友中按顺序每隔 N 个人就发出一个红包。请你编写程序帮助他确定中奖名单。
 输入格式：
 输入第一行给出三个正整数 M（≤ 1000）、N 和 S，分别是转发的总量、小明决定的中奖间隔、以及第一位中奖者的序号（编号从 1 开始）。随后 M 行，顺序给出转发微博的网友的昵称（不超过 20 个字符、不包含空格回车的非空字符串）。
 注意：可能有人转发多次，但不能中奖多次。所以如果处于当前中奖位置的网友已经中过奖，则跳过他顺次取下一位。
 输出格式：
 按照输入的顺序输出中奖名单，每个昵称占一行。如果没有人中奖，则输出 Keep going...。
 输入样例 1：
9 3 2
Imgonnawin!
PickMe
PickMe
LookHere
Imgonnawin!
TryAgainAgain
TryAgainAgain
Imgonnawin!
TryAgainAgain
 输出样例 1：
PickMe
Imgonnawin!
TryAgainAgain
 输入样例 2：
2 3 5
Imgonnawin!
PickMe
 输出样例 2：
 Keep going...
 */

#include<stdio.h>
#include<string.h>

int main(){
    int m,n,s;//分别是转发的总量、小明决定的中奖间隔、以及第一位中奖者的序号
    char id_zhongjiang[1003][25],id[25];
    int i=1,index=0,j,flag=0,count_zj=0;
    scanf("%d%d%d",&m,&n,&s);
    for(j=0;j<s-1;j++) {scanf("%s",id);i++;}//跳过第一位中奖者前面的序号
    while(i<=m){
        scanf("%s",id);i++;//读取要中奖的人的id
        flag=0;
        for(j=0;j<index;j++){//判断这人是不是已经中过奖了
            if(strcmp(id,id_zhongjiang[j])==0) {flag=1;break;}
        }
        if(flag) continue;//如果他中过奖了，进入下一次循环，读取下一个id
        else if(flag==0) {//如果他没中奖，把他的id放到中奖名单中，并记录中奖次数+1
            strcpy(id_zhongjiang[index++],id);
            count_zj++;
        }
        if(i+n-1<=m){
            for(j=1;j<n;j++) {scanf("%s",id);i++;}//跳过中间间隔的id
        }
        else break;
    }
    for(j=0;j<index;j++)printf("%s\n",id_zhongjiang[j]);
    if(count_zj==0)printf("Keep going...\n");
    return 0;
}
```



### PAT_1070结绳

```c
/*给定一段一段的绳子，你需要把它们串成一条绳。每次串连的时候，是把两段绳子对折，再如下图所示套接在一起。这样得到的绳子又被当成是另一段绳子，可以再次对折去跟另一段绳子串连。每次串连后，原来两段绳子的长度就会减半。
 给定 N 段绳子的长度，你需要找出它们能串成的绳子的最大长度。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例第 1 行给出正整数 N (2≤N≤10 4  )；第 2 行给出 N 个正整数，即原始绳段的长度，数字间以空格分隔。所有整数都不超过10 4。
 输出格式：
 在一行中输出能够串成的绳子的最大长度。结果向下取整，即取为不超过最大长度的最近整数。
 输入样例：
8
10 15 12 3 4 13 1 15
 输出样例：
 14
 */

#include<stdio.h>
#include<stdlib.h>

int cmp(const void* _a, const void* _b){
    int a=*(int*)_a;
    int b=*(int*)_b;
    return a-b;
}

int main(){
    int n,nums[10004],sum=0,i;
    scanf("%d",&n);
    for(i=0;i<n;i++){scanf("%d",&nums[i]);}
    qsort(nums,n,sizeof(int),cmp);
    sum=nums[0];
    for(i=1;i<n;i++){
        sum=(sum+nums[i])/2;
    }
    printf("%d\n",sum);
    return 0;
}
```



## 1071-1080

### PAT_1071小赌怡情

```c
/*常言道“小赌怡情”。这是一个很简单的小游戏：首先由计算机给出第一个整数；然后玩家下注赌第二个整数将会比第一个数大还是小；玩家下注 t 个筹码后，计算机给出第二个数。若玩家猜对了，则系统奖励玩家 t 个筹码；否则扣除玩家 t 个筹码。
 注意：玩家下注的筹码数不能超过自己帐户上拥有的筹码数。当玩家输光了全部筹码后，游戏就结束。
 输入格式：
 输入在第一行给出 2 个正整数 T 和 K（≤ 100），分别是系统在初始状态下赠送给玩家的筹码数、以及需要处理的游戏次数。随后 K 行，每行对应一次游戏，顺序给出 4 个数字： n1 b t n2
 其中 n1 和 n2 是计算机先后给出的两个[0, 9]内的整数，保证两个数字不相等。b 为 0 表示玩家赌小，为 1 表示玩家赌大。t 表示玩家下注的筹码数，保证在整型范围内。
 输出格式：
 对每一次游戏，根据下列情况对应输出（其中 t 是玩家下注量，x 是玩家当前持有的筹码量）：
 玩家赢，输出 Win t! Total = x.；
 玩家输，输出 Lose t. Total = x.；
 玩家下注超过持有的筹码量，输出 Not enough tokens. Total = x.；
 玩家输光后，输出 Game Over. 并结束程序。
 输入样例 1：
100 4
8 0 100 2
3 1 50 1
5 1 200 6
7 0 200 8
 输出样例 1：
 Win 100!  Total = 200.
 Lose 50.  Total = 150.
 Not enough tokens.  Total = 150.
 Not enough tokens.  Total = 150.
 输入样例 2：
100 4
8 0 100 2
3 1 200 1
5 1 200 6
7 0 200 8
 输出样例 2：
 Win 100!  Total = 200.
 Lose 200.  Total = 0.
 Game Over.
 */

#include<stdio.h>

int main(){
    int T,K;
    int n1,b,t,n2;
    scanf("%d%d",&T,&K);
    while(K--){
        scanf("%d%d%d%d",&n1,&b,&t,&n2);
        if(t>T) {printf("Not enough tokens.  Total = %d.\n",T);continue;}
        if((n2>n1 && b==1) || (n2<n1 && b==0)){//win
            T=T+t;
            printf("Win %d!  Total = %d.\n",t,T);
        }
        else{
            T=T-t;
            printf("Lose %d.  Total = %d.\n",t,T);
            if(T==0) {printf("Game Over.");break;}
        }
    }
    return 0;
}
```



### PAT_1072开学寄语

```c
/*本题要求你写个程序帮助这所学校的老师检查所有学生的物品，以助其成大器。
 输入格式：
 输入第一行给出两个正整数 N（≤ 1000）和 M（≤ 6），分别是学生人数和需要被查缴的物品种类数。第二行给出 M 个需要被查缴的物品编号，其中编号为 4 位数字。随后 N 行，每行给出一位学生的姓名缩写（由 1-4 个大写英文字母组成）、个人物品数量 K（0 ≤ K ≤ 10）、以及 K 个物品的编号。
 输出格式：
 顺次检查每个学生携带的物品，如果有需要被查缴的物品存在，则按以下格式输出该生的信息和其需要被查缴的物品的信息（注意行末不得有多余空格）：
 姓名缩写: 物品编号1 物品编号2 ……
 最后一行输出存在问题的学生的总人数和被查缴物品的总数。
 输入样例：
4 2
2333 6666
CYLL 3 1234 2345 3456
U 4 9966 6666 8888 6666
GG 2 2333 7777
JJ 3 0012 6666 2333
 输出样例：
 U: 6666 6666
 GG: 2333
 JJ: 6666 2333
 3 5
 */

#include<stdio.h>
#include<string.h>

int main(){
    int n,m,k,temp;
    char name[10];
    int i,num[10004],count_stu=0,count_thing=0,pr[15],index=0;
    scanf("%d%d",&n,&m);
    for(i=0;i<=9999;i++) num[i]=0;
    for(i=0;i<m;i++){
        scanf("%d",&temp);
        num[temp]=1;
    }
    while(n--){
        scanf("%s%d",name,&k);
        index=0;
        for(i=0;i<k;i++){
            scanf("%d",&temp);
            if(num[temp]==1){
                count_thing++;
                pr[index++]=temp;
            }
        }
        if(index>0) {
            count_stu++;
            printf("%s: ",name);
            for(i=0;i<index-1;i++){printf("%04d ",pr[i]);}
            if(index>0) printf("%04d\n",pr[i]);
        }
    }
    printf("%d %d\n",count_stu,count_thing);
    return 0;
}
```

