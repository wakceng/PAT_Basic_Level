## 1073-1080

### PAT-1073多选题常见计分法

```c
/*批改多选题是比较麻烦的事情，有很多不同的计分方法。有一种最常见的计分方法是：如果考生选择了部分正确选项，并且没有选择任何错误选项，则得到50%分数；如果考生选择了任何一个错误的选项，则不能得分。本题就请你写个程序帮助老师批改多选题，并且指出哪道题的哪个选项错的人最多。
 输入格式：
 输入在第一行给出两个正整数 N（≤1000）和 M（≤100），分别是学生人数和多选题的个数。随后 M 行，每行顺次给出一道题的满分值（不超过 5 的正整数）、选项个数（不少于 2 且不超过 5 的正整数）、正确选项个数（不超过选项个数的正整数）、所有正确选项。注意每题的选项从小写英文字母 a 开始顺次排列。各项间以 1 个空格分隔。最后 N 行，每行给出一个学生的答题情况，其每题答案格式为 (选中的选项个数选项1……)，按题目顺序给出。注意：题目保证学生的答题情况是合法的，即不存在选中的选项数超过实际选项数的情况。
 输出格式：
 按照输入的顺序给出每个学生的得分，每个分数占一行，输出小数点后1位。最后输出错得最多的题目选项的信息，格式为：错误次数题目编号（题目按照输入的顺序从1开始编号）-选项号。如果有并列，则每行一个选项，按题目编号递增顺序输出；再并列则按选项号递增顺序输出。行首尾不得有多余空格。如果所有题目都没有人错，则在最后一行输出 Too simple。
 输入样例 1：
3 4
3 4 2 a c
2 5 1 b
5 3 2 b c
1 5 4 a b d e
(2 a c) (3 b d e) (2 a c) (3 a b e)
(2 a c) (1 b) (2 a b) (4 a b d e)
(2 b d) (1 e) (1 c) (4 a b c d)
 输出样例 1：
 3.5
 6.0
 2.5
 2 2-e
 2 3-a
 2 3-b
 输入样例 2：
2 2
3 4 2 a c
2 5 1 b
(2 a c) (1 b)
(2 a c) (1 b)
 输出样例 2：
 5.0
 5.0
 Too simple
 */

/*
 * （该题为 1058. 选择题 的基础上，增加了 选择部分正确选项&没选错误选项，则得到50%分数的判断）
 */
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int score;//满分值
    int cnt;//2 <= 选项个数 <= 5
    int right_cnt;//正确选项的个数
    int opt[5];//下标代表选项
} question;
int main() {
    int N, M;//学学生人数、多选题的个数
    scanf("%d %d", &N, &M);
    question q[M];
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < 5; j++) {
            q[i].opt[j] = 0;
        }
    }
    for (int i = 0; i < M; i++) {//给出多选题
        scanf("%d %d %d", &q[i].score, &q[i].cnt, &q[i].right_cnt);
        char c;
        for (int j = 0; j < q[i].right_cnt; j++) {
            scanf(" %c", &c);
            q[i].opt[c-'a']++;//记录答案
        }
    }
    int error[M][5], max_error = 0;
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < 5; j++) {
            error[i][j] = 0;//错误次数
        }
    }
    for (int i = 0; i < N; i++) { //学生答题情况
        getchar();
        double grades = 0.0;
        for (int j = 0; j < M; j++) { //每一道题的答案
            int opt_cnt, isRight = 1, isAllRight = 1;//选择的数量, 选项是否正确
            char c;
            int opt_stu[5] = {0};
            scanf("(%d", &opt_cnt);
            for (int k = 0; k < opt_cnt; k++) {
                scanf(" %c", &c);
                opt_stu[c-'a'] = 1;//选择了该选项
            }
            for (int k = 0; k < 5; k++) {
                if(q[j].opt[k] == 1 && opt_stu[k] == 0) {//答案有， 没选该答案
                    isAllRight = 0;
                    error[j][k]++;
                } else if (q[j].opt[k] == 0 && opt_stu[k] == 1) {//答案没有，选了该答案，不得分
                    isRight = 0;
                    error[j][k]++;
                }
                if (max_error < error[j][k]) {
                    max_error = error[j][k];
                }
            }
            scanf(")");
            if (j != M - 1) {
                scanf(" ");
            }
            if (isRight) {//选项都正确
                if (!isAllRight) {//选择的数量 少于正确答案
                    grades += q[j].score / 2.0;
                } else {//选择的数量 等于 正确答案
                    grades += q[j].score;
                }
            }
        }
        printf("%.1f\n", grades);
    }
    if (max_error == 0) {
        printf("Too simple\n");
    } else {
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < 5; j++) {
                if (error[i][j] == max_error) {
                    printf("%d %d-%c\n", error[i][j], i+1, 'a'+j);
                }
            }
        }
    }
    return 0;
}
```



### PAT_1074宇宙无敌加法器

```c
/*
 地球人习惯使用十进制数，并且默认一个数字的每一位都是十进制的。而在 PAT 星人开挂的世界里，每个数字的每一位都是不同进制的，这种神奇的数字称为“PAT数”。每个 PAT 星人都必须熟记各位数字的进制表，例如“……0527”就表示最低位是 7 进制数、第 2 位是 2 进制数、第 3 位是 5 进制数、第 4 位是 10 进制数，等等。每一位的进制 d 或者是 0（表示十进制）、或者是 [2，9] 区间内的整数。理论上这个进制表应该包含无穷多位数字，但从实际应用出发，PAT 星人通常只需要记住前 20 位就够用了，以后各位默认为 10 进制。
 在这样的数字系统中，即使是简单的加法运算也变得不简单。例如对应进制表“0527”，该如何计算“6203 + 415”呢？我们得首先计算最低位：3 + 5 = 8；因为最低位是 7 进制的，所以我们得到 1 和 1 个进位。第 2 位是：0 + 1 + 1（进位）= 2；因为此位是 2 进制的，所以我们得到 0 和 1 个进位。第 3 位是：2 + 4 + 1（进位）= 7；因为此位是 5 进制的，所以我们得到 2 和 1 个进位。第 4 位是：6 + 1（进位）= 7；因为此位是 10 进制的，所以我们就得到 7。最后我们得到：6203 + 415 = 7201。
 输入格式：
 输入首先在第一行给出一个 N 位的进制表（0 < N ≤ 20），以回车结束。 随后两行，每行给出一个不超过 N 位的非负的 PAT 数。
 输出格式：
 在一行中输出两个 PAT 数之和。
 输入样例
30527
06203
415
 输出样例：
 7201
 */

#include<stdio.h>
#include<string.h>

int main(){
    char jinzhi[21],num1[21],num2[21],temp[21],result[21];
    scanf("%s%s%s",jinzhi,num1,num2);
    if(strlen(num2)>strlen(num1)){
        strcpy(temp,num1);strcpy(num1,num2);strcpy(num2,temp);
    }
    int index,len1,len2,t=0;//指针
    int n1,n2,jz,d=0,re;//jz进制，d进位,re结果
    index=strlen(jinzhi)-1;
    len1=strlen(num1)-1;len2=strlen(num2)-1;
    while(len1>=0 && len2>=0){
        n1=num1[len1]-'0';n2=num2[len2]-'0';
        jz=jinzhi[index]-'0';  if(jz==0) jz=10;
        re=(n1+n2+d)%jz;d=(n1+n2+d)/jz;
        result[t++]=re+'0';
        len1--;len2--;index--;
    }
    while(len1>=0){
        n1=num1[len1]-'0';
        jz=jinzhi[index]-'0';  if(jz==0) jz=10;
        re=(n1+d)%jz;d=(n1+d)/jz;
        result[t++]=re+'0';
        len1--;index--;
    }
    result[t++]=d+'0';
    int flag=1;
    while(t--){
        if(result[t]=='0' && flag){continue;}
        else{printf("%c",result[t]);flag=0;}
    }
    if(flag) printf("0");
    
    return 0;
}
```

```
注意当答案为全0时的情况，注意最后一位如果也有进位，记得把它加上。
```



### PAT_1075链表元素分类

```c
/*
 给定一个单链表，请编写程序将链表元素进行分类排列，使得所有负值元素都排在非负值元素的前面，而 [0, K] 区间内的元素都排在大于 K 的元素前面。但每一类内部元素的顺序是不能改变的。例如：给定链表为 18→7→-4→0→5→-6→10→11→-2，K 为 10，则输出应该为 -4→-6→-2→7→0→5→10→18→11。
 输入格式：
 每个输入包含一个测试用例。每个测试用例第 1 行给出：第 1 个结点的地址；结点总个数，即正整数N (≤105
  )；以及正整数K (≤103)。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。
 接下来有 N 行，每行格式为：
 Address Data Next
 其中 Address 是结点地址；Data 是该结点保存的数据，为 [−105,105] 区间内的整数；Next 是下一结点的地址。题目保证给出的链表不为空。
 输出格式：
 对每个测试用例，按链表从头到尾的顺序输出重排后的结果链表，其上每个结点占一行，格式与输入相同。
 输入样例：
00100 9 10
23333 10 27777
00000 0 99999
00100 18 12309
68237 -6 23333
33218 -4 00000
48652 -2 -1
99999 5 68237
27777 11 48652
12309 7 33218
 输出样例：
 33218 -4 68237
 68237 -6 48652
 48652 -2 12309
 12309 7 00000
 00000 0 99999
 99999 5 23333
 23333 10 00100
 00100 18 27777
 27777 11 -1
 */


#include<stdio.h>
 
typedef struct Node
{
    int data;
    int next;
}Node;

int main(){
    int first,n,k,mark;
    scanf("%d%d%d",&first,&n,&k);
    mark=first;
    
    int add=0,data=0,next=0;
    Node node[100000];
    
    for(int i=0;i<n;i++){
        scanf("%d%d%d",&add,&data,&next);
        node[add].data = data;
        node[add].next = next;
    }
    
    Node resu[100000];
    int arr[100000],index=0;
    for(int i=0;i<n;i++){
        if(node[first].data<0){
            if(index>0){
                resu[index-1].next=first;
            }
            arr[index]=first;
            resu[index++].data=node[first].data;
        }
        if(-1==node[first].next) break;
        first=node[first].next;
    }
    
    first=mark;
    for(int i=0;i<n;i++){
        if(node[first].data>=0 && k>=node[first].data){
            if(index>0){
                resu[index-1].next=first;
            }
            arr[index]=first;
            resu[index++].data=node[first].data;
        }
        if(-1==node[first].next) break;
        first=node[first].next;
    }
    
    first=mark;
    for(int i=0;i<n;i++){
        if(node[first].data>k){
            if(index>0){
                resu[index-1].next=first;
            }
            arr[index]=first;
            resu[index++].data=node[first].data;
        }
        if(-1==node[first].next) break;
        first = node[first].next;
    }
    
    for(int i = 0 ; i < index-1 ; i++)
    {
        printf("%05d %d %05d\n",arr[i],resu[i].data,resu[i].next);
    }
        printf("%05d %d -1\n",arr[index-1],resu[index-1].data);

    
    return 0;
}
```



### PAT_1076Wifi密码

```c
/*
 输入第一行给出一个正整数 N（≤ 100），随后 N 行，每行按照 编号-答案 的格式给出一道题的 4 个选项，T 表示正确选项，F 表示错误选项。选项间用空格分隔。
 输出格式：
 在一行中输出 wifi 密码。
 输入样例：
8
A-T B-F C-F D-F
C-T B-F A-F D-F
A-F D-F C-F B-T
B-T A-F C-F D-F
B-F D-T A-F C-F
A-T C-F B-F D-F
D-T B-F C-F A-F
C-T A-F B-F D-F
 输出样例：
 13224143
 */

#include<stdio.h>
#include<string.h>

int main(){
    int n;
    int i,j,index=0;
    scanf("%d",&n);
    char s[6],code[105];
    for(i=0;i<n;i++){
        for(j=0;j<4;j++){
            scanf("%s",s);
            if(strcmp(s,"A-T")==0) code[index++]='1';
            else if(strcmp(s,"B-T")==0) code[index++]='2';
            else if(strcmp(s,"C-T")==0) code[index++]='3';
            else if(strcmp(s,"D-T")==0) code[index++]='4';
        }
    }
    code[index]='\0';/////////IMPORTANT
    printf("%s\n",code);
    return 0;
}
```



### PAT_1077互评成绩计算

