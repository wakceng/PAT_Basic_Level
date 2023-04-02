### 1.ACM_1000_A+B Problem

```c
#include <stdio.h>

int main() {
    int a,b;
    printf("请输入两个数：");
    scanf("%d %d",&a,&b);
    printf("他们的和是%d\n",a+b);
    return 0;
}
```



### 2.ACM_1001_printf

```c
#include <stdio.h>

int main(){
    printf(
           "**************************\n"
           "         Very    Good!\n"
           "**************************\n"
           );
    return 0;
}
```



### 3.ACM_1002_abcMax

```c
#include <stdio.h>

int main(){
    int a,b,c,x;
    printf("请输入三个整数，我将告诉你最大值\n");
    scanf("%d %d %d",&a,&b,&c);
    x=(a>b)? a:b;
    x=(x>c)? x:c;
    printf("最大值是%d\n",x);
    return 0;
}
```



### 4.ACM_1003_rename

```c
#include <stdio.h>

int main(){
    char c1,c2,c3,c4,c5;
    int num;
    char a='e';
    char b='a';
    num = a-b;
    printf("%d\n",num);
    scanf("%c%c%c%c%c",&c1,&c2,&c3,&c4,&c5);
    printf("%c%c%c%c%c\n",c1+num,c2+num,c3+num,c4+num,c5+num);
    return 0;
}
```



### 5.ACM_1004_Pi_V

```c
//输入两个浮点数，圆半径r和圆柱体高h
//Pi=3.14
//圆周长C1、圆面积Sa、圆球表面积Sb、圆球体积Va、圆柱体积Vb。
//保留两位小数，每个结果后换行。
#include<stdio.h>

#define PI 3.14
int main(){
    float r,h;
    scanf("%f %f",&r,&h);
    printf("C1=%.2f\n",2*PI*r);
    printf("Sa=%.2f\n",PI*r*r);
    printf("Sb=%.2f\n",4*PI*r*r);
    printf("Va=%.2f\n",PI*r*r*r*4/3);
    printf("Vb=%.2f\n",h*PI*r*r);
    return 0;
}
```



### 6.ACM_1005_C_F

```c
#include <stdio.h>

int main() {
    float f;
    scanf("%f",&f);
    printf("c=%.2f\n",5.0*(f-32)/9);
    return 0;
}
```



### 7.ACM_1006_Max(abc)

```c
#include <stdio.h>

int max(int a,int b){
    int x = (a>b)? a:b;
    return x;
}

int main(){
    int a,b,c;
    scanf("%d %d %d",&a,&b,&c);
    printf("%d\n",max(max(a,b),c));
    return 0;
}
```



### 8.ACM_1007_fdhs

```c
#include<stdio.h>

int xy(int x){
    int y;
    if(x<1){y=x;}
    else if(x<10){y=2*x-1;}
    else{y=3*x-11;}
    return y;
}

int main(){
    int x;
    scanf("%d",&x);
    printf("%d\n",xy(x));
    return 0;
}
```



### 9.ACM_1008_Grade

```c
#include<stdio.h>

int main(){
    int g;
    scanf("%d",&g);
    if(g>=90){printf("A\n");}
    else if(g>=80){printf("B\n");}
    else if(g>=70){printf("C\n");}
    else if(g>=60){printf("D\n");}
    else{printf("E\n");}
    return 0;
}
```



### 10.ACM_1009_nixu

```c
//输入
//一个不大于5位的数字
//输出
//三行
//第一行 位数
//第二行 用空格分开的每个数字，注意最后一个数字后没有空格
//第三行 按逆序输出这个数
//样例输入
//12345
//样例输出
//5
//1 2 3 4 5
//54321

#include<stdio.h>

int get_len(int x);
int ten_e_i(int x);

int main(){
    int num,len_num,i;
    int str[15]={0};
    int ten_i;
    scanf("%d",&num);
    len_num = get_len(num);
    printf("%d\n",len_num);
    
    i=len_num;
    while(i>1){
        ten_i=ten_e_i(i-1);
        str[i]=num / ten_i;
        num = num - str[i]*ten_i;
        printf("%d ",str[i]);
        i--;
    }
    ten_i=ten_e_i(i-1);
    str[i]=num / ten_i;
    num = num - str[i]*ten_i;
    printf("%d\n",str[i]);
    i--;
    
    for(i=1;i<=len_num;i++){
        printf("%d",str[i]);
    }
    printf("\n");
    
    return 0;
}


int get_len(int x){
    int len=1;
    while(x/10>=1){
        len++;
        x=x/10;
    }
    return len;
}

int ten_e_i(int x){
    int ten=1;
    for(int i = x; x>=1 ;x--){
        ten = 10*ten;
    }
    return ten;
}
```



