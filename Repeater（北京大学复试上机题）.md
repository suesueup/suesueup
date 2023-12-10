## Repeater（北京大学复试上机题）

 https://www.nowcoder.com/practice/97fd3a67eff4455ea3f4d179d6467de9?tpId=40&tqId=21389&tPage=1&rp=1&ru=/ta/kaoyan&qru=/ta/kaoyan/question-ranking

## 题目描述

![image-20231210092248800](C:\Users\苏苏\AppData\Roaming\Typora\typora-user-images\image-20231210092248800.png)

```
示例输入
```

3

\# #

 \# 

\# #

1

3

\# #

 \# 

\# #

3

4

 OO 

O O

O O

 OO 

2

0

```
示例输出：
```

\# #

 \# 

\# #

\# #  # #     # #  # #

 \#   #      #   # 

\# #  # #     # #  # #

  \# #        # #  

  \#         #  

  \# #        # #  

\# #  # #     # #  # #

 \#   #      #   # 

\# #  # #     # #  # #

​     \# #  # #     

​     \#   #     

​     \# #  # #     

​      \# #      

​       \#       

​      \# #      

​     \# #  # #     

​     \#   #     

​     \# #  # #     

\# #  # #     # #  # #

 \#   #      #   # 

\# #  # #     # #  # #

  \# #        # #  

  \#         #  

  \# #        # #  

\# #  # #     # #  # #

 \#   #      #   # 

\# #  # #     # #  # #

   OO OO   

  O OO O  

  O OO O  

   OO OO   

 OO     OO 

O O    O O

O O    O O

 OO     OO 

 OO     OO 

O O    O O

O O    O O

 OO     OO 

   OO OO   

  O OO O  

  O OO O  

   OO OO   

## 思路

用一个二维数组mould储存模板，这个模板就是每次repeat使用的。用temp储存repeat的中间过程，用picture储存repeat的结果。这里有一点需要注意，repeat的数目是输入的q的数目减一。

  ***repeat的过程是这样的，遍历模板，在模板是空格的地方，在picture相应的位置放一个与上一步repeat结果大小一样的空白区，如果模板不是空格（有图形），那就在picture相应的位置放上上一步repeat的结果图形。*** 

  这道题很有趣味，因为题意难以理解，这道题里repeat的题意是用分形的方式，把原图形扩大一下，就是把原图形看做一个元素，在模板有图形的地方用这个元素替换。设模板大小是m_size，每次repeat，最终图形的大小变成原来大小的m_size倍。

————————————————

版权声明：本文为CSDN博主「ujingzanghai」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/ujingzanghai/article/details/79163851

```c++
#include <cstring>
#include <iostream>
using namespace std;
 
char mould[7][7];
char picture[3005][3005];
char temp[3005][3005];

 //用模板填充
void duplicate(int m_size, int p_left, int p_top)
{
    for(int i = 0; i < m_size; i++)
    {
        for(int j = 0; j < m_size; j++)
        {
            picture[p_left + i][p_top + j] = temp[i][j];
        }
    }
}
 //用空格填充
void enblank(int m_size, int p_left, int p_top)
{
    for(int i = 0; i < m_size; i++)
    {
        for(int j = 0; j < m_size; j++)
        {
            picture[p_left + i][p_top + j] = ' ';
        }
    }
}
 
int repeater(int m_size, int repeater_times)
{
    int n = m_size;
    while(--repeater_times)
    {
        for(int i = 0; i < m_size; i++)
        {
            for(int j = 0; j < m_size; j++)
            {
                if(mould[i][j] != ' ')
                    duplicate(n, n*i, n*j);
                else
                    enblank(n, n*i, n*j);
            }
        }
        n *= m_size;
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < n; j++)
            {
                temp[i][j] = picture[i][j];
            }
        }
    }
    return n;
}
 
int main()
{
    int n, q;
    while((scanf("%d", &n) != EOF) && n != 0)
    {
        getchar();
        for(int i = 0; i < n; i++)
        {
            gets(mould[i]);
            strcpy(temp[i], mould[i]);
            strcpy(picture[i], mould[i]);
        }
        scanf("%d", &q);
        getchar();
        n = repeater(n, q);
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < n; j++)
            {
                printf("%c", picture[i][j]);
            }
            printf("\n");
        }
    }
        return 0；
}
```