```c
/*
 在浙大的计算机专业课中，经常有互评分组报告这个环节。一个组上台介绍自己的工作，其他组在台下为其表现评分。最后这个组的互评成绩是这样计算的：所有其他组的评分中，去掉一个最高分和一个最低分，剩下的分数取平均分记为 G1；老师给这个组的评分记为G2。该组得分(G1+G2)/2，最后结果四舍五入后保留整数分。本题就要求你写个程序帮助老师计算每个组的互评成绩。
 输入格式：
 输入第一行给出两个正整数 N（> 3）和 M，分别是分组数和满分，均不超过 100。随后 N 行，每行给出该组得到的 N 个分数（均保证为整型范围内的整数），其中第 1 个是老师给出的评分，后面 N−1 个是其他组给的评分。合法的输入应该是 [0,M] 区间内的整数，若不在合法区间内，则该分数须被忽略。题目保证老师的评分都是合法的，并且每个组至少会有 3 个来自同学的合法评分。
 输出格式：
 为每个组输出其最终得分。每个得分占一行。
 输入样例：
6 50
42 49 49 35 38 41
36 51 50 28 -1 30
40 36 41 33 47 49
30 250 -25 27 45 31
48 0 0 50 50 1234
43 41 36 29 42 29
 输出样例：
 42
 33
 41
 31
 37
 39
 */

#include<stdio.h>

void Qsort(int a[],int L,int R);

int main(){
    int n,m;
    scanf("%d%d",&n,&m);
    int i,index,j,G2,g1,g[105],sum,count;
    for(i=0;i<n;i++){
        scanf("%d",&G2);
        index=0;
        sum=0;count=0;
        for(j=0;j<n-1;j++){
            scanf("%d",&g1);
            if(0<=g1 && g1<=m) g[index++]=g1;
        }
        Qsort(g, 0, index-1);
        for(j=1;j<index-1;j++){sum+=g[j];count++;}
        sum=((1.0*sum/count)+G2)/2+0.5;
        printf("%d\n",sum);
    }
    
    return 0;
}

void Qsort(int a[],int L,int R){
    if(L>=R) return;
    int i=L,j=R;
    int temp;
    int key=a[L];
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



### PAT_1078字符串压缩与解压

```c
/*
 文本压缩有很多种方法，这里我们只考虑最简单的一种：把由相同字符组成的一个连续的片段用这个字符和片段中含有这个字符的个数来表示。例如 ccccc 就用 5c 来表示。如果字符没有重复，就原样输出。例如 aba 压缩后仍然是 aba。
 解压方法就是反过来，把形如 5c 这样的表示恢复为 ccccc。
 本题需要你根据压缩或解压的要求，对给定字符串进行处理。这里我们简单地假设原始字符串是完全由英文字母和空格组成的非空字符串。
 输入格式：
 输入第一行给出一个字符，如果是C就表示下面的字符串需要被压缩；如果是D就表示下面的字符串需要被解压。第二行给出需要被压缩或解压的不超过1000个字符的字符串，回车结尾。题目保证字符重复个数在整型范围内，且输出文件不超过 1MB。
 输出格式：
 根据要求压缩或解压字符串，并在一行中输出结果。
 输入样例 1：
C
TTTTThhiiiis isssss a   tesssst CAaaa as
输出样例 1：
5T2h4is i5s a3 te4st CA3a as
输入样例 2：
D
5T2h4is i5s a3 te4st CA3a as10Z
 输出样例 2：
 TTTTThhiiiis isssss a   tesssst CAaaa asZZZZZZZZZZ
 */

#include<stdio.h>
#include<string.h>

void yasuo(char s[]);
void jieya(char s[]);
char s[10001]={"\0"},c,t=0;

int main(){
    char CD;
    CD=getchar();
    c=getchar();
//    while((c=getchar())!='\n'){
//        s[t++]=c;
//    }
//    s[t]='\0';
    gets(s);
    if(CD=='C') {yasuo(s);}//jieya(s);}
    else if(CD=='D') {jieya(s);}//yasuo(s);}
    return 0;
}

void yasuo(char s[]){
    int i=0,len,count;
    len=strlen(s);
    while(i<len){
        count=0;
        while(s[i]==s[i+count]){
            count++;
        }
//        printf("%d",count);
        if(count>1) printf("%d",count);
        printf("%c",s[i]);
        i+=count;
    }
    printf("\n");
}
void jieya(char s[]){
    int i=0,len,count=0,num=0,j;
    len=strlen(s);
    while(i<len){
        num=0;count=0;
        if('0'<=s[i] && s[i]<='9'){
            while('0'<=s[i+num] && s[i+num]<='9'){
                num++;
            }
            for(j=0;j<num;j++){
                count=count*10+s[i+j]-'0';
            }
            while(count--){
                printf("%c",s[i+num]);
            }
        }
        else printf("%c",s[i]);
        i+=num+1;
    }
    printf("\n");
}
```



### PAT_1079延迟的回文数

```c
/*
 给定一个 k+1 位的正整数 N，写成 a k  ⋯a 1  a 0   的形式，其中对所有 i 有 0≤a i  <10 且 a k  >0。N 被称为一个回文数，当且仅当对所有 i 有 a i  =a k−i  。零也被定义为一个回文数。
 非回文数也可以通过一系列操作变出回文数。首先将该数字逆转，再将逆转数与该数相加，如果和还不是一个回文数，就重复这个逆转再相加的操作，直到一个回文数出现。如果一个非回文数可以变出回文数，就称这个数为延迟的回文数。（定义翻译自 https://en.wikipedia.org/wiki/Palindromic_number ）
 给定任意一个正整数，本题要求你找到其变出的那个回文数。
 输入格式：
 输入在一行中给出一个不超过1000位的正整数。
 输出格式：
 对给定的整数，一行一行输出其变出回文数的过程。每行格式如下
 A + B = C
 其中 A 是原始的数字，B 是 A 的逆转数，C 是它们的和。A 从输入的整数开始。重复操作直到 C 在 10 步以内变成回文数，这时在一行中输出 C is a palindromic number.；或者如果 10 步都没能得到回文数，最后就在一行中输出 Not found in 10 iterations.。
 输入样例 1：
97152
 输出样例 1：
 97152 + 25179 = 122331
 122331 + 133221 = 255552
 255552 is a palindromic number.
*/

#include<stdio.h>
#include<string.h>

int isH(char n[]);//是回文就返回1
void getNX(char n1[],char n2[]);//得到n1的逆序

int main(){
    char n1[2005],n2[2005],temp[2005],n3[2005];
    int count=10,index,a,b,d=0,re,p,t=0;
    scanf("%s",n1);
    while(count--){
        strcpy(temp,n1);
        if(isH(temp)) break;
        getNX(n1,n2);
        printf("%s + %s = ",n1,n2);
        index=0;p=strlen(n1)-1;
        //a是n1的低位，b是n2的低位，re是两个相加的低位，d是两个相加的进位,p是数据的指针
        while(p>=0){
            a=n1[p]-'0';b=n2[p]-'0';
            re=(a+b+d)%10;d=(a+b+d)/10;
            n3[t++]=re+'0';
            p--;
        }
        if(d>0) n3[t++]=d+'0';///////////////// IMPORTANT!!!!!
        n3[t]='\0';//////////////////////////// IMPORTANT!!!!!
        getNX(n3,temp);
        printf("%s\n",temp);
        t=0;d=0;
        strcpy(n1,temp);
        if(isH(temp)) break;
    }
    if(isH(temp)) printf("%s is a palindromic number.\n",temp);
    else printf("Not found in 10 iterations.\n");
    
    return 0;
}

int isH(char n[]){
    int len,i;
    len=strlen(n);
    for(i=0;i<len/2;i++){
        if(n[i]!=n[len-1-i]) return 0;
    }
    return 1;
}
void getNX(char n1[],char n2[]){
    int len,i;
    len=strlen(n1);
    for(i=0;i<len;i++){
        n2[len-1-i]=n1[i];
    }
    n2[len]='\0';
}
```



### PAT_1080MOOC期终成绩

## qsort排列结构体bsearch二分法搜索

```c
/*对于在中国大学MOOC学习“数据结构”课程的学生，想要获得一张合格证书，必须首先获得不少于200分的在线编程作业分，然后总评获得不少于60分（满分100）。总评成绩的计算公式为 G=(G mid−term  ×40%+G final  ×60%)，如果 G mid−term  >G final  ；否则总评 G 就是 G final  。这里 G mid−term   和 G final   分别为学生的期中和期末成绩。现在的问题是，每次考试都产生一张独立的成绩单。本题就请你编写程序，把不同的成绩单合为一张。
 输入格式：
 输入在第一行给出3个整数，分别是P（做了在线编程作业的学生数）、M（参加了期中考试的学生数）、N（参加了期末考试的学生数）。每个数都不超过10000。接下来有三块输入。第一块包含 P 个在线编程成绩 G p  ；第二块包含 M 个期中考试成绩 G mid−term；第三块包含 N 个期末考试成绩 G final  。每个成绩占一行，格式为：学生学号 分数。其中学生学号为不超过20个字符的英文字母和数字；分数是非负整数（编程总分最高为900分，期中和期末的最高分为100分）。
 输出格式：
 打印出获得合格证书的学生名单。每个学生占一行，格式为：
 学生学号 G p   G mid−term   G final G如果有的成绩不存在（例如某人没参加期中考试），则在相应的位置输出“−1”。输出顺序为按照总评分数（四舍五入精确到整数）递减。若有并列，则按学号递增。题目保证学号没有重复，且至少存在1个合格的学生。
 输入样例：
6 6 7
01234 880
a1903 199
ydjh2 200
wehu8 300
dx86w 220
missing 400
ydhfu77 99
wehu8 55
ydjh2 98
dx86w 88
a1903 86
01234 39
ydhfu77 88
a1903 66
01234 58
wehu8 84
ydjh2 82
missing 99
dx86w 81
 输出样例：
 missing 400 -1 99 99
 ydjh2 200 98 82 88
 dx86w 220 88 81 84
 wehu8 300 55 84 84
 
 */


#include<stdio.h>
#include<string.h>
#include<stdlib.h>

typedef struct stu{
    char name[25];       /*储存学号*/
    int p;               /*储存在线编程成绩*/
    int m;               /*储存期中考试成绩*/
    int n;               /*储存期末成绩*/
    int zong;            /*储存期终成绩*/
    int check;           /*是否合格*/
}stu;


int comp1(const void* a,const void* b);    /*按照学号升序排列*/
int comp2(const void* a,const void* b);    /*排序总函数*/
int comp3(const void* a,const void* b);    /*按学号查找函数*/


int main(){
    int p,m,n,i=0,x=0;    /*储存各类考试成绩*/
    int mp,mm,mn;
    char name[25];
    stu a[100000];        /*这里是100000个学生*/
    stu *dent;
    scanf("%d %d %d",&p,&m,&n);
    while(p--){
        scanf("%s %d",name,&mp);
        strcpy(a[i].name,name);
        a[i].p=mp;
        a[i].m=-1;      /*其他两项成绩初始化，默认没有*/
        a[i].n=-1;
        i++;
    }
    qsort(a,i,sizeof(stu),comp1);
    
    
    while(m--){
        scanf("%s %d",name,&mm);
        dent=(stu*)bsearch(name,a,i,sizeof(stu),comp3);
        if(dent!=0)         /*若在线编程没有成绩，则一定不合格，不考虑*/
            dent->m=mm;
    }

    while(n--){
        scanf("%s %d",name,&mn);
        dent=(stu*)bsearch(name,a,i,sizeof(stu),comp1);
        if(dent!=0) dent->n=mn;
    }
    
    for(x=0;x<i;x++)      /*这个循环计算最终成绩，并判定是否合格*/
    {
        if(a[x].m<a[x].n){//如果 G mid−term  >G final  ；否则总评 G 就是 G final
            a[x].zong=a[x].n;
            if(a[x].zong>=60&&a[x].p>=200){
                a[x].check=1;
            }
            else a[x].check=0;
            continue;
        }
        a[x].zong=(int)(a[x].m*0.4+a[x].n*0.6+0.5);   /*四舍五入后储存*/
        if(a[x].zong+0.5>=60&&a[x].p>=200){a[x].check=1;}
        else a[x].check=0;
    }
    
    
    qsort(a,i,sizeof(stu),comp2);          /*排序*/
    for(x=0;x<i&&a[x].check==1;x++){
        printf("%s %d %d %d %d\n",a[x].name,a[x].p,a[x].m,a[x].n,a[x].zong);
    }
    
    
    return 0;
}

int comp1(const void* _a,const void* _b){
    stu* x=(stu*)_a;
    stu* y=(stu*)_b;
    return strcmp(x->name,y->name);
}
int comp3(const void* a,const void* b){
    char *x=(char*)a;
    stu *y=(stu*)b;
    return strcmp(x,y->name);        /*查找*/
}
int comp2(const void* a,const void* b){
    stu* x=(stu*)a;
    stu* y=(stu*)b;
    if(x->check != y->check)         /*合格在前*/
        return y->check - x->check;
    else if(x->zong != y->zong)     /*最终成绩高的在前*/
        return y->zong - x->zong;
    else                             /*按名字升序*/
        return strcmp(x->name,y->name);
}
```



## 1081-1090

### PAT_1081检查密码

```c
/*
 本题要求你帮助某网站的用户注册模块写一个密码合法性检查的小功能。该网站要求用户设置的密码必须由不少于6个字符组成，并且只能有英文字母、数字和小数点 .，还必须既有字母也有数字。
 输入第一行给出一个正整数 N（≤ 100），随后 N 行，每行给出一个用户设置的密码，为不超过 80 个字符的非空字符串，以回车结束。注意： 题目保证不存在只有小数点的输入。
 输出格式：
 对每个用户的密码，在一行中输出系统反馈信息，分以下5种：
 如果密码合法，输出Your password is wan mei.；
 如果密码太短，不论合法与否，都输出Your password is tai duan le.；
 如果密码长度合法，但存在不合法字符，则输出Your password is tai luan le.；
 如果密码长度合法，但只有字母没有数字，则输出Your password needs shu zi.；
 如果密码长度合法，但只有数字没有字母，则输出Your password needs zi mu.。
 输入样例：
5
123s
zheshi.wodepw
1234.5678
WanMei23333
pass*word.6
 输出样例：
 Your password is tai duan le.
 Your password needs shu zi.
 Your password needs zi mu.
 Your password is wan mei.
 Your password is tai luan le.
 */

#include<stdio.h>
#include<string.h>
#include<ctype.h>