### 11.ACM_1010_jiangjin

```c
//企业发放的奖金根据利润提成。利润低于或等于100000元的，奖金可提10%;
//利润高于100000元，低于200000元（100000<I≤200000）时，低于100000元的部分按10％提成，
//高于100000元的部分，可提成7.5%;
//200000<I≤400000时，低于200000元部分仍按上述办法提成，（下同），高于200000元的部分按5％提成；
//400000<I≤600000元时，高于400000元的部分按3％提成；600000<I≤1000000时，高于600000元的部分按1.5%提成；
//I>1000000时，超过1000000元的部分按1%提成。从键盘输入当月利润I,求应发奖金总数。

#include<stdio.h>
int main(){
    int a,b,s;
    b=0;
    //a是利润，b是奖金
    scanf("%d",&a);
    s=a/100000;
    if(s>10){s=10;}
//    printf("%d\n",s);
    switch(s)
    {
        case 10:b=b+(a-1000000)/100;
                a=1000000;
        case 9:
        case 8:
        case 7:
        case 6:b=b+(a-600000)*15/1000;
               a=600000;
        case 5:
        case 4:b=b+(a-400000)*3/100;
               a=400000;
        case 3:
        case 2:b=b+(a-200000)/20;
               a=200000;
        case 1:b=b+(a-100000)*75/1000;
               a=100000;
        case 0:b=b+a/10;
    }
    printf("%d\n",b);
    return 0;
}
```



### 12.ACM_1011_yue

```c
//输入两个正整数m和n，求其最大公约数和最小公倍数。
#include<stdio.h>

int big_yue(int x,int y);
int small_bei(int x,int y);
int main(){
    int x,y,t;
    scanf("%d %d",&x,&y);
    if(x>y){t=x;x=y;y=t;}//结果是y大
    printf("%d\n",big_yue(x,y));
    printf("%d\n",small_bei(x,y));
    return 0;
}

int big_yue(int x,int y){
    int num=-1;
    while (y%x) {
        num = y%x;
        y=x;
        x=num;
    }
    num = x;
    return num;
}

int small_bei(int x,int y){
    int num=-1;
    int sum;
    sum = x*y;
    while (y%x) {
        num = y%x;
        y=x;
        x=num;
    }
    num = x;
    sum = sum/num;
    return sum;
}
```



### 13.ACM_1012_strjishu

```c
#include<stdio.h>
#include<string.h>

int main(){
    char str[100];
    int E_num=0,N_num=0,S_num=0,Q_num=0;
    int len_str=0;
    gets(str);
    len_str=strlen(str);
    for(int i=0;i<len_str;i++)
    {
        if(65<=str[i] && str[i]<=90) E_num++;
        else if (97<=str[i] && str[i]<=122) E_num++;
        else if (str[i]==32) S_num++;
        else if (48<=str[i] && str[i]<=57) N_num++;
        else Q_num++;
    }

    printf("%d %d %d %d\n",E_num,N_num,S_num,Q_num);
    return 0;
}
```



### 14.ACM_1013_a+aa

```c
#include<stdio.h>

int main(){
    int a,n;
    long sum=0;
    int aaa=0;
    scanf("%d %d",&a,&n);
    for(int i=1;i<=n;i++)
    {
        aaa = 0;
        for(int j = 1;j<=i;j++){
            aaa = aaa*10+a;
        }
        sum = sum + aaa;
    }
    printf("%ld\n",sum);
    return 0;
}
```



### 15.ACM_1014_n!

```c
#include<stdio.h>

int main(){
    long sum=0,n_t=0;
    int n;
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        n_t=1;
        for(int j=1;j<=i;j++){
            n_t = n_t*j;
        }
        sum = sum + n_t;
    }
    printf("%ld\n",sum);
    return 0;
}
```



### 16.ACM_1015_a.b.c

```c
#include<stdio.h>

int main(){
    int a,b,c;
    double sum=0;
    scanf("%d %d %d",&a,&b,&c);
    for(int i = 1;i<=a;i++){
        sum += i;
    }
    for(int i = 1;i<=b;i++){
        sum += i*i;
    }
    for(int i = 1;i<=c;i++){
        sum += 1.0/i;
    }
    printf("%.2lf\n",sum);
    return 0;
}
```



### 17.ACM_1016_sxh

```c
//打印出所有"水仙花数"，所谓"水仙花数"是指一个三位数，其各位数字立方和等于该本身。
//例如：153是一个水仙花数，因为153=1^3+5^3+3^3。
#include<stdio.h>

int main(){
    int num,i,j,k;
    for(num = 100;num<1000;num++){
        i = num/100;
        j = (num - 100*i)/10;
        k = num%10;
        if(i*i*i+j*j*j+k*k*k==num) printf("%d\n",num);
    }
    return 0;
}
```



### 18.ACM_1017_wanshu

```c
//一个数如果恰好等于它的因子之和，这个数就称为"完数"。 例如，6的因子为1、2、3，而6=1+2+3，因此6是"完数"。 编程序找出N之内的所有完数，并按下面格式输出其因子：
//输入
//N
//输出
//? its factors are ? ? ?
//样例输入
//1000
//样例输出
//6 its factors are 1 2 3
//28 its factors are 1 2 4 7 14
//496 its factors are 1 2 4 8 16 31 62 124 248
//
#include<stdio.h>

int main(){
    int N;
    int num_yin=0,sum=0;
    int yin[50]={0};
    scanf("%d",&N);
    
    for(int i = 2;i<=N;i++){
        for(int j = 1;j<=i/2;j++){
            if(i%j==0){
                yin[num_yin] = j;
                num_yin++;
                sum+=j;
            }
        }
        if(i==sum){
            printf("%d its factors are",i);
            for(int j=0;j<num_yin;j++)printf(" %d",yin[j]);
            printf("\n");
        }
        sum=0;
        num_yin=0;
    }
    return 0;
}
```



### 19.ACM_1018_21+32

```c
//有一分数序列：
//2/1 3/2 5/3 8/5 13/8 21/13......
//求出这个数列的前N项之和，保留两位小数。

#include<stdio.h>

int main(){
    int a=2,b=1,n,t;
    double sum=0;
    scanf("%d",&n);
    for(int i = 1;i<=n;i++)
    {
        sum = sum + 1.0*a/b;
        t=a;
        a = a+b;
        b=t;
    }
    printf("%.2lf\n",sum);
    return 0;
}
```



### 20.ACM_1019_luoti

```c
//一球从M米高度自由下落，每次落地后返回原高度的一半，再落下。在第N次落地时反弹多高？共经过多少米？保留两位小数
//输入M N输出它在第N次落地时反弹多高？共经过多少米？保留两位小数，空格隔开，放在一行
//样例输入1000 5样例输出31.25 2875.00

#include<stdio.h>

int main(){
    int M,N;
    float sum=0,tan;
    scanf("%d %d",&M,&N);
    tan = M;
    for(int i = 1;i<=N;i++)
    {
        sum = sum + tan + tan/2.0;
        tan = tan /2.0;
    }
    printf("%.2f %.2f\n",tan,sum-tan);
    return 0;
}
```



### 21.ACM_1020_MeatP

```c
//猴子吃桃问题。猴子第一天摘下若干个桃子，当即吃了一半，还不过瘾，又多吃了一个。
//第二天早上又将剩下的桃子吃掉一半，又多吃一个。以后每天早上都吃了前一天剩下的一半零一个。
//到第N天早上想再吃时，见只剩下一个桃子了。求第一天共摘多少桃子。

#include<stdio.h>

int main(){
    int sum=1,n;
    scanf("%d",&n);
    for(int i=1; i<n ;i++){
        sum=(sum+1)*2;
    }
    printf("%d\n",sum);
    return 0;
}
```



### 22.ACM_1021_diedai

```c
//用迭代法求求平方根的迭代公式为：X[n+1]=1/2(X[n]+a/X[n])要求前后两次求出的得差的绝对值少于0.00001。
#include<stdio.h>
#include<math.h>

int main(){
    int n;
    double x1,x2;
    scanf("%d",&n);
    x2 = n/2.0;
    while(fabs(x1-x2)>0.0001)
    {
        x1=x2;
        x2 = (x1+n/x1)/2.0;
    }
    printf("%.3lf\n",x1);
    return 0;
}
```