int main(){
    char s[100];
    int n,cnt_num,cnt_eng,cnt_point,i;
    scanf("%d",&n);
    gets(s);
    while(n--){
        cnt_num=0;cnt_eng=0;cnt_point=0;
//        scanf("%s",s);
        gets(s);
        if(strlen(s)<6) {printf("Your password is tai duan le.\n");continue;}
        for(i=0;i<strlen(s);i++){
            if(isalpha(s[i])) cnt_eng++;
            else if('0'<=s[i] && s[i]<='9') cnt_num++;
            else if(s[i]=='.') cnt_point++;
        }
        if(cnt_eng+cnt_num+cnt_point != strlen(s)) {
            printf("Your password is tai luan le.\n");
            continue;
        }
        else if(cnt_eng==0 && cnt_num>0){
            printf("Your password needs zi mu.\n");
            continue;
        }
        else if(cnt_num==0 && cnt_eng>0){
            printf("Your password needs shu zi.\n");
            continue;
        }
        else{
            printf("Your password is wan mei.\n");
            continue;
        }
        
    }
    
    return 0;
}
```

```
可能会有空格输入，最好用gets
```



### PAT_1082射击比赛

```c
/*本题目给出的射击比赛的规则非常简单，谁打的弹洞距离靶心最近，谁就是冠军；谁差得最远，谁就是菜鸟。本题给出一系列弹洞的平面坐标(x,y)，请你编写程序找出冠军和菜鸟。我们假设靶心在原点(0,0)。
 输入格式：
 输入在第一行中给出一个正整数 N（≤ 10 000）。随后 N 行，每行按下列格式给出：
 ID x y其中 ID 是运动员的编号（由 4 位数字组成）；x 和 y 是其打出的弹洞的平面坐标(x,y)，均为整数，且 0 ≤ |x|, |y| ≤ 100。题目保证每个运动员的编号不重复，且每人只打 1 枪。
 输出格式：
 输出冠军和菜鸟的编号，中间空 1 格。题目保证他们是唯一的。
 输入样例：
3
0001 5 7
1020 -1 3
0233 0 -1
 输出样例：
 0233 0001
 */

#include<stdio.h>

int main(){
    int n;
    int max,min,x,y,max_id,min_id,id;
    scanf("%d",&n);
    if(n>0){
        scanf("%d%d%d",&id,&x,&y);
        max_id=id;min_id=id;
        min=max=x*x+y*y;
        n--;
    }
    else return 0;
    while(n--){
        scanf("%d%d%d",&id,&x,&y);
        if(max<x*x+y*y){
            max_id=id;max=x*x+y*y;
        }
        if(min>x*x+y*y){
            min_id=id;min=x*x+y*y;
        }
    }
    printf("%04d %04d\n",min_id,max_id);
    return 0;
}
```



### PAT_1083是否存在相等的差

```c
/*给定 N 张卡片，正面分别写上 1、2、……、N，然后全部翻面，洗牌，在背面分别写上 1、2、……、N。将每张牌的正反两面数字相减（大减小），得到 N 个非负差值，其中是否存在相等的差？
 输入格式：
 输入第一行给出一个正整数 N（2 ≤ N ≤ 10 000），随后一行给出 1 到 N 的一个洗牌后的排列，第 i 个数表示正面写了 i 的那张卡片背面的数字。
 输出格式：
 按照“差值 重复次数”的格式从大到小输出重复的差值及其重复的次数，每行输出一个结果。
 输入样例：
8
3 5 8 6 2 1 4 7
 输出样例：
 5 2
 3 3
 2 2
 */

#include<stdio.h>
#include<stdlib.h>
#include<math.h>

int main(){
    int n,num[10010],i,temp;
    scanf("%d",&n);
    for(i=0;i<=n;i++) num[i]=0;
    for(i=1;i<=n;i++){
        scanf("%d",&temp);
        temp=abs(temp-i);
        num[temp]++;
    }
    for(i=n;i>=0;i--){
        if(num[i]>1) printf("%d %d\n",i,num[i]);
    }
    return 0;
}
```



### PAT_1084外观数列

```c
/*外观数列是指具有以下特点的整数序列：
 d, d1, d111, d113, d11231, d112213111, ...
 它从不等于 1 的数字 d 开始，序列的第 n+1 项是对第 n 项的描述。比如第 2 项表示第 1 项有 1 个 d，所以就是 d1；第 2 项是 1 个 d（对应 d1）和 1 个 1（对应 11），所以第 3 项就是 d111。又比如第 4 项是 d113，其描述就是 1 个 d，2 个 1，1 个 3，所以下一项就是 d11231。当然这个定义对 d = 1 也成立。本题要求你推算任意给定数字 d 的外观数列的第 N 项。
 输入格式：
 输入第一行给出 [0,9] 范围内的一个整数 d、以及一个正整数 N（≤ 40），用空格分隔。
 输出格式：
 在一行中给出数字 d 的外观数列的第 N 项。
 输入样例：
 1 8
 输出样例：
 1123123111
 */

#include<stdio.h>
#include<string.h>

int main(){
    int n,index,i=0,len,cnt;
    char d;
    char s[100010],temp[100010];
    scanf("%c%d",&d,&n);
    s[0]= d;s[1]='\0';
    n--;
    while(n--){
        index=0;cnt=0;i=0;
        len=strlen(s);
        while(i<len){
            cnt=1;
            while(s[i+cnt]==s[i]){
                cnt++;
            }
            temp[index++]=s[i];
            temp[index++]=cnt+'0';
            i+=cnt;
        }
        temp[index++]='\0';
        strcpy(s,temp);
        
    }
    printf("%s\n",s);
    return 0;
}
```



### PAT_1085PAT_单位排名（qsort排列结构体

```c
/*输入第一行给出一个正整数 N（≤105），即考生人数。随后 N 行，每行按下列格式给出一个考生的信息：准考证号 得分 学校其中准考证号是由6个字符组成的字符串，其首字母表示考试的级别：B代表乙级，A代表甲级，T代表顶级；得分是 ,100]区间内的整数；学校是由不超过6个英文字母组成的单位码（大小写无关）。注意：题目保证每个考生的准考证号是不同的。
 首先在一行中输出单位个数。随后按以下格式非降序输出单位的排行榜：排名 学校 加权总分 考生人数
 其中排名是该单位的排名（从 1 开始）；学校是全部按小写字母输出的单位码；加权总分定义为乙级总分/1.5 + 甲级总分 + 顶级总分*1.5的整数部分；考生人数是该属于单位的考生的总人数。
 学校首先按加权总分排行。如有并列，则应对应相同的排名，并按考生人数升序输出。如果仍然并列，则按单位码的字典序输。
 输入样例：
10
A57908 85 Au
B57908 54 LanX
A37487 60 au
T28374 67 CMU
T32486 24 hypu
A66734 92 cmu
B76378 71 AU
A47780 45 lanx
A72809 100 pku
A03274 45 hypu
 输出样例：
 5
 1 cmu 192 2
 1 au 192 3
 3 pku 100 1
 4 hypu 81 2
 4 lanx 81 2
 */


#include<stdio.h>
#include<string.h>
#include<stdlib.h>
struct student{
    char id[6];//准考证号,由 6 个字符组成的字符串
    char grade;//记录考试等级
    int marks;//得分,是 [0, 100] 区间内的整数
    char school[7];//学校是由不超过 6 个英文字母组成的单位码(大小写无关)
};

struct university{
    char name[7];
    double temp_toal;
    int total;//加权总分=乙级总分/1.5 + 甲级总分 + 顶级总分*1.5的整数部分
    int num_s;//考生人数
};

int cmp_school(const void *a,const void *b){
    struct student c = *(struct student *)a;
    struct student d = *(struct student *)b;
    return strcmp(c.school,d.school);
}

int cmp(const void *a,const void *b){
    struct university c = *(struct university *)a;
    struct university d = *(struct university *)b;
    if (c.total!=d.total)
        return d.total-c.total;//总分降序
    else
    {
        if (c.num_s!=d.num_s)
            return c.num_s-d.num_s;//考生人数升序输出
        else
            return strcmp(c.name,d.name);//单位码的字典序输出
    }
}

int main(){
    int N,i,j,len,rank,k = 0;//k记录不同学校的数目
    scanf("%d\n",&N);
    struct student S[N];
    struct university U[N];
    for (i=0;i<N;i++)
    {
        U[i].num_s = 0;//初始化
        U[i].temp_toal = 0;
        scanf("%c%s %d %s\n",&S[i].grade,S[i].id,&S[i].marks,S[i].school);
        len = strlen(S[i].school);
        for (j=0;j<len;j++)
            if (S[i].school[j]>64 && S[i].school[j]<91)//大写字母
                S[i].school[j]+=32;//转为小写
    }
    qsort(S,N,sizeof(S[0]),cmp_school);//学校相同的排列在一起
    for (i=0;i<N;i++)
    {
        if (i!=0 && strcmp(S[i].school,U[k].name)!=0)
            k++;
        strcpy(U[k].name,S[i].school);
        U[k].num_s++;
        switch (S[i].grade)
        {
            case 'A':U[k].temp_toal+=S[i].marks;break;
            case 'B':U[k].temp_toal+=(S[i].marks/1.5);break;
            case 'T':U[k].temp_toal+=(S[i].marks*1.5);break;
        }
    }
    for (i=0;i<=k;i++)
        U[i].total = U[i].temp_toal;//去整数部分
    qsort(U,k+1,sizeof(U[0]),cmp);
    printf("%d\n",k+1);
    for (i=0;i<=k;i++)
    {
        if (i==0)
            rank = 1;
        else if (i!=0 && U[i].total!=U[i-1].total)
            rank = i+1;
        printf("%d %s %d %d\n",rank,U[i].name,U[i].total,U[i].num_s);
    }
    return 0;
}
```



### PAT_1086就不告诉你

```c
/*输入在第一行给出两个不超过 1000 的正整数 A 和 B，其间以空格分隔。
 输出格式：
 在一行中倒着输出 A 和 B 的乘积。
 输入样例：
 5 7
 输出样例：
 53
 */

#include<stdio.h>

int main(){
    int a,b,ji,num[1000],index=0,i;

    scanf("%d%d",&a,&b);
    ji=a*b;
    while(ji>=10){
        num[index++]=ji%10;
        ji/=10;
    }
    num[index++]=ji;
    int flag=1;
    for(i=0;i<index;i++){
        if(num[i]==0 && flag) continue;
        else{flag=0;printf("%d",num[i]);}
    }
    
    return 0;
}
```

```
注意如果是100*100=10000，反过来应该输出1，而不是00001。
```



### PAT_1087有多少不同的值

```c
/*当自然数 n 依次取 1、2、3、……、N 时，算式 ⌊n/2⌋+⌊n/3⌋+⌊n/5⌋ 有多少个不同的值？（注：⌊x⌋ 为取整函数，表示不超过 x 的最大自然数，即 x 的整数部分。）
 输入格式：
 输入给出一个正整数 N（2≤N≤104）。
 输出格式：
 在一行中输出题面中算式取到的不同值的个数。
 输入样例：
 2017
 输出样例：
 1480
*/

#include<stdio.h>

int main(){
    int n,i,sum,num[100010],cnt=0;
    scanf("%d",&n);
    for(i=0;i<n*1.5;i++){
        num[i]=0;
    }
    for(i=1;i<=n;i++){
        sum=i/2+i/3+i/5;
        num[sum]++;
    }
    for(i=0;i<n*1.5;i++){
        if(num[i]>0) cnt++;
    }
    printf("%d\n",cnt);
    return 0;
}
```



### PAT_1088三人行

```c
/*子曰：“三人行，必有我师焉。择其善者而从之，其不善者而改之。”
 本题给定甲、乙、丙三个人的能力值关系为：甲的能力值确定是 2 位正整数；把甲的能力值的 2 个数字调换位置就是乙的能力值；甲乙两人能力差是丙的能力值的 X 倍；乙的能力值是丙的 Y 倍。请你指出谁比你强应“从之”，谁比你弱应“改之”。
 输入格式：
 输入在一行中给出三个数，依次为：M（你自己的能力值）、X 和 Y。三个数字均为不超过 1000 的正整数。
 输出格式：
 在一行中首先输出甲的能力值，随后依次输出甲、乙、丙三人与你的关系：如果其比你强，输出 Cong；平等则输出 Ping；比你弱则输出 Gai。其间以 1 个空格分隔，行首尾不得有多余空格。
 注意：如果解不唯一，则以甲的最大解为准进行判断；如果解不存在，则输出 No Solution。
 输入样例 1：
 48 3 7
 输出样例 1：
 48 Ping Cong Gai
 输入样例 2：
 48 11 6
 输出样例 2：
 No Solution
 */

#include<stdio.h>
#include<stdlib.h>
#include<math.h>

int get_yi(int x);

int main(){
    int jia=99,yi=0,x,y,m;
    double bing=0;
    scanf("%d%d%d",&m,&x,&y);
    while(jia>9){
        yi=get_yi(jia);
        bing = 1.0*yi/y;
        if( y*abs(yi-jia)==x*yi && bing!=0 ) break;
        else jia--;
    }
    if(jia==9) {printf("No Solution\n");return 0;}
    printf("%d ",jia);
    if(m==jia) printf("Ping ");
    else if(m<jia) printf("Cong ");
    else if(m>jia) printf("Gai ");
    if(m==yi) printf("Ping ");
    else if(m<yi) printf("Cong ");
    else if(m>yi) printf("Gai ");
    if(m==bing) printf("Ping\n");
    else if(m<bing) printf("Cong\n");
    else if(m>bing) printf("Gai\n");
    
    return 0;
}

int get_yi(int x){
    int num;
    num = (x%10)*10+(x/10);
    return num;
}
```

```
丙可以是小数，只要等式成立即可
```



### PAT_1089狼人杀-简单版

```c
/*以下文字摘自《灵机一动·好玩的数学》：“狼人杀”游戏分为狼人、好人两大阵营。在一局“狼人杀”游戏中，1 号玩家说：“2 号是狼人”，2 号玩家说：“3 号是好人”，3 号玩家说：“4 号是狼人”，4 号玩家说：“5 号是好人”，5 号玩家说：“4 号是好人”。已知这 5 名玩家中有 2 人扮演狼人角色，有 2 人说的不是实话，有狼人撒谎但并不是所有狼人都在撒谎。扮演狼人角色的是哪两号玩家？
 本题是这个问题的升级版：已知 N 名玩家中有 2 人扮演狼人角色，有 2 人说的不是实话，有狼人撒谎但并不是所有狼人都在撒谎。要求你找出扮演狼人角色的是哪几号玩家？
 输入格式：
 输入在第一行中给出一个正整数 N（5≤N≤100）。随后 N 行，第 i 行给出第 i 号玩家说的话（1≤i≤N），即一个玩家编号，用正号表示好人，负号表示狼人。
 输出格式：
 如果有解，在一行中按递增顺序输出 2 个狼人的编号，其间以空格分隔，行首尾不得有多余空格。如果解不唯一，则输出最小序列解 —— 即对于两个序列 A=a[1],...,a[M] 和 B=b[1],...,b[M]，若存在 0≤k<M 使得 a[i]=b[i] （i≤k），且 a[k+1]<b[k+1]，则称序列 A 小于序列 B。若无解则输出 No Solution。
 输入样例 1：
5
-2
+3
-4
+5
+4
 输出样例 1：
 1 4
输入样例 2：
6
+6
+3
+1
-5
-2
+4
 输出样例 2（解不唯一）：
 1 5
 输入样例 3：
5
-2
-3
-4
-5
-1
 输出样例 3：
 No Solution
 
 5
1 -2 L sh
2 +3
3 -4   sh
4 +5   sh
5 +4 L
 */


#include<stdio.h>
#include<stdlib.h>
#include<math.h>

typedef struct lang{
    int no;//每个人的编号
    int speak;//表示这人说了什么
}lang;

int main(){
    int n,i,j,k;
    int all_lie,wolf_lie;//表示所有人说谎的次数、狼说谎的次数
    lang L[105];
    int langid[105],index=0;
    scanf("%d",&n);
    for(i=1;i<=n;i++) scanf("%d",&L[i].speak);
    
    for(i=1;i<=n;i++){
        for(j=i+1;j<=n;j++){//假设编号是ij的两个是狼
            all_lie=0;wolf_lie=0;
            for(k=1;k<=n;k++){//对每个人说的话进行判断
                if(k==i || k==j){//这人是狼
                    if(L[k].speak<0 && abs(L[k].speak)!=i && abs(L[k].speak)!=j){
                        //他说别人是狼，但那个人并不是狼
                        wolf_lie++;all_lie++;
                    }
                    else if(L[k].speak>0 && (L[k].speak==i || L[k].speak==j)){
                        //他说别人是好人，但是那人是狼
                        wolf_lie++;all_lie++;
                    }
                }
                else{//这人不是狼
                    if(L[k].speak<0 && abs(L[k].speak)!=i && abs(L[k].speak)!=j){
                        //他说别人是狼，但那个人并不是狼
                        all_lie++;
                    }
                    else if(L[k].speak>0 && (L[k].speak==i || L[k].speak==j)){
                        //他说别人是好人，但是那人是狼
                        all_lie++;
                    }
                }
            }
            //对说谎次数进行判断
            if(wolf_lie==1 && all_lie==2){
                langid[index++]=i;
                langid[index++]=j;
            }
        }
    }
//    for(i=0;i<index;i++) printf("%d\n",langid[i]);
    if(index==0) printf("No Solution\n");
    else printf("%d %d\n",langid[0],langid[1]);

    return 0;
}
```

```
他的最小序列只需要输出第一组狼人即可
100个中有两个狼人，两个人说谎，枚举两个狼人会比枚举两个说谎来的容易
```



### PAT_1090危险品装箱

```c
//暴力解，，，会超时
#include<stdio.h>

int main(){
    int n,m,i,j,k,FlagFind,x,y;
    int bz[10010][2];
    int list[1010];
    scanf("%d%d",&n,&m);
    for(i=0;i<n;i++){
        scanf("%d%d",&bz[i][0],&bz[i][1]);
    }
    for(i=0;i<m;i++){
        scanf("%d",&k);
        for(j=0;j<k;j++){
            scanf("%d",&list[j]);
        }
        
        FlagFind=0;
        for(j=0;j<k;j++){//对list中的所有元素遍历
            for(x=0;x<n;x++){//对会爆炸的所有元素遍历
                if(bz[x][0]==list[j]){
                    for(y=0;y<k;y++){
                        if(bz[x][1]==list[y]) FlagFind=1;
                    }
                }
            }
        }
        if(FlagFind) printf("No\n");
        else printf("Yse\n");
    }
    return 0;
}
```

```c
/*集装箱运输货物时，我们必须特别小心，不能把不相容的货物装在一只箱子里。比如氧化剂绝对不能跟易燃液体同箱，否则很容易造成爆炸。本题给定一张不相容物品的清单，需要你检查每一张集装箱货品清单，判断它们是否能装在同一只箱子里。
 输入格式：
 输入第一行给出两个正整数：N (≤104) 是成对的不相容物品的对数；M (≤100) 是集装箱货品清单的单数。
 随后数据分两大块给出。第一块有 N 行，每行给出一对不相容的物品。第二块有 M 行，每行给出一箱货物的清单，格式如下：
 K G[1] G[2] ... G[K]
 其中 K (≤1000)是物品件数，G[i]是物品的编号。简单起见，每件物品用一个5位数的编号代表。两个数字之间用空格分隔。
 输出格式：
 对每箱货物清单，判断是否可以安全运输。如果没有不相容物品，则在一行中输出 Yes，否则输出 No。
 输入样例：
6 3
20001 20002
20003 20004
20005 20006
20003 20001
20005 20004
20004 20006
4 00001 20004 00002 20003
5 98823 20002 20003 20006 10010
3 12345 67890 23333
 输出样例：
 No
 Yes
 Yes
 */

#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a, const void *b)
{
        return *(int*)a - *(int*)b;
}

int main()
{
        int n, m, k;
        int list[10000][2] = {{0}}, tmp[1000];
        int i, j, f;

        scanf("%d %d", &n, &m);
        for(i = 0; i < n; i++)
                scanf("%d %d", &list[i][0], &list[i][1]);
        for (i = 0; i < m; i++) {
                f = 1;
                scanf("%d", &k);
            for (j = 0; j < k; j++) scanf("%d", &tmp[j]);
                qsort(tmp, k, sizeof(int), cmp);

                for (j = 0; j < n; j++) {
                        if ( bsearch(&list[j][0], tmp, k, sizeof(int), cmp)
                        &&   bsearch(&list[j][1], tmp, k, sizeof(int), cmp)) {
                                puts("No");
                                f = 0;
                                break;
                        }
                }
                if (f) puts("Yes");
        }
        return 0;
}
```

```
暴力求会超时，需要先对输入进来的清单进行qsort排序，然后用bsearch二分法进行查找
```



## 1091-1100

### PAT_1091N-自守数

```c
/*
 如果某个数 K 的平方乘以 N 以后，结果的末尾几位数等于 K，那么就称这个数为“N-自守数”。例如 3×92
 2=25392，而 25392 的末尾两位正好是 92，所以 92 是一个 3-自守数。
 本题就请你编写程序判断一个给定的数字是否关于某个 N 是 N-自守数。
 输入格式：
 输入在第一行中给出正整数 M（≤20），随后一行给出 M 个待检测的、不超过 1000 的正整数。
 输出格式：
 对每个需要检测的数字，如果它是 N-自守数就在一行中输出最小的 N 和 NK2的值，以一个空格隔开；否则输出 No。注意题目保证 N<10。
 输入样例：
 3
 92 5 233
 输出样例：
 3 25392
 1 25
 No
 */

#include<stdio.h>
#include<math.h>

int get_wei(int x);

int main(){
    int m,i,j,n,k,kf;
    scanf("%d",&m);
    while(m--){
        scanf("%d",&k);
        kf=k*k;
        for(i=1;i<10;i++){
            if( (i*kf)%((int)(pow(10,get_wei(k))) )==k ){
                printf("%d %d\n",i,i*kf);break;
            }
        }
        if(i==10) printf("No\n");
    }
    
    
    return 0;
}

int get_wei(int x){
    int n=0;
    while(x>0){
        x/=10;
        n++;
    }
    return n;
}
```



PAT_1092

```c
/*在这里我们用数字说话，给出全国各地各种月饼的销量，要求你从中找出销量冠军，认定为最好吃的月饼。
 输入格式：
 输入首先给出两个正整数N（≤1000）和M（≤100），分别为月饼的种类数（于是默认月饼种类从1到N编号）和参与统计的城市数量。
 接下来 M 行，每行给出 N 个非负整数（均不超过 1 百万），其中第i个整数为第i种月饼的销量（块）。数字间以空格分隔。
 输出格式：
 在第一行中输出最大销量，第二行输出销量最大的月饼的种类编号。如果冠军不唯一，则按编号递增顺序输出并列冠军。数字间以 1 个空格分隔，行首尾不得有多余空格。
 输入样例：
5 3
1001 992    0  233    6
   8   0 2018    0 2008
  36  18    0 1024    4
 输出样例：
 2018
 3 5
 */

#include<stdio.h>
#include<stdlib.h>

int main(){
    int n,m,i,xl,index=0,pr[1010];
    long b[1010],max;
    scanf("%d%d",&n,&m);

    for(i=1;i<=n;i++) b[i]=0;
    while(m--){
        for(i=1;i<=n;i++){
            scanf("%d",&xl);
            b[i]+=xl;
        }
    }
    max=b[1];
    for(i=1;i<=n;i++) max=b[i]>max? b[i]:max;
    for(i=1;i<=n;i++) if(b[i]==max) pr[index++]=i;
    printf("%ld\n",max);
    for(i=0;i<index-1;i++){
        printf("%d ",pr[i]);
    }
    printf("%d\n",pr[i]);

    return 0;
}
```

```
不需要创建一个结构体并对他排序，只需要用一个数组，先对数组遍历得到他的最大值，再遍历一遍数组将等于这个最大值的编号输出即可。
```



PAT_1093

```c
/*给定两个字符串 A 和 B，本题要求你输出 A+B，即两个字符串的并集。要求先输出 A，再输出 B，但重复的字符必须被剔除。
 输入格式：
 输入在两行中分别给出A和B，均为长度不超过106的、由可见ASCII字(即码值为32~126)和空格组成的、由回车标识结束的非空字符串。
 输出格式：
 在一行中输出题面要求的 A 和 B 的和。
 输入样例：
This is a sample test
to show you_How it works
 输出样例：
 This ampletowyu_Hrk
 */

#include<stdio.h>
#include<string.h>

int main(){
    char a[5000000+10],b[1000000+10];
    int ch[150],cnt_k=0,i,len1,num;
    for(i=0;i<=140;i++) ch[i]=0;
    gets(a);gets(b);
    strcat(a,b);
    len1=strlen(a);
    for(i=0;i<len1;i++){
        num=a[i];
        if(ch[num]==0) {
            printf("%c",a[i]);
            ch[num]++;
        }
    }
    printf("\n");
    return 0;
}
```



### PAT_1094谷歌的招聘分数

```c
/*自然常数 e 是一个著名的超越数，前面若干位写出来是这样的：e = 2.718281828459045235360287471352662497757247093699959574966967627724076630353547594571382178525166427427466391932003059921... 其中粗体标出的 10 位数7427466391就是答案
 本题要求你编程解决一个更通用的问题：从任一给定的长度为 L 的数字中，找出最早出现的 K 位连续数字所组成的素数。
 输入格式：
 输入在第一行给出2个正整数，分别是L（不超过1000的正整数，为数字长度）和K（小于10的正整数）。接下来一行给出一个长度为 L 的正整数 N。
 输出格式：
 在一行中输出N中最早出现的K位连续数字所组成的素数。如果这样的素数不存在，则输出404。注意，原始数字中的前导零也计算在位数之内。例如在 200236 中找 4 位素数，0023 算是解；但第一位 2 不能被当成 0002 输出，因为在原始数字中不存在这个 2 的前导零。
 输入样例 1：
20 5
23654987725541023819
输出样例 1：
49877
输入样例 2：
10 3
2468001680
输出样例 2：
404
 */

#include<stdio.h>
#include<math.h>
int isPrime(int x);//返回1表示不是素数
int get_len(int x);//返回x的位数

int main(){
    int L,K,i,j,p=0,x=0,flag=0;
    int nums[1000+10];
    char num[1010];
    scanf("%d%d",&L,&K);
    scanf("%s",num);
    for(i=0;i<L;i++){
        nums[i]=num[i]-'0';
    }
    while(p+K<=L){
        x=0;
        for(j=0;j<K;j++){
            x=x*10+nums[p+j];
        }
        if(isPrime(x)==0){flag=1;break;}
        p++;
    }
//    if(flag) printf("%d\n",x);//不能这样写要有前导零
    if(flag){
        for(i=0;i<K-get_len(x);i++) printf("0");
        printf("%d\n",x);
    }
    else printf("404\n");
    
    return 0;
}


int isPrime(int x){
    int i,n=0;
    if(x==0) return 1;//0不是素数
    if(x==1) return 1;//1不是素数
    if(x==2) return 0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) {n++;break;}
    }
    return n;
}
int get_len(int x){
    int n=0;
    int num=x;
    while(num>0){
        num/=10;
        n++;
    }
    return n;
}
```

```
注意题目要求前导零依然需要输出
```



### PAT_1095解码PAT准考证

```