### 23.ACM_1022_sushu

```c
//求N内的素数。

#include<stdio.h>

int is_su(int x);

int main(){
    int N;
    scanf("%d",&N);
    for(int i = 1; i <= N;i++){
        if(is_su(i)==1)
        printf("%d\n",i);
    }
    return 0;
}

int is_su(int x){
    int flag=0;
    for(int i = 1; i <= x/2 ;i++){
        if(x%i==0)flag++;
    }
    return flag;
}
```

```c
//用筛法求之N内的素数。筛法求素数：把 2 到 n 中所有的数都列出来，然后从 2 开始，先划掉 n 以内的所有 2 的倍数，然后每次从下一个剩下的数（必然是素数）开始，划掉其 n 内的所有倍数。最后剩下的数，就都是素数。（空间换时间，提高了运算速度）
#include<stdio.h>
int main(){
    int num[4000] = {0};//如果下标不是素数，将num值改为1；
    int N;
    scanf("%d",&N);
    for(int i=2;i<=N;i++)
    {
        if(num[i]==0)//若i是素数，从素数i开始，将2i、3i、、、都认为不是素数
        {
            for(int j = 2 * i; j <= N; j = j + i)
            {
                num[j]=1;
            }
        }
    }
//    如此，所有不是素数的都都是1
    for(int i = 2;i<=N;i++){
        if(num[i]==0){
            printf("%d\n",i);
        }
    }
//    printf("finish");
    return 0;
}
```



### 24.ACM_1023_paixu_xz

```c
//用选择法对10个整数从小到大排序。按照升序的排序，设有10个元素，从第一个开始和其余求个进行比较，最小的放在第一个数，再将第二个数和余下8个进行比较，再将最小的放在第二位，一直到排序结束。
#include<stdio.h>

int main(){
    int num[11]={0};
    int t;
    for(int i=0;i<10;i++){
        scanf("%d",&num[i]);
    }
    for(int i = 0;i<10;i++)
    {
        for(int j = i+1;j<10;j++)
        {
            if(num[i]>num[j])
            {
                t=num[i];num[i]=num[j];num[j]=t;
            }
        }
    }
    for(int i=0;i<10;i++){
        printf("%d\n",num[i]);
    }
    return 0;
}
```



### 25.ACM_1024_3x3he

```c
//主对角线 副对角线 元素和
#include<stdio.h>

int main(){
    int num[3][3];
    int sum1=0,sum2=0;
    for(int i =0;i<3;i++)
    {
        for(int j=0;j<3;j++)
        {
            scanf("%d",&num[i][j]);
        }
    }
    for(int i=0;i<3;i++)sum1+=num[i][i];
    for(int i=0;i<3;i++)sum2+=num[i][2-i];
    printf("%d %d\n",sum1,sum2);
    return 0;
}
```



### 26.ACM_1025_inpaixu

```c
//已有一个已排好的9个元素的数组，今输入一个数要求按原来排序的规律将它插入数组中。
#include<stdio.h>

int main(){
    int num1[10]={0};
    int num2[11]={0};
    int n,i;
    for(i=0;i<9;i++){
        scanf("%d",&num1[i]);
    }
    scanf("%d",&n);
    for(i=0;i<9;i++){
        if((num1[i]<=n)&&(n<=num1[i+1])) break;
    }
    for(int j = 0;j<=i;j++){num2[j]=num1[j];}
    num2[i+1]=n;
    for(int j =i+2;j<10;j++){num2[j]=num1[j-1];}
    for(int j=0;j<10;j++){
        printf("%d\n",num2[j]);
    }
    return 0;
}
```



### 27.ACM_1026_Nnixu

```c
//输入10个数字，然后逆序输出。

#include<stdio.h>

int main(){
    int num[11];
    for(int i=0;i<10;i++){
        scanf("%d",&num[i]);
    }
    for(int i=9;i>0;i--){
        printf("%d ",num[i]);
    }
    printf("%d\n",num[0]);
    return 0;
}
```



### 28.ACM_1027_yue2