```



### PAT_1096大美数

```
四个for暴力求解
```

```c
/*若正整数 N 可以整除它的 4 个不同正因数之和，则称这样的正整数为“大美数”。本题就要求你判断任一给定的正整数是否是“大美数”。
输入格式：
 输入在第一行中给出正整数 K（≤10），随后一行给出 K 个待检测的、不超过 104的正整数。
 输出格式：
 对每个需要检测的数字，如果它是大美数就在一行中输出 Yes，否则输出 No。
 输入样例：
 3
 18 29 40
 输出样例：

 Yes
 No
 Yes
 */

#include<stdio.h>
#include<stdlib.h>
#include<math.h>
//
//测试点1：仔细看题目后发现是输入数整除四个正因数的和，除不是除以
int get_yin(int x,int a[]);//return num of yin

int main(){
    int i,n,j,k,x,y,yin[1010],sum;
    int flag,len;
    scanf("%d",&k);
    while(k--){
        scanf("%d",&n);
        len=get_yin(n,yin);
        if(len<4) {printf("No\n");continue;}
        
        flag=0;
        for(i=0;i<len;i++){
            for(j=i+1;j<len;j++){
                for(x=j+1;x<len;x++){
                    for(y=x+1;y<len;y++){
                        sum=yin[i]+yin[j]+yin[x]+yin[y];
                        if( sum%n==0 )
                        {
                            flag=1;
                            break;
                        }
                    }
                    if(flag) break;
                }
                if(flag) break;
            }
            if(flag) break;
        }
        if(flag) printf("Yes\n");
        else printf("No\n");
    }
    return 0;
}
int get_yin(int x,int a[]){
    int ln=0,i;
    for(i=1;i<=x;i++){
        if(x%i==0) a[ln++]=i;
    }
    return ln;
}
```



### PAT_1097矩阵行平移

```
个人感觉题目描述的不太清楚，这里的意思是，奇数行向右平移，每次平移1，2，3 … k, 1， 2， 3， … ，k。并不是1， k， 1， k。而且示例给的实在太狡猾了。容易被误导
```

```c
/*给定一个 n×n 的整数矩阵。对任一给定的正整数 k<n，我们将矩阵的奇数行的元素整体向右依次平移 1、……、k、1、……、k、…… 个位置，平移空出的位置用整数 x 补。你需要计算出结果矩阵的每一列元素的和。
 输入格式：
 输入第一行给出 3 个正整数：n（<100）、k（<n）、x（<100），分别如题面所述。
 接下来 n 行，每行给出 n 个不超过 100 的正整数，为矩阵元素的值。数字间以空格分隔。
 输出格式：
 在一行中输出平移后第 1 到 n 列元素的和。数字间以 1 个空格分隔，行首尾不得有多余空格。
 输入样例：
7 2 99
11 87 23 67 20 75 89
37 94 27 91 63 50 11
44 38 50 26 40 26 24
73 85 63 28 62 18 68
15 83 27 97 88 25 43
23 78 98 20 30 81 99
77 36 48 59 25 34 22
 输出样例：
 529 481 479 263 417 342 343
 样例解读
 需要平移的是第 1、3、5、7 行。给定 k=2，应该将这三列顺次整体向右平移 1、2、1、2 位（如果有更多行，就应该按照 1、2、1、2、1、2 …… 这个规律顺次向右平移），左端的空位用 99 来填充。平移后的矩阵变成：
 99 11 87 23 67 20 75
 37 94 27 91 63 50 11
 99 99 44 38 50 26 40
 73 85 63 28 62 18 68
 99 15 83 27 97 88 25
 23 78 98 20 30 81 99
 99 99 77 36 48 59 25
*/
//个人感觉题目描述的不太清楚，这里的意思是，奇数行向右平移，每次平移1，2，3 … k, 1， 2， 3， … ，k。并不是1， k， 1， k。而且示例给的实在太狡猾了。容易被误导
#include<stdio.h>

int main(){
    int n,k,x,line,i,j,num[110][100+10],sum,step;
    scanf("%d%d%d",&n,&k,&x);
    line=1;step=1;
    while(line<=n){
        for(i=1;i<=n;i++) scanf("%d",&num[line][i]);
        if(line%2==1){
            if(step>k) step=1;
            for(i=n;i>=step+1;i--){
                num[line][i]=num[line][i-step];
            }
            for(i=1;i<=step;i++){
                num[line][i]=x;
            }
            step++;
        }
        line++;
    }
    
    for(i=1;i<n;i++){
        sum=0;
        for(j=1;j<=n;j++) sum+=num[j][i];
        printf("%d ",sum);
    }
    sum=0;
    for(j=1;j<=n;j++) sum+=num[j][i];
    printf("%d\n",sum);

    return 0;
}
```



### PAT_1098岩洞施工

```c
/*输入在第一行给出一个不超过100的正整数N，即横向采样的点数。随后两行数据，从左到右顺次给出采样点的纵坐标：第 1 行是岩洞顶部的采样点，第 2 行是岩洞底部的采样点。这里假设坐标原点在左下角，每个纵坐标为不超过 1000的非负整数。同行数字间以空格分隔。题目保证输入数据是合理的，即岩洞底部的轮廓线不会与顶部轮廓线交叉
 输出格式：
 如果可以直接施工，则在一行中输出Yes和可以送入的管道的最大直径；如果不行，则输出No和至少需要削掉的高度。答案和数字间以 1 个空格分隔。
 输入样例 1：
11
7 6 5 5 6 5 4 5 5 4 4
3 2 2 2 2 3 3 2 1 2 3
 输出样例 1：
 Yes 1
 输入样例 2：
11
7 6 5 5 6 5 4 5 5 4 4
3 2 2 2 3 4 3 2 1 2 3
 输出样例 2：
 No 1
 */

#include<stdio.h>

int main(){
    int n,a[110],b[110];//b是下面的管道
    int FlagPass,max_b,i,max_len;
    scanf("%d",&n);
    for(i=0;i<n;i++) scanf("%d",&a[i]);
    for(i=0;i<n;i++) scanf("%d",&b[i]);
    max_b=b[0];
    for(i=0;i<n;i++){
        max_b=b[i]>max_b? b[i]:max_b;
    }
    
    max_len=a[0]-max_b;
    for(i=0;i<n;i++){
        max_len=(a[i]-max_b)<max_len? (a[i]-max_b):max_len;
    }
    if(max_len>0) FlagPass=1;//表示能通过
    else FlagPass=0;
    if(FlagPass) {printf("Yes %d\n",max_len);return 0;}
    
    max_len=-max_len+1;
    printf("No %d\n",max_len);
    return 0;
}
```



### PAT_1099性感素数

```
若 N 不是性感素数，则在一行中输出 No，然后在第二行输出大于 N 的最小性感素数。
也就是如果n不是素数，检查大于n的数x，如果x和x-6都是素数，输出x
如果x和x+6都是素数输出x
```

```c
/*“性感素数”是指形如 (p, p+6) 这样的一对素数。之所以叫这个名字，是因为拉丁语管“六”叫“sex”（即英语的“性感”）。
 现给定一个整数，请你判断其是否为一个性感素数。
 输入格式：
输入在一行中给出一个正整数 N (≤108
 输出格式：
 若N是一个性感素数，则在一行中输出Yes，并在第二行输出与N配对的另一个性感素数（若这样的数不唯一，输出较小的那个。若 N 不是性感素数，则在一行中输出 No，然后在第二行输出大于 N 的最小性感素数。
输入样例 1：
 47
 输出样例 1：
 Yes
 41
 输入样例 2：
 21
 输出样例 2：
 No
 23
 */

#include<stdio.h>
#include<math.h>
#include<stdlib.h>

int isPrime(int x);//如果是素数返回0；不是素数返回1；

int main(){
    int n;
    scanf("%d",&n);
    if( isPrime(n)==0 && isPrime(n-6)==0 ){
        printf("Yes\n%d\n",n-6);
        return 0;
    }
    if( isPrime(n)==0 && isPrime(n+6)==0 ){
        printf("Yes\n%d\n",n+6);
        return 0;
    }
    while(n++){
        if( isPrime(n)==0 && isPrime(n-6)==0 ){
            printf("No\n%d\n",n);
            return 0;
        }
        if( isPrime(n)==0 && isPrime(n+6)==0 ){
            printf("No\n%d\n",n);
            return 0;
        }
    }
    
    
    return 0;
}

int isPrime(int x){
    int n=0,i;
    if(x<=1) return 1;
    if(x==2) return 0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) {n++;break;}
    }
    return n;
}
```



### PAT_1100校庆

```
这个解法在最后两个测试点会超时，思路，用二分法bsearch优化，懒得做了
如果是C++的话可以用哈希，C语言的哈希太麻烦了，不想做
```

```c
/*为了准备校庆，校友会收集了所有校友的身份证号。现在需要请你编写程序，根据来参加校庆的所有人士的身份证号，统计来了多少校友。
 输入格式：
 输入在第一行给出不超过105的正整数N，随后N行，每行给出一位校友的身份证号（18位由数字和大写字母X组成的字符串）。题目保证身份证号不重复。 随后给出前来参加校庆的所有人士的信息：首先是一个不超过 105的正整数 M，随后 M 行，每行给出一位人士的身份证号。题目保证身份证号不重复。
 输出格式：
 首先在第一行输出参加校庆的校友的人数。然后在第二行输出最年长的校友的身份证号 —— 注意身份证第 7-14 位给出的是 yyyymmdd格式的生日。如果没有校友来，则在第二行输出最年长的来宾的身份证号。题目保证这样的校友或来宾必是唯一
 输入样例：
5
372928196906118710
610481197806202213
440684198612150417
13072819571002001X
150702193604190912
6
530125197901260019
150702193604190912
220221196701020034
610481197806202213
440684198612150417
370205198709275042
 输出样例：
 3
 150702193604190912
 */

#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct XY{
    char id[25];
    int comed;//1表示来了
}XY;

int main(){
    int n,m,i,cntXYcomed=0,year,max_year=90000000,max_i_id;
    char no[25],max_no[25];
    XY y[100000+10];
    scanf("%d",&n);
    for(i=0;i<n;i++){
        scanf("%s",y[i].id);
        //y[i].old=y[i].id[13]-'0'+ 10*(y[i].id[12]-'0')+ 100*(y[i].id[11]-'0')+ 1000*(y[i].id[10]-'0')+  10000*(y[i].id[9]-'0')+ 100000*(y[i].id[8]-'0')+ 1000000*(y[i].id[7]-'0')+ 10000000*(y[i].id[6]-'0');
        y[i].comed=0;
    }
    scanf("%d",&m);
    while(m--){
        scanf("%s",no);
        year=no[13]-'0'+ 10*(no[12]-'0')+ 100*(no[11]-'0')+ 1000*(no[10]-'0')+  10000*(no[9]-'0')+ 100000*(no[8]-'0')+ 1000000*(no[7]-'0')+ 10000000*(no[6]-'0');
        if(year<max_year) {max_year=year;strcpy(max_no,no);}
        for(i=0;i<n;i++){
            if( strcmp(no,y[i].id)==0 ){
                cntXYcomed++;
                y[i].comed=1;
                break;
            }
        }
    }
    printf("%d\n",cntXYcomed);
    if(cntXYcomed==0){
        printf("%s\n",max_no);
    }
    else{
        max_year=90000000;
        for(i=0;i<n;i++){
            if( y[i].comed==1 ){
                year=y[i].id[13]-'0'+ 10*(y[i].id[12]-'0')+ 100*(y[i].id[11]-'0')+ 1000*(y[i].id[10]-'0')+  10000*(y[i].id[9]-'0')+ 100000*(y[i].id[8]-'0')+ 1000000*(y[i].id[7]-'0')+ 10000000*(y[i].id[6]-'0');
//                if(year<max_year) {max_year=year;strcpy(max_no,y[i].id);}
                if(year<max_year) {max_year=year;max_i_id=i;}
            }
        }
//        printf("%s\n",max_no);
        printf("%s\n",y[max_i_id].id);
        
    }
    return 0;
}
```



## 1101-1110

### PAT_1101B是A的多少倍

```c
/*设一个数 A 的最低 D 位形成的数是 ad   。如果把 ad截下来移到 A 的最高位前面，就形成了一个新的数 B。B 是 A 的多少倍？例如将 12345 的最低 2 位 45 截下来放到 123 的前面，就得到 45123，它约是 12345 的 3.66 倍。
 输入格式：
 输入在一行中给出一个正整数 A（≤109）和要截取的位数 D。题目保证 D 不超过 A 的总位数。
 输出格式：
 计算 B 是 A 的多少倍，输出小数点后 2 位。
 输入样例 1：
 12345 2
 输出样例 1：
 3.66
 输入样例 2：
 12345 5
 输出样例 2：
 1.00
 */

#include<stdio.h>
#include<string.h>
#include<math.h>

int main(){
    int d,len,i;
    int a=0,b=0;
    char num[15];
    scanf("%s%d",num,&d);
    len=strlen(num);
    for(i=0;i<len;i++){
        a=a*10+num[i]-'0';
    }
    for(i=len-d;i<len;i++){
        b=b*10+num[i]-'0';
    }
    for(i=0;i<len-d;i++){
        b=b*10+num[i]-'0';
    }
    printf("%.2lf\n",1.0*b/a);
    
    return 0;
}
```



### PAT_1102教超冠军卷

```c
/*“教育超市”是拼题A系统的一个衍生产品，发布了各种试卷和练习供用户选购。在试卷列表中，系统不仅列出了每份试卷的单价，还显示了当前的购买人次。本题就请你根据这些信息找出教育超市所有试卷中的销量（即购买人次）冠军和销售额冠军。
 输入格式：
 输入首先在第一行中给出一个正整数N（≤104），随后N行，每行给出一份卷子的独特ID（由小写字母和数字组成的、长度不超过8位的字符串）、单价（为不超过 100 的正整数）和购买人次（为不超过 10 6   的非负整数）。
 输出格式：
 在第一行中输出销量冠军的ID及其销量，第二行中输出销售额冠军的ID及其销售额。同行输出间以一个空格分隔。题目保证冠军是唯一的，不存在并列。
 输入样例：
4
zju007 39 10
pku2019 9 332
pat2018 95 79
qdu106 19 38
 输出样例：
 pku2019 332
 pat2018 7505
 */

#include<stdio.h>

typedef struct XL{
    char id[15];
    int dj;
    int num;
    int sum;
}XL;

int main(){
    int n,i,maxnum=0,maxsum=0,i_maxnum=0,i_maxsum=0;
    scanf("%d",&n);
    XL a[10010];
    for(i=0;i<n;i++){
        scanf("%s%d%d",a[i].id,&a[i].dj,&a[i].num);
        a[i].sum=a[i].dj*a[i].num;
        if(a[i].num > maxnum){
            i_maxnum=i;
            maxnum=a[i].num;
        }
        if(a[i].sum > maxsum){
            i_maxsum=i;
            maxsum=a[i].sum;
        }
    }
    printf("%s %d\n",a[i_maxnum].id,a[i_maxnum].num);
    printf("%s %d\n",a[i_maxsum].id,a[i_maxsum].sum);
    return 0;
}
```



### PAT_1103缘分数

```c
/*所谓缘分数是指这样一对正整数 a 和 b，其中 a 和它的小弟 a−1 的立方差正好是另一个整数 c 的平方，而 c 正好是 b 和它的小弟 b−1 的平方和。例如 83  −7 3  =169=13 2  ，而 13=3 2  +2 2  ，于是 8 和 3 就是一对缘分数。
 给定 a 所在的区间 [m,n]，是否存在缘分数？
输入格式：
 输入给出区间的两个端点 0<m<n≤25000，其间以空格分隔。
 输出格式：
 按照 a 从小到大的顺序，每行输出一对缘分数，数字间以空格分隔。如果无解，则输出 No Solution。
 输入样例 1：
 8 200
 输出样例 1：
 8 3
 105 10
 输入样例 2：
 9 100
 输出样例 2：
 No Solution
 */

#include<stdio.h>
#include<math.h>

typedef struct PR{
    int a;
    int b;
}PR;

int main(){
    int m,n,a,b,i,j,t,x,index=0;
    PR pr[1000];
    scanf("%d%d",&m,&n);
    for(i=m;i<=n;i++){
        a=i;
        t=pow(a,3)-pow(a-1,3);
        x=sqrt(t);
        if(x*x==t){//满足这个相减是一个平方数
            for(j=1;j<=n;j++){
                b=j;
                if(x==pow(b,2)+pow(b-1,2) && a!=b){//没有这a！=b会有一个1 1的答案
                    pr[index].a=a;
                    pr[index].b=b;
                    index++;
                    break;
                }
                if(x<pow(b,2)+pow(b-1,2)) break;
            }
        }
        
    }
    
    if(index==0) {printf("No Solution\n");return 0;}
    for(i=0;i<index;i++){
        printf("%d %d\n",pr[i].a,pr[i].b);
    }
    
    return 0;
}
```



### PAT_1104天长地久

```
在自己机器上测试的时候先不考虑时间把所有结果打印出来看看，发现后几位数都是9，所以只需把9取出来只遍历前面的部分就大大减少运行时间了。在m=45，56的时候，后面都是9999，m=34的时候只有99。没有发现3个9的情况，所以我瞎猜，m<45的时候都是99，else都是9999。然后按照这个思路去做，测试点3就翻车了，看来只能提取99，不能提多了。
这样能减少循环的次数，从而降低运行时间
是要按照n递增输出，所以还得qsort
```

```c
/*“天长地久数”是指一个 K 位正整数 A，其满足条件为：A 的各位数字之和为 m，A+1 的各位数字之和为 n，且 m 与 n 的最大公约数是一个大于 2 的素数。本题就请你找出这些天长地久数。
 输入在第一行给出正整数 N（≤5），随后 N 行，每行给出一对 K（3<K<10）和 m（1<m<90），其含义如题面所述。
 对每一对输入的 K 和 m，首先在一行中输出 Case X，其中 X 是输出的编号（从 1 开始）；然后一行输出对应的 n 和 A，数字间以空格分隔。如果解不唯一，则每组解占一行，按n的递增序输出；若仍不唯一，则按A的递增序输出。若解不存在，则在一行中输出 No Solution。
 输入样例：
2
6 45
7 80
 输出样例：
 Case 1
 10 189999
 10 279999
 10 369999
 10 459999
 10 549999
 10 639999
 10 729999
 10 819999
 10 909999
 Case 2
 No Solution
 */

#include<stdio.h>
#include<math.h>
#include<stdlib.h>

typedef struct PR{
    int p1;
    int p2;
}PR;

int GCD(int a,int b);//求最大公约数
int isPrime(int x);//判断是不是素数，是素数返回0；不是素数返回1；
int getAsum(int x);//计算A的各位数字之和
int cmp(const void* _a,const void* _b);

int main(){
    int N,k,m,n,CASE=1,cnt,A,gcd1,i;
    PR pr[1000];
    scanf("%d",&N);
    while(CASE<=N){
        printf("Case %d\n",CASE);CASE++;
        cnt=0;
        scanf("%d%d",&k,&m);
//        for(A=pow(10,k-1);A<pow(10,k);A++){//A是k位数
        for (A = 99 + pow(10, k - 1); A < pow(10, k); A += 100){
            if(getAsum(A)==m){
                n=getAsum(A+1);
                gcd1=abs(GCD(m, n));
                if(isPrime(gcd1)==0 && gcd1>2){
                    pr[cnt].p1=n;
                    pr[cnt].p2=A;
                    cnt++;
//                    printf("%d %d\n",n,A);
                }
            }
        }
        if(cnt==0) printf("No Solution\n");
        else{
            qsort(pr,cnt,sizeof(PR),cmp);
            for(i=0;i<cnt;i++){
                printf("%d %d\n",pr[i].p1,pr[i].p2);
            }
            
        }
    }
    return 0;
}


int GCD(int a,int b){
    if(b==0) return a;  //可以用条件表达式表达 return b==0?a:gcd(b,a%b)
    return GCD(b,a%b);
}
int isPrime(int x){
    int i,n=0;
    if(x<=1) return 1;
    if(x==2) return 0;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) {n++;break;}
    }
    return n;
}
int getAsum(int x){
    int s=0;
    while(x>0){
        s+=x%10;
        x/=10;
    }
    return s;
}
int cmp(const void* _a,const void* _b){
    PR* a=(PR*)_a;
    PR* b=(PR*)_b;
    if(a->p1==b->p1) return a->p2 - b->p2;
    else return a->p1 - b->p1;
}
```



### PAT_1105链表合并

```c
/*
 给定两个单链表 L 1  =a 1  →a 2  →⋯→a n−1  →a n   和 L 2  =b 1  →b 2  →⋯→b m−1  →b m  。如果 n≥2m，你的任务是将比较短的那个链表逆序，然后将之并入比较长的那个链表，得到一个形如 a 1  →a 2  →b m   →a 3  →a 4  →b m−1  ⋯ 的结果。例如给定两个链表分别为 6→7 和 1→2→3→4→5，你应该输出 1→2→7→3→4→6→5。 输入格式：
 输入首先在第一行中给出两个链表 L 1   和 L 2   的头结点的地址，以及正整数 N (≤10 5  )，即给定的结点总数。一个结点的地址是一个 5 位数的非负整数，空地址 NULL 用 -1 表示。 随后 N 行，每行按以下格式给出一个结点的信息： Address Data Next 其中 Address 是结点的地址，Data 是不超过 10 5   的正整数，Next 是下一个结点的地址。题目保证没有空链表，并且较长的链表至少是较短链表的两倍长。
 输出格式：
 按顺序输出结果链表，每个结点占一行，格式与输入相同。
 输入样例：
00100 01000 7
02233 2 34891
00100 6 00001
34891 3 10086
01000 1 02233
00033 5 -1
10086 4 00033
00001 7 -1
 输出样例：
 01000 1 02233
 02233 2 00001
 00001 7 34891
 34891 3 10086
 10086 4 00100
 00100 6 00033
 00033 5 -1
 */

#include<stdio.h>
#include<string.h>

typedef struct{
    int addr;
    int data;
    int next;
}Node;

int main(){
    int firstAddr1,firstAddr2,N;
    int len1,len2;
    int lenlong,lenshort;
    int firstAddr;
    scanf("%d%d%d",&firstAddr1,&firstAddr2,&N);
    Node nodes[100005];
    Node node1[100005];
    Node node2[100005];
    int addr,i,j,k;
    for(i=0;i<N;i++){
        scanf("%d",&addr);
        nodes[addr].addr=addr;
        scanf("%d %d", &nodes[addr].data, &nodes[addr].next);
    }
    node1[0].addr=firstAddr1;
    node1[0].data=nodes[firstAddr1].data;
    node1[0].next=nodes[firstAddr1].next;
    for(i=1;i<N;i++){
        if(node1[i-1].next !=-1){
            node1[i].addr=node1[i-1].next;
            node1[i].data=nodes[node1[i].addr].data;
            node1[i].next=nodes[node1[i].addr].next;
        }
        else{
            break;
        }
    }
    len1=i;
    
    node2[0].addr = firstAddr2;
    node2[0].data = nodes[firstAddr2].data;
    node2[0].next = nodes[firstAddr2].next;
    for (i = 1; i < N; i++)
    {
        if (node2[i - 1].next != -1)
        {
            node2[i].addr = node2[i - 1].next;
            node2[i].data = nodes[node2[i].addr].data;
            node2[i].next = nodes[node2[i].addr].next;
        }
        else
        {
            break;
        }
    }
    len2 = i;
    
    lenlong = (len2 > len1 ? len2 : len1);
    lenshort = (len2 > len1 ? len1 : len2);
    for (i = 1, j = lenshort - 1; j >= 0; i = i + 2, j--)
    {
        if (lenlong == len1)
        {
            node1[i].next = node2[j].addr;
            if (j == 0 && lenlong == 2 * lenshort)//短链表作结尾的情况
            {
                node2[j].next = -1;
            }
            else
                node2[j].next = node1[i + 1].addr;//长链表作结尾的情况
        }
        else
        {
            node2[i].next = node1[j].addr;
            if (j == 0 && lenlong == 2 * lenshort)
            {
                node1[j].next = -1;
            }
            else
                node1[j].next = node2[i + 1].addr;
        }
    }
    Node newnodes[100002];//下标存放地址
    for (k = 0; k < len1; k++)
    {
        newnodes[node1[k].addr].addr = node1[k].addr;
        newnodes[node1[k].addr].data = node1[k].data;
        newnodes[node1[k].addr].next = node1[k].next;
    }
    for (k = 0; k < len2; k++)
    {
        newnodes[node2[k].addr].addr = node2[k].addr;
        newnodes[node2[k].addr].data = node2[k].data;
        newnodes[node2[k].addr].next = node2[k].next;
    }
    if (lenlong == len1)
        firstAddr = node1[0].addr;
    else
        firstAddr = node2[0].addr;
    while (firstAddr != -1)
    {
        if (newnodes[firstAddr].next != -1)
            printf("%05d %d %05d\n", newnodes[firstAddr].addr, newnodes[firstAddr].data, newnodes[firstAddr].next);
        else
            printf("%05d %d -1\n", newnodes[firstAddr].addr, newnodes[firstAddr].data);
        firstAddr = newnodes[firstAddr].next;
    }
    return 0;
}
```



### PAT_11062019数列

```c
/*把 2019 各个数位上的数字 2、0、1、9 作为一个数列的前 4 项，用它们去构造一个无穷数列，其中第 n（>4）项是它前 4 项之和的个位数字。例如第 5 项为 2， 因为 2+0+1+9=12，个位数是 2。本题就请你编写程序，列出这个序列的前 n 项。
 输入格式：
 输入给出正整数 n（≤1000）。
 输出格式：
 在一行中输出数列的前 n 项，数字间不要有空格。
 输入样例：
 10
 输出样例：
 2019224758
 */

#include<stdio.h>

int main(){
    int num[1010]={0,2,0,1,9},n,i;
    scanf("%d",&n);
    for(i=5;i<=n;i++){
        num[i]=(num[i-1]+num[i-2]+num[i-3]+num[i-4])%10;
    }
    for(i=1;i<=n;i++) printf("%d",num[i]);
    
    return 0;
}
```



### PAT_1107老鼠爱大米

```c
/*翁恺老师曾经设计过一款 Java 挑战游戏，叫“老鼠爱大米”（或许因为他的外号叫“胖胖鼠”）。每个玩家用 Java 代码控制一只鼠，目标是抢吃尽可能多的大米让自己变成胖胖鼠，最胖的那只就是冠军。 因为游戏时间不能太长，我们把玩家分成N组，每组M只老鼠同场竞技，然后从N个分组冠军中直接选出最胖的冠军胖胖鼠。现在就请你写个程序来得到冠军的体重。
 输入格式：
 输入在第一行中给出2个正整数：N（≤100）为组数，M（≤10）为每组玩家个数。随后N行，每行给出一组玩家控制的M只老鼠最后的体重，均为不超过 10 4   的非负整数。数字间以空格分隔。
 输出格式：
 首先在第一行顺次输出各组冠军的体重，数字间以1个空格分隔，行首尾不得有多余空格。随后在第二行输出冠军胖胖鼠的体重。
 输入样例：
3 5
62 53 88 72 81
12 31 9 0 2
91 42 39 6 48
 输出样例：
 88 31 91
 91
 */