```c
//写两个函数，分别求两个整数的最大公约数和最小公倍数，用主函数调用这两个函数，并输出结果两个整数由键盘输入。

#include<stdio.h>

int dayue(int x,int y);
int xiaobei(int x,int y,int yue);

int main(){
    int x,y,yue,bei,t;
    scanf("%d %d",&x,&y);
    if(x>y){t=x;x=y;y=t;}
    yue = dayue(x, y);
    bei = xiaobei(x, y, yue);
    printf("%d %d\n",yue,bei);
    return 0;
}


int dayue(int x,int y){
    int n;
    while(y%x){
        n=x;
        x=y%x;
        y=n;
    }
    return x;
}
int xiaobei(int x,int y,int yue){
    int n;
    n = x*y/yue;
    return n;
}
```



### 29.ACM_1028_gen

```c
#include<stdio.h>
#include<math.h>

void dayu(double a,double b,double c);
void dengyu(double a,double b,double c);
void xiaoyu(double a,double b,double c);

int main(){
    float a,b,c,d;
    scanf("%f %f %f",&a,&b,&c);
    d = b*b - 4.0*a*c;
    if(d>0)dayu(a,b,c);
    else if(d==0)dengyu(a,b,c);
    else if(d<0)xiaoyu(a,b,c);
    else printf("error\n");
    return 0;
}

void dayu(double a,double b,double c){
    double x1,x2;
    x1=(0.0-b+sqrt(b*b-4.0*a*c))/(2.0*a);
    x2=(0.0-b-sqrt(b*b-4.0*a*c))/(2.0*a);
    printf("x1=%.3lf x2=%.3lf\n",x1,x2);
}
void dengyu(double a,double b,double c){
    dayu(a,b,c);
}
void xiaoyu(double a,double b,double c){
    double r,i;
    r = (0.0-b)/(2.0*a);
    i = (sqrt(4.0*a*c-b*b))/(2.0*a);
    printf("x1=%.3lf+%.3lfi x2=%.3lf-%.3lfi\n",r,i,r,i);
}
```



### 30.ACM_1029_sushu2

```c
#include<stdio.h>

int is_prime(int x);

int main(){
    int x,flag;
    scanf("%d",&x);
    flag=is_prime(x);
    if(flag>1)printf("not prime\n");
    else printf("prime\n");
    return 0;
}

int is_prime(int x){
    int flag = 0;
    for(int i=1;i<=x/2;i++){
        if(x%i==0){
//            printf("%d\n",i);
            flag++;
        }
    }
    return flag;
}
```



### 31.ACM_1030_3x3zz

```c
//写一个函数，使给定的一个二维数组（３×３）转置，即行列互换。
#include<stdio.h>

void zz(int num[3][3]);

int main(){
    int num[3][3];
    for(int i =0;i<3;i++)
    {
        for(int j=0;j<3;j++)
        {
            scanf("%d",&num[i][j]);
        }
    }
    zz(num);
    for(int i =0;i<3;i++)//输出
    {
        for(int j=0;j<3;j++)
        {
            if(j==2)printf("%d",num[i][j]);
            else printf("%d ",num[i][j]);
        }
        printf("\n");
    }
    return 0;
}

void zz(int num[3][3]){
    int t;
    for(int i =0;i<3;i++)
    {
        for(int j=0;j<i;j++)
        {
            t=num[i][j];
            num[i][j]=num[j][i];
            num[j][i]=t;
        }
    }
}
```



### 32.ACM_1031_fanstr

```c
//写一函数，使输入的一个字符串按反序存放，在主函数中输入输出反序后的字符串。
#include<stdio.h>
#include<string.h>

int main(){
    char str[50]={0};
    gets(str);
    for(int i = (strlen(str)-1);i>=0;i--){
        printf("%c",str[i]);
    }
    printf("\n");
    return 0;
}
```



### 33.ACM_1032_addstr

```c
/*写一函数，将两个字符串连接两行字符串
123
abc
123abc
*/
#include<stdio.h>
#include<string.h>

int main(){
    char str[100]={0};
    char str2[50]={0};
    gets(str);
    gets(str2);
    strcat(str,str2);
    puts(str);
    return 0;
}
```



### 34.ACM_1033_aeiuo

```c
//写一函数，将字符串中的元音字母复制到另一个字符串，然后输出。
#include<stdio.h>
#include<string.h>

void yuan(char a[],char b[]);

int main(){
    char a[50]={0};
    char b[50]={0};
    gets(a);
    yuan(a,b);
    puts(b);
    return 0;
}

void yuan(char a[],char b[]){
    int i=0,j=0;
    for(i=0;i<strlen(a);i++){
        if((a[i]=='a')||(a[i]=='e')||(a[i]=='i')||(a[i]=='o')||(a[i]=='u')){
            b[j]=a[i];
            j++;
        }
    }
    b[j]='\0';
}
```



### 35.ACM_1034_1990

```c
//写一函数，输入一个四位数字，要求输出这四个数字字符，但每两个数字间空格。如输入1990，应输出"1 9 9 0"。
#include<stdio.h>
#include<string.h>

void add_s(char a[],char b[]);

int main(){
    char a[50]={0};
    char b[50]={0};
    gets(a);
    add_s(a,b);
    puts(b);
    return 0;
}

void add_s(char a[],char b[])
{
    int i=0,j=0;
    for(i=0;i<(strlen(a)-1);i++){
        b[j]=a[i];j++;
        b[j]=' ';j++;
    }
    b[j]=a[(strlen(a)-1)];
}
```



### 36.ACM_1035_jishu2

```c
//编写一函数，由实参传来一个字符串，统计此字符串中字母、数字、空格和其它字符的个数，在主函数中输入字符串以及输出上述结果。
#include<stdio.h>
#include<string.h>

int E_num=0,N_num=0,S_num=0,O_num=0;
void count(char str[]);
int main(){
    char str[50];
    gets(str);
    count(str);
    printf("%d %d %d %d\n",E_num,N_num,S_num,O_num);
    
    return 0;
}
void count(char str[]){
    for(int i=0;i<(strlen(str));i++)
    {
        if(('a'<=str[i])&&(str[i]<='z')) E_num++;
        else if(('A'<=str[i])&&(str[i]<='Z')) E_num++;
        else if(('0'<=str[i])&&(str[i]<='9')) N_num++;
        else if(str[i]==' ') S_num++;
        else O_num++;
    }
}
```



### 37.ACM_1036_hong

```c
//定义一个带参的宏，使两个参数的值互换，并写出程序，输入两个数作为使用宏时的实参。输出已交换后的两个值。
#include<stdio.h>
int main(){
    int x,y,z;
    scanf("%d %d",&x,&y);
    CHANGE(x,y,z);
    printf("%d %d\n",x,y);
    return 0;
}
```



### 38.ACM_1037_hong2

```c
//输入两个整数，求他们相除的余数。用带参的宏来实现，编程序。
#include<stdio.h>

#define YU(a,b) a%b;

int main(){
    int a,b,c;
    scanf("%d%d",&a,&b);
    c=YU(a,b);
    printf("%d\n",c);
    return 0;
}
```



### 39.ACM_1038_hong3

```c
//三角形面积=SQRT(S*(S-a)*(S-b)*(S-c))其中S=(a+b+c)/2，a、b、c为三角形的三边。定义两个带参的宏，一个用来求area，另一个宏用来求S。写程序，在程序中用带实参的宏名来求面积area。
#include<stdio.h>
#include<math.h>

#define S(a,b,c) (a+b+c)/2.0
#define AREA(s,a,b,c) (sqrtf(s*(s-a)*(s-b)*(s-c)))

int main(){
    int a,b,c;
    float s,area;
    scanf("%d%d%d",&a,&b,&c);
    s=S(a,b,c);
    area=AREA(s, a, b, c);
    printf("%.3f\n",area);
    
    return 0;
}
```



### 40.ACM_1039_hong4

```c
//给年份year，定义一个宏，以判别该年份是否闰年。提示：宏名可以定义为LEAP_YEAR，形参为y，既定义宏的形式为  #define LEAP_YEAR(y) （读者设计的字符串）
#include<stdio.h>

#define LEAP_YEAR(y) ( (y%400==0) || ((y%4==0)&&(y%100!=0)) )

int main(){
    int y,flag;
    scanf("%d",&y);
    flag = LEAP_YEAR(y);
    if(flag) printf("L\n");
    else printf("N\n");
    return 0;
}
```



### 41.ACM_1040_6.2f