#include<stdio.h>

int main(){
    int n,m,max,i,num[110],index=0,j,temp;
    scanf("%d%d",&n,&m);
    for(i=0;i<n;i++){
        max=0;
        for(j=0;j<m;j++){
            scanf("%d",&temp);
            max=max>temp? max:temp;
        }
        num[index++]=max;
    }
    max=0;
    for(i=0;i<index-1;i++){
        printf("%d ",num[i]);
        max=max>num[i]? max:num[i];
    }
    printf("%d\n",num[i]);
    max=max>num[i]? max:num[i];
    printf("%d\n",max);
    return 0;
}
```



### PAT_1108String复读机

```
/*给定一个长度不超过 104的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 StringString.... （注意区分大小写）这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 String 的顺序打印，直到所有字符都被输出。例如 gnirtSSs 要调整成 StringS 输出，其中 s 是多余字符被忽略。
 输格式：
 输入在一行中给出一个长度不超过 10 4   的、仅由英文字母构成的非空字符串。
 输出格式：
 在一行中按题目要求输出排序后的字符串。题目保证输出非空。
 输入样例：
sTRidlinSayBingStrropriiSHSiRiagIgtSSr
 输出样例：
 StringStringSrigSriSiSii
 */

#include<stdio.h>
#include<string.h>


int main(){
    char c;
    int cntS=0,cntt=0,cntr=0,cnti=0,cntn=0,cntg=0;
    while((c=getchar())!='\n'){
        if(c=='S') cntS++;
        else if(c=='t') cntt++;
        else if(c=='r') cntr++;
        else if(c=='i') cnti++;
        else if(c=='n') cntn++;
        else if(c=='g') cntg++;
    }
    while(cntS>0 || cntt>0 || cntr>0 || cnti>0 || cntn>0 || cntg>0){
        if(cntS>0){printf("S");cntS--;}
        if(cntt>0){printf("t");cntt--;}
        if(cntr>0){printf("r");cntr--;}
        if(cnti>0){printf("i");cnti--;}
        if(cntn>0){printf("n");cntn--;}
        if(cntg>0){printf("g");cntg--;}
    }
    printf("\n");
    return 0;
}
```



### PAT_1109擅长C

```c
/*输入首先给出 26 个英文大写字母 A-Z，每个字母用一个 7×5 的、由 C 和 .
 组成的矩阵构成。最后在一行中给出一个句子，以回车结束。句子是由若干个单词（每个包含不超过10个连续的大写英文字母）组成的，单词间以任何非大写英文字母分隔。
 题目保证至少给出一个单词。
 对每个单词，将其每个字母用矩阵形式在一行中输出，字母间有一列空格分隔。单词的首尾不得有多余空格。
 相邻的两个单词间必须有一空行分隔。输出的首尾不得有多余空行。
 输出样例：
 C...C CCCCC C.... C.... .CCC.
 C...C C.... C.... C.... C...C
 C...C C.... C.... C.... C...C
 CCCCC CCCC. C.... C.... C...C
 C...C C.... C.... C.... C...C
 C...C C.... C.... C.... C...C
 C...C CCCCC CCCCC CCCCC .CCC.

 C...C .CCC. CCCC. C.... CCCC.
 C...C C...C C...C C.... C...C
 C...C C...C CCCC. C.... C...C
 C.C.C C...C CC... C.... C...C
 CC.CC C...C C.C.. C.... C...C
 C...C C...C C..C. C.... C...C
 C...C .CCC. C...C CCCCC CCCC.
 */
#include <stdio.h>
#include <string.h>

// 判断字符是否是大写字母
int isUpper(char ch);
// 打印一个单词
void printWordMatrix(char *w, int len, char Matrix[][6]);

int main() {
    int x = 26 * 7;
    int y = 6;
    // 获取输入并分别放置到两个数组 英文矩阵数组 && 句子数组
    char matrix[x][y];
    for (int i = 0; i < x + 1; i++) {
        if (i == x) {
            // 将英文矩阵数组最后的空格符吸收
            getchar();

            // 输入一个完整的单词后，就输出矩阵
            char ch;
            char result[10] = {0};
            int index = 0, newline = 0;
            while((ch = getchar()) != '\n') {
                if (!isUpper(ch)) {
                    result[index] = '\0';
                    int len = strlen(result);
                    if (len != 0) {
                        // 输出额外的空行，首尾不得有多余空行
                        if (newline != 0) {
                            printf("\n");
                        }
                        printWordMatrix(result, len, matrix);
                        newline += 1;
                    }

                    // 重置单词数组
                    index = 0;
                    result[index] = '\0';
                } else {
                    result[index++] = ch;
                }
            }

            // 解决输入案例的句子最后一个字符为 大写英文字母 的情况
            if (strlen(result) != 0) {
                if (newline != 0) {
                    printf("\n");
                }
                printWordMatrix(result, strlen(result), matrix);
            }
        } else {
            // 英文字符矩阵数组
            scanf("%s", matrix[i]);
        }
    }

    return 0;
}

// 判断字符是否是大写字母
int isUpper(char ch) {
    // if ('A' <= ch && ch <= 'Z') {}

    int num = ch - 'A';
    if (0 <= num && num <= 25) {
        return 1;
    } else {
        return 0;
    }
}

// 打印一个单词
void printWordMatrix(char *w, int len, char Matrix[][6]) {
    // 打印行数为 7 次，因此字符矩阵为 7 * 5
    for (int i = 0; i < 7; i++) {
        // 打印单词的长度
        for (int j = 0; j < len; j++) {
            int t = w[j] - 'A';
            // 英文矩阵数组的行下标，输出一整行字符串
            int index = t * 7 + i;
            printf("%s", Matrix[index]);

            if (j != len - 1) {
                printf(" ");
            }
        }
        printf("\n");
    }
}






/*
 输入样例：
..C..
.C.C.
C...C
CCCCC
C...C
C...C
C...C
CCCC.
C...C
C...C
CCCC.
C...C
C...C
CCCC.
.CCC.
C...C
C....
C....
C....
C...C
.CCC.
CCCC.
C...C
C...C
C...C
C...C
C...C
CCCC.
CCCCC
C....
C....
CCCC.
C....
C....
CCCCC
CCCCC
C....
C....
CCCC.
C....
C....
C....
CCCC.
C...C
C....
C.CCC
C...C
C...C
CCCC.
C...C
C...C
C...C
CCCCC
C...C
C...C
C...C
CCCCC
..C..
..C..
..C..
..C..
..C..
CCCCC
CCCCC
....C
....C
....C
....C
C...C
.CCC.
C...C
C..C.
C.C..
CC...
C.C..
C..C.
C...C
C....
C....
C....
C....
C....
C....
CCCCC
C...C
C...C
CC.CC
C.C.C
C...C
C...C
C...C
C...C
C...C
CC..C
C.C.C
C..CC
C...C
C...C
.CCC.
C...C
C...C
C...C
C...C
C...C
.CCC.
CCCC.
C...C
C...C
CCCC.
C....
C....
C....
.CCC.
C...C
C...C
C...C
C.C.C
C..CC
.CCC.
CCCC.
C...C
CCCC.
CC...
C.C..
C..C.
C...C
.CCC.
C...C
C....
.CCC.
....C
C...C
.CCC.
CCCCC
..C..
..C..
..C..
..C..
..C..
..C..
C...C
C...C
C...C
C...C
C...C
C...C
.CCC.
C...C
C...C
C...C
C...C
C...C
.C.C.
..C..
C...C
C...C
C...C
C.C.C
CC.CC
C...C
C...C
C...C
C...C
.C.C.
..C..
.C.C.
C...C
C...C
C...C
C...C
.C.C.
..C..
..C..
..C..
..C..
CCCCC
....C
...C.
..C..
.C...
C....
CCCCC
HELLO~WORLD!
 */
```



### PAT_1110区块反转

```c
/*给定一个单链表 L，我们将每 K 个结点看成一个区块（链表最后若不足K个结点，也看成一个区块），请编写程序将 L 中所有区块的链接反转。例如：给定 L 为 1→2→3→4→5→6→7→8，K 为3，则输出应该为7→8→4→5→6→1→2→3。
 输入格式：
 每个输入包含 1 个测试用例。每个测试用例第 1 行给出第 1 个结点的地址、结点总个数正整数 N (≤105  )、以及正整数 K (≤N)，即区块的大小。结点的地址是 5 位非负整数，NULL 地址用 −1 表示。
 接下来有 N 行，每行格式为：
 Address Data Next
 其中 Address 是结点地址，Data 是该结点保存的整数数据，Next 是下一结点的地址。
 输出格式：
 对每个测试用例，顺序输出反转后的链表，其上每个结点占一行，格式与输入相同。
 输入样例：
00100 8 3
71120 7 88666
00000 4 99999
00100 1 12309
68237 6 71120
33218 3 00000
99999 5 68237
88666 8 -1
12309 2 33218
 输出样例：
 71120 7 88666
 88666 8 00000
 00000 4 99999
 99999 5 68237
 68237 6 00100
 00100 1 12309
 12309 2 33218
 33218 3 -1
*/

#include<stdio.h>

typedef struct Node{
    int addr;
    int data;
    int next;
}Node;

int main(){
    int firstaddr,n,k,i,address;
    scanf("%d%d%d",&firstaddr,&n,&k);
    Node node_scanf[100005];
    Node link1[100005];
    Node link2[100005];
    for(i=0;i<n;i++){
        scanf("%d",&address);
        node_scanf[address].addr=address;
        scanf("%d%d",&node_scanf[address].data,&node_scanf[address].next);
    }
    
    //把scanf来的节点们按照原来的顺序放入link1中
    link1[0].addr=firstaddr;
    link1[0].data=node_scanf[firstaddr].data;
    link1[0].next=node_scanf[firstaddr].next;
    address=link1[0].next;
    for(i=1;i<n;i++){
        if(link1[i-1].next!=-1){
            link1[i].addr=node_scanf[address].addr;
            link1[i].data=node_scanf[address].data;
            link1[i].next=node_scanf[address].next;
            address=link1[i].next;
        }
        else break;
    }
    n=i;
//    for(i=0;i<n;i++){
//        printf("%05d %d %05d\n",link1[i].addr,link1[i].data,link1[i].next);
//    }
    int zu,j=0;
    if(n%k==0) zu=n/k;
    else zu=n/k+1;
    
    for(i=(zu-1)*k;i<n;i++){
        link2[j++]=link1[i];
    }
    zu--;
    while(zu--){
        for(i=zu*k;i<zu*k+k;i++){
            link2[j++]=link1[i];
        }
    }
    
    for(i=0;i<n-1;i++){
        link2[i].next=link2[i+1].addr;
    }
    link2[i].next=-1;
    
    for(i=0;i<n-1;i++){
        printf("%05d %d %05d\n",link2[i].addr,link2[i].data,link2[i].next);
    }
    printf("%05d %d %d\n",link2[i].addr,link2[i].data,link2[i].next);
    return 0;
}
```

```
错误提示
输入可能出现多余结点，例如以下测试数据中真正有意义的链表节点少于输入的N
输入
33333 3 1
11111 10 -1
33333 30 22222
22222 20 -1
正确输出
22222 20 33333
33333 30 -1
若出现了上述错误则会输出
00000 0 22222
22222 20 33333
33333 30 -1

解决办法：这种情况发生的条件就是n比实际有用的数据点要多，在把scanf来的节点们按照原来的顺序放入link1中时，会通过break出来，正好此时的i的值就是实际有用的节点个数，所以只需要在后将i赋给n即可，这么做对n=i的情况也不影响。
```



## 1111-1115

### PAT_1111对称日

```c
/*央视新闻发了一条微博，指出 2020 年有个罕见的“对称日”，即 2020 年 2 月 2 日，按照 年年年年月月日日 格式组成的字符串 20200202 是完全对称的。
 给定任意一个日期，本题就请你写程序判断一下，这是不是一个对称日？
 输入首先在第一行给出正整数 N（1<N≤10）。随后 N 行，每行给出一个日期，却是按英文习惯的格式：Month Day, Year。其中 Month 是月份的缩写，对应如下：
 一月：Jan
 二月：Feb
 三月：Mar
 四月：Apr
 五月：May
 六月：Jun
 七月：Jul
 八月：Aug
 九月：Sep
 十月：Oct
 十一月：Nov
 十二月：Dec
 Day 是月份中的日期，为 [1, 31] 区间内的整数；Year 是年份，为 [1, 9999] 区间内的整数。
 输出格式：
 对每一个给定的日期，在一行中先输出 Y 如果这是一个对称日，否则输出 N；随后空一格，输出日期对应的 年年年年月月日日 格式组成的字符串。
 输入样例：
5
Feb 2, 2020
Mar 7, 2020
Oct 10, 101
Nov 21, 1211
Dec 29, 1229
 输出样例：
 Y 20200202
 N 20200307
 Y 01011010
 Y 12111121
 N 12291229
 */

#include<stdio.h>
#include<string.h>