```c
//请设计输出实数的格式，包括：⑴一行输出一个实数；⑵一行内输出两个实数；⑶一行内输出三个实数。实数用"6.2f"格式输出。
#include<stdio.h>
int main(){
    float n;
    scanf("%f",&n);
    printf("%6.2f\n",n);
    printf("%6.2f%6.2f\n",n,n);
    printf("%6.2f%6.2f%6.2f\n",n,n,n);
    return 0;
}
```



### 42.ACM_1041_hong6

```c
//分别用函数和带参的宏，从三个数中找出最大的数。
#include<stdio.h>
#define DEFINEMAX(a,b,c,d) {d=(a>b)?a:b;d=(d>c)?d:c;}

float Max(float a,float b,float c);

int main(){
    float a,b,c,d,e;
    scanf("%f%f%f",&a,&b,&c);
    DEFINEMAX(a, b, c, d);
    e=Max(a, b, c);
    printf("%.3f\n%.3f\n",d,e);
    return 0;
}

float Max(float a,float b,float c){
    float d;
    d=(a>b)?a:b;
    d=(d>c)?d:c;
    return d;
}
```



### 43.ACM_1042_a2b

```c
//输入一行电报文字，将字母变成其下一字母（如’a’变成’b’……’z’变成’ａ’其它字符不变）。
#include<stdio.h>
#include<string.h>

int main(){
    char str[50];
    gets(str);
    for(int i=0;i<strlen(str);i++){
        if(('a'<=str[i])&&(str[i]<='y')) str[i]=str[i]+1;
        else if(str[i]=='z') str[i]='a';
        else if(('A'<=str[i])&&(str[i]<='Y')) str[i]=str[i]+1;
        else if(str[i]=='Z') str[i]='A';
    }
    puts(str);
    return 0;
}
```



### 44.ACM_1043_shunxu

```c
//输入三个整数，按由小到大的顺序输出。
#include<stdio.h>

int main(){
    int a,b,c,t;
    scanf("%d %d %d",&a,&b,&c);
    if(a>b){t=a;a=b;b=t;}
    if(b>c){t=b;b=c;c=t;}
    if(a>b){t=a;a=b;b=t;}
    printf("%d %d %d \n",a,b,c);
    return 0;
}
```



### 45.ACM_1044_strsx

```c
//输入三个字符串，按由小到大的顺序输出 strcmp strcpy
#include<stdio.h>
#include<string.h>
int main()
{
    char a[10]={0}, b[10]={0}, c[10]={0}, t[10]={0};
    gets(a);
    gets(b);
    gets(c);
    if(strcmp(a, b) > 0)
    {
        strcpy(t, a);
        strcpy(a, b);
        strcpy(b, t);
    }
    if(strcmp(b, c) > 0)
    {
        strcpy(t, b);
        strcpy(b, c);
        strcpy(c, t);
    }
    if(strcmp(a, b) > 0)
    {
        strcpy(t, a);
        strcpy(a, b);
        strcpy(b, t);
    }
    puts(a);
    puts(b);
    puts(c);
    return 0;
}
```



### 46.ACM_1045_1to10

```c
//输入10个整数，将其中最小的数与第一个数对换，把最大的数与最后一个数对换。写三个函数；①输入10个数；②进行处理；③输出10个数。
#include<stdio.h>

void input(int num[11]);
void change(int num[11]);
void ouput(int num[11]);

int main(){
    int num[11];
    input(num);
    change(num);
    ouput(num);
    return 0;
}

void input(int num[11]){
    for(int i=0;i<10;i++){
        scanf("%d",&num[i]);
    }
}
void change(int num[11]){
    int t,a;
    t=0;
    for(int i=1;i<10;i++){
        if(num[t]>num[i]){
            t=i;
        }
    }
    a=num[0];num[0]=num[t];num[t]=a;
    
    t=10;
    for(int i=0;i<9;i++){
        if(num[t]<num[i]){
            t=i;
        }
    }
    a=num[9];num[9]=num[t];num[t]=a;
}
void ouput(int num[11]){
    for(int i=0;i<10;i++){
        printf("%d ",num[i]);
    }
    printf("\n");
}
```



### 47.ACM_1046_nm