int main(){
    int n;
    char m[5],d[5],y[6],ymd[20];
    scanf("%d",&n);
    while(n--){
        scanf("%s%s%s",m,d,y);
        strcpy(ymd,"");
        if( strcmp(m,"Jan")==0 ) strcpy(m,"01");
        else if( strcmp(m,"Feb")==0 ) strcpy(m,"02");
        else if( strcmp(m,"Mar")==0 ) strcpy(m,"03");
        else if( strcmp(m,"Apr")==0 ) strcpy(m,"04");
        else if( strcmp(m,"May")==0 ) strcpy(m,"05");
        else if( strcmp(m,"Jun")==0 ) strcpy(m,"06");
        else if( strcmp(m,"Jul")==0 ) strcpy(m,"07");
        else if( strcmp(m,"Aug")==0 ) strcpy(m,"08");
        else if( strcmp(m,"Sep")==0 ) strcpy(m,"09");
        else if( strcmp(m,"Oct")==0 ) strcpy(m,"10");
        else if( strcmp(m,"Nov")==0 ) strcpy(m,"11");
        else if( strcmp(m,"Dec")==0 ) strcpy(m,"12");
        m[2]='\0';
        
        if(strlen(d)==2) {d[1]=d[0];d[0]='0';}
        d[2]='\0';
        if(strlen(y)==1) {y[3]=y[0];y[0]='0';y[1]='0';y[2]='0';}
        else if(strlen(y)==2) {y[2]=y[0];y[3]=y[1];y[1]='0';y[0]='0';}
        else if(strlen(y)==3) {y[3]=y[2];y[2]=y[1];y[1]=y[0];y[0]='0';}
        y[4]='\0';
        
        strcat(ymd, y);strcat(ymd, m);strcat(ymd, d);
        
        if(ymd[0]==ymd[7] && ymd[1]==ymd[6] && ymd[2]==ymd[5] && ymd[3]==ymd[4]) printf("Y ");
        else printf("N ");
        printf("%s\n",ymd);
    }
}
```



### PAT_1112超标区间

```c
/*其中红色横线表示正常数据的阈值（在此图中阈值是25）。你的任务就是把超出阈值的非正常数据所在的区间找出来。例如上图中横轴 [3, 5] 区间中的 3 个数据点超标，横轴上点9（可以表示为区间[9,9]）对应的数据点也超标。
 输入格式：
 输入第一行给出两个正整数 N（≤10 4  ）和 T（≤100），分别是数据点的数量和阈值。第二行给出 N 个数据点的纵坐标，均为不超过 1000 的正整数，对应的横坐标为整数 0 到 N−1。
 输出格式：
 按从左到右的顺序输出超标数据的区间，每个区间占一行，格式[A,B]，其中A和B为区间的左右端点。如果没有数据超标，则在一行中输出所有数据的最大值。
 输入样例 1：
11 25
21 15 25 28 35 27 20 24 18 32 23
 输出样例 1：
 [3, 5]
 [9, 9]
 输入样例 2：
11 40
21 15 25 28 35 27 20 24 18 32 23
 输出样例 2：
 35
 */

#include<stdio.h>

int main(){
    int n,T,i,max=-1,cnt=0,num[10010],flag=0;
    scanf("%d%d",&n,&T);
    for(i=0;i<n;i++){
        scanf("%d",&num[i]);
        if(num[i]>T) cnt++;
        max=max>num[i]? max:num[i];
    }
    num[i++]=-1;num[i++]=-1;//多赋值两个，避免其他错误
    if(cnt==0){
        printf("%d\n",max);
        return 0;
    }
    cnt=1;i=0;
    while(i<n){
        if(num[i]>T) flag=1;
        while(num[i]>T && num[i+cnt]>T){
            cnt++;
        }
        if(flag){printf("[%d, %d]\n",i,i+cnt-1);flag=0;}
        i+=cnt;
        cnt=1;
    }   
    return 0;
}
```



### PAT_1113钱串子的加法

```c
/*
 这个世界上有一种叫“钱串子”（学名“蚰蜒”）的生物，有30只细长的手/脚，在它们的世界里，数字应该是30进制的。本题就请你实现钱串子世界里的加法运算。
 输入格式：
 输入在一行中给出两个钱串子世界里的非负整数，其间以空格分隔。
 所谓“钱串子世界里的整数”是一个 30 进制的数字，其数字 0 到 9 跟人类世界的整数一致，数字 10 到 29 用小写英文字母 a 到 t 顺次表示。
 输入给出的两个整数都不超过 10 5   位。
 输出格式：
 在一行中输出两个整数的和。注意结果数字不得有前导零。
 输入样例：
2g50ttaq 0st9hk381
0st9hk381
 输出样例：
 11feik2ir
 */

#include<stdio.h>
#include<string.h>

void get_ni(char n[]);//让n变成逆序

int main(){
    char n1[100005],n2[100005];
    char temp[100005];
    int index=0;
    int x,y,z=0,w,i;//x是n1的当前位，y是n2的当前位，w是相加后的当前位，z是进位。
    int len1,len2;
    char huan[30]={'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t'};
    scanf("%s%s",n1,n2);
    if(strlen(n1)<strlen(n2)){
        strcpy(temp,n1);strcpy(n1, n2);strcpy(n2,temp);
    }
    get_ni(n1);get_ni(n2);
    len1=strlen(n1);len2=strlen(n2);
    for(i=len2;i<len1;i++){
        n2[i]='0';
    }
    n2[i]='\0';
    //数据预处理已完成，以下进行加法运算，将结果存入temp中
    for(i=0;i<len1;i++){
        if('0'<=n1[i] && n1[i]<='9') x=n1[i]-'0';
        else x=n1[i]-'a'+10;
        if('0'<=n2[i] && n2[i]<='9') y=n2[i]-'0';
        else y=n2[i]-'a'+10;
        
        w=(x+y+z)%30;//当前位
        z=(x+y+z)/30;//进位
        temp[index++]=huan[w];
    }
    temp[index++]=huan[z];
    temp[index]='\0';
//    printf("%s\n",temp);
//    strcpy(temp,"00000");
    int flag=1;
    for(i=index-1;i>0;i--){
        if(temp[i]=='0' && flag) continue;
        else{
            printf("%c",temp[i]);
            flag=0;
        }
    }
    printf("%c\n",temp[i]);
    
    
    return 0;
}

void get_ni(char n[]){
    int i,len=strlen(n);
    char t;
    for(i=0;i<len/2;i++){
        t=n[i];n[i]=n[len-i-1];n[len-i-1]=t;
    }
}
```



### PAT_1114全素日

```c
/*
2019年5月23日。即不仅20190523本身是个素数，它的任何以末尾数字3结尾的子串都是素数。
 本题就请你写个程序判断一个给定日期是否是“全素日”。
 输入格式：
 输入按照 yyyymmdd 的格式给出一个日期。题目保证日期在0001年1月1日到9999年12月31日之间。
 输出格式：
 从原始日期开始，按照子串长度递减的顺序，每行首先输出一个子串和一个空格，然后输出Yes，如果该子串对应的数字是一个素数，否则输出 No。如果这个日期是一个全素日，则在最后一行输出 All Prime!。
 输入样例 1：
 20190523
 输出样例 1：
 20190523 Yes
 0190523 Yes
 190523 Yes
 90523 Yes
 0523 Yes
 523 Yes
 23 Yes
 3 Yes
 All Prime!
 输入样例 2：
 20191231
 输出样例 2：
 20191231 Yes
 0191231 Yes
 191231 Yes
 91231 No
 1231 Yes
 231 No
 31 Yes
 1 No
 */

#include<stdio.h>
#include<math.h>

int isPrime(int x);//是素数返回1；不是素数返回0

int main(){
    int cnt=0,data;
    scanf("%d",&data);
    
    printf("%08d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data=data%10000000;
    
    printf("%07d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=1000000;
    
    printf("%06d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=100000;
    
    printf("%05d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=10000;
    
    printf("%04d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=1000;
    
    printf("%03d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=100;
    
    printf("%02d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    data%=10;
    
    printf("%d",data);
    if(isPrime(data)) printf(" Yes\n");
    else {printf(" No\n");cnt++;}
    
    if(cnt==0) printf("All Prime!\n");
    
    return 0;
}

int isPrime(int x){
    int i;
    if(x<=1) return 0;
    if(x==2) return 1;
    for(i=2;i<=sqrt(x);i++){
        if(x%i==0) return 0;
    }
    return 1;
}
```



### PAT_1115裁判机

```
之前用expendnout函数，在每次有新数字加入后扩充能出现的数字，越到后面需要判断的次数就越多，会导致超时，后改用canExist函数，每次有新数字出现时判断这个数字能不能出现，如果能就直接break出来，一定程度上减少了运行时间，但实质和第一个方法是一样的，取巧了
```

```c
/*有一种数字游戏的规则如下：首先由裁判给定两个不同的正整数，然后参加游戏的几个人轮流给出正整数。要求给出的数字必须是前面已经出现的某两个正整数之差，且不能等于之前的任何一个数。游戏一直持续若干轮，中间有写重复或写错的人就出局。本题要求你实现这个游戏的裁判机，自动判断每位游戏者给出的数字是否合法，以及最后的赢家
 输入格式：
 输入在第一行中给出 2 个初始的正整数，保证都在 [1,10 5  ] 范围内且不相同。
 第二行依次给出参加比赛的人数 N（2≤N≤10）和每个人都要经历的轮次数 M（2≤M≤10 3  ）。
 以下 N 行，每行给出 M 个正整数。第 i 行对应第 i 个人给出的数字（i=1,?,N）。游戏顺序是从第 1 个人给出第 1 个数字开始，每人顺次在第 1 轮给出自己的第 1 个数字；然后每人顺次在第 2 轮给出自己的第 2个数字，以此类推。
 输出格式：
 如果在第k轮，第i个人出局，就在一行中输出Round#k:iisout.。出局人后面给出的数字不算；
 同一轮出局的人按编号增序输出。直到最后一轮结束，在一行中输出 Winner(s): W1 W2 ... Wn，其中 W1 ... Wn 是最后的赢家编号，按增序输出。数字间以 1 个空格分隔，行末不得有多余空格。如果没有赢家，则输出 Nowinner.。
 输入样例 1：
101 42
4 5
59 34 67 9 7
17 9 8 50 7
25 92 43 26 37
76 51 1 41 40
 输出样例 1：
 Round #4: 1 is out.
 Round #5: 3 is out.
 Winner(s): 2 4
 */


#include<stdio.h>
#include<math.h>
#include<stdlib.h>


int n_out[100005] , n_index=0;//已经出现过的数，以及数量
int n_flag[100005];//哈希，每个数字的一个flag，1表示已经出现过，-1表示没有出现过，0表示可以出现
int id_out[20],idout_now=0,idout_ex,idout_flag[20];
                                 //idout_flag用于标记这个id没有出局，1表示没有出局，-1表示出局

void expendnout(void);//作用：根据目前所有n_out中的元素 推断有哪些数可以出现
int canExist(int x);//判断x能不能存在，1表示能存在，0表示不能

int main(){
    int N,M;//N是参与人数，M是轮数
    int num[20][1100];//前面的是人的编号,后面是round轮数
    int n1,n2,n;
    int i,j;
    int round,id;
    
    for(i=0;i<100005;i++) n_flag[i]=-1;
    scanf("%d%d",&n1,&n2);
    n_flag[n1]=1;n_flag[n2]=1;
    n_out[n_index++]=n1;n_out[n_index++]=n2;
//    expendnout();
    scanf("%d%d",&N,&M);
    for(i=1;i<=N;i++) idout_flag[i]=1;
    for(i=1;i<=N;i++){
        for(j=1;j<=M;j++)
            scanf("%d",&num[i][j]);
    }
    
    for(round=1;round<=M;round++){//每一轮
        idout_ex=idout_now;//记录下之前idout数组里面有多少
        
        for(id=1;id<=N;id++){//每个人
            if(idout_flag[id]==-1) continue;
            n=num[id][round];//n是当前人报出的数字
            if(n_flag[n]!=1 && canExist(n)){//这个数字可以出现
                n_flag[n]=1;
                n_out[n_index++]=n;
//                expendnout();
            }
            else{//这个数字不能出现
                id_out[idout_now++]=id;
                idout_flag[id]=-1;
                printf("Round #%d: %d is out.\n",round,id);
            }
            
        }
        
    }
    //所有回合结束，判断out的id的个数是不是所有人
    if(idout_now == N){
        printf("No winner.\n");
        return 0;
    }
    
    printf("Winner(s): ");
    int need_pr=N-idout_now;
    for(i=1;i<=N;i++){
        if(idout_flag[i]==1 && need_pr>1){
            printf("%d ",i);
            need_pr--;
        }
        else if(idout_flag[i]==1 && need_pr==1){
            printf("%d\n",i);
            need_pr--;
        }
    }
    
    
    
    return 0;
}


void expendnout(void){
    int i,j,n;
    for(i=0;i<n_index;i++){
        for(j=i+1;j<n_index;j++){
            n=abs(n_out[i]-n_out[j]);
            if(n_flag[n]==-1) n_flag[n]=0;
        }
    }
}
int canExist(int x){
    int flag=0,i,j;
    for(i=0;i<n_index;i++){
        for(j=i+1;j<n_index;j++){
            if(x==abs(n_out[i]-n_out[j])) {flag=1;break;}
        }
        if(flag) break;
    }
    return flag;
}



/*
 输入样例 2：
42 101
4 5
59 34 67 9 7
17 9 18 50 49
25 92 58 1 39
102 32 2 6 41
 输出样例 2：
 Round #1: 4 is out.
 Round #3: 2 is out.
 Round #4: 1 is out.
 Round #5: 3 is out.
 No winner.
*/
```