```c
//有n个整数，使前面各数顺序向后移m个位置，最后m个数变成前面m个数，见图。写一函数：实现以上功能，在主函数中输入n个数和输出调整后的n个数。
#include<stdio.h>

int main(){
    int num1[50]={0},num2[50]={0};
    int n=0,m=0,i=0,j=0;
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%d",&num1[i]);
    }
    scanf("%d",&m);
    for(i=n-m;i<n;i++){
        num2[j++]=num1[i];
    }
    for(i=0;i<n-m;i++){
        num2[j++]=num1[i];
    }
    for(i=0;i<n;i++){
        printf("%d ",num2[i]);
    }
    printf("\n");
    return 0;
}
```



### 48.ACM_1047_3ntui

```c
//有n人围成一圈，顺序排号。从第1个人开始报数（从1到3报数），凡报到3的人退出圈子，问最后留下的是原来的第几号的那位。
#include<stdio.h>

int main(){
    int n=0,num[100]={0},i=0,cnt=0,j=0;
    scanf("%d",&n);
    for(i=1;i<=n;i++){num[i]=1;}//所有都赋值1，表示还在队伍中
    i=1;
    while(1){
        if(num[i]!=0){
            if(j==i){break;}
            else{cnt++;j=i;}//记录下当前的序号，与上一次比较，如果是同一个，就是最后一个
            if(cnt==3) {
                num[i]=0;//标记为0，表示被t出队伍
                cnt=0;//同时计数归零
            }
        }
        if(i==n) i=1;
        else i++;
    }
    printf("%d\n",j);
    return 0;
}
```



### 49.ACM_1048_strcopy

```c
//有一字符串，包含n个字符。写一函数，将此字符串中从第m个字符开始的全部字符复制成为另一个字符串。
#include<stdio.h>

void strcopy(char str1[], char str2[],int n,int m);

int main(){
    int n,m,i=0;
    char str1[50]={0},str2[50]={0};
    scanf("%d",&n);
    for(i=0;i<=n;i++){
        scanf("%c",&str1[i]);
    }
    scanf("%d",&m);
    strcopy(str1,str2,n,m);
    puts(str2);
    return 0;
}

void strcopy(char str1[], char str2[],int n,int m){
    int i=0,j=0;
    for(i=m;i<=n;i++){
        str2[j++]=str1[i];
    }
}
```



### 50.ACM_1049_ymd

```c
//定义一个结构体变量（包括年、月、日）。计算该日在本年中是第几天，注意闰年问题。 
#include<stdio.h>
#define LEAP_YEAR(y) ( (y%400==0) || ((y%4==0)&&(y%100!=0)) )

int main(){
    struct date{
        int year;
        int month;
        int day;
    }date_1;
    int all=0;
    scanf("%d%d%d",&date_1.year,&date_1.month,&date_1.day);
    switch(date_1.month){
        case 12:all+=30;
        case 11:all+=31;
        case 10:all+=30;
        case 9:all+=31;
        case 8:all+=31;
        case 7:all+=30;
        case 6:all+=31;
        case 5:all+=30;
        case 4:all+=31;
        case 3:all+=28;
        case 2:all+=31;
        case 1: ;
    }
    all+=date_1.day;
    if((LEAP_YEAR(date_1.year) && (date_1.month>2))) all++;
    printf("%d\n",all);
    return 0;
}
```



### 51.ACM_1050_student

```c
//现有有N个学生的数据记录，每个记录包括学号、姓名、三科成绩。
//编写一个函数input,用来输入一个学生的数据记录。
//编写一个函数print,打印一个学生的数据记录。
//在主函数调用这两个函数，读取N条记录输入，再按要求输出。

#include<stdio.h>

struct stu{
    char num[20];
    char name[10];
    int grade_a;
    int grade_b;
    int grade_c;
}students[50];

void input(struct stu *st,int N);
void print(struct stu *st,int N);

int main(){
    int N=0;
    scanf("%d",&N);
    input(students,N);
    print(students,N);
    return 0;
}

void input(struct stu *st,int N){
    for(int i=0;i<N;i++){
        scanf("%s %s %d %d %d", st->num, st->name, &st->grade_a, &st->grade_b, &st->grade_c);
        st++;
    }
}
void print(struct stu *st,int N){
    for(int i=0;i<N;i++){
        printf("%s,%s,%d,%d,%d\n", st->num, st->name, st->grade_a, st->grade_b, st->grade_c);
        st++;
    }
}
```

