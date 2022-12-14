@author:  yangyuyan

@time:  2022年9月3日

---

# 我的学习报告

## 学习内容10：Git 学习

时间： 2022年9月14日

### Git的基本初级指令

#### git使用前的配置

**在使用Git之前，需要告诉Git你是谁，在向Git仓库中提交时需要用到。**

* 配置提交人姓名：git config --global user.name 提交人的姓名
* 配置提交人邮箱：git config --global user.email 提交人邮箱
* 查看git配置信息：git config --list

**注意**

* 如果要对配置信息进行修改，重复上述命令即可。
* 配置只需要执行一次。

***



#### git提交操作

* git init 初始化git仓库
* git status 查看文件状态
* git add 文件列表     追踪文件(其实就是将项目文件提交到暂存区)
* git reset  文件列表  （将项目文件从暂存区移出）
* git commit -m 提交信息       向仓库中提交代码（将暂存区中的文件提交到仓库中）
* git log 查看提交记录

***

#### git撤销操作

* 用暂存区中的文件覆盖工作目录中的文件： **git checkout** 文件     **而且用暂存区的文件覆盖工作目录的文件后，缓存区的原文件依然存在。**
* 将文件从缓存区删除：**git rm --cached**  文件
* 将git仓库中指定的更新记录恢复过来，并且覆盖暂存区和工作目录：**git rest --hard commit ID**

***

### Git进阶操作

#### 分支种类

**为了便于理解，我们暂时可以认为分支就是工作目录中代码的一份副本，使用分支可以让我们从开发主任务上分离出来，以免影响开发主线。**

1. **主分支(master)**：第一次向git仓库中提交的更新数据时自动产生的一个分支。
2. **开发分支(develop)**：作为开发的分支,基于master分支创建。
3. **功能分支(feature)**:作为开发分支具体功能的分支，基于开发分支创建。开发一个独立的功能，当功能开发完成后，再将功能分支的代码合并到开发分支中，这是功能分支就可以删除了。当开发分支累计到一定程度时，再将开发分支的代码合并到主分支上。

#### 分支操作

>git branch <u>查看分支</u>(查看当前位于哪个分支中，以及总共有几个分支)
>
>git branch 分支名称 <u>创建分支</u>
>
>git checkout 分支名称 <u>切换分支</u>
>
>git merge 来源分支 <u>合并分支</u>
>
>git branch -d 分支名称 <u>删除分支</u>（**分支被合并后才允许删除**） （-D强制删除）

* **需要特别注意的是分支与分支之间应该是相互独立的，没有任何联系。所以在切换分支之前，当前分支上的工作一定要提交到Git仓库中，要保持当前分支上的工作区是完全干净的状态，否则就会出现问题。**
*  **用合并分支命令时 （如将开发分支合并到主分支上）应先将分支调到主分支上，然后再在主分支上输入命令“ git merge develop"，这样开发分支就合并到主分支上了。应该注意的是虽然我们的开发分支已经合并到主分支上了，但是开发分支依旧存在，合并完开发分支后，我们仍然可以切换到开发分支上继续开发。也就是说合并分支其实是将开发分支上的文件提交到主分支上。**
* **需要注意的是如果你要删除的分支没有被合并过，一般情况下，这个分支是不允许删除的。而且我们不能从当前分支上删除当前分支，只能从别的分支上删除当前分支。**

在git中，可以暂时提取分支上的所有的改动并储存，让开发人员得到一个干净的工作副本，临时转向其他工作。

使用场景：**分支临时切换**

* 储存临时改动：<u>git stash</u>
* 恢复改动：<u>git stash pop</u>

**需要特别注意的是git提供的储存功能是独立于分支的，也就是说在其他分支上也可以执行恢复改动这个命令，如果在其他分支上执行这个命令，就会将改动恢复到其他分支上。**

***

## 学习内容2：数据结构中线性表的操作

***



时间： 2022年9月15日

### 线性表

**线性表可以采取顺序储存和链式储存两种。采用顺序存储结构是表示线性表最简单的方法，具体做法是将线性表的元素一个接着一个的存储在一片相邻的储存空间。这种顺序表示的线性表也叫做<u>顺序表.</u>**

1. **顺序表的数据结构定义**

```c
#include<stdio.h>
#include<stdlib.h>
typedef int DataType;
struct seqList
{//有3个数据成员
  int MAXNUM;//用于记录顺序线性表中能存放的最大元素个数的 整型 MAXNUM   
  int curNum;//用于存放顺序线性表中数据元素的个数  整型  curNum
  DataType *element;//用于存放顺序线性表数据元素的连续空间的起始地址  
};
typedef struct seqList* PseqList;
```

2. **创建一个空的线性顺序表**

```c
PseqList createNullList(int m)//创建一个空的顺序表，能存放的最大元素个数为m
{
  if(m==0)
  return NULL;
   PseqList p=(PseqList)malloc(sizeof(struct seqList));
   if(p!=NULL)
   {
       p->element=(DataType*)(sizeof(DateType)*m);
       if(p->element!=NULL)
       {
           p->MAXNUM=m;
           P->curNum=0;
           return p;
       }
       else free(p);
   }
    return NULL;
    
}
```

3. **判断线性表是否已经满并在线性表下标为p的位置插入元素**

```c
int isFullList_seq(PseqList L)
{
    if(p->curNum>=MAXNUM||p<0)
    {
        return 1;
    }
    return 0;
}
```

```c
int insertPre(PseList L, int p , int x)
{
    isFullList_seq(L);
    int i;
    for(i=L->curNum;i>p;i--)
    {
        L->element[i]=L->element[i-1];
    }
      L->element[p]=x;
      L->curNum++;
    return 1;
}
```

4. 销毁的线性表

```c
int destroyList_seq(PseqList L)
{
    //返回值为销毁的线性表中现有数据元素的个数，若待销毁的线性表不存在，则返回0
    if(L==NULL) {
    return NULL;
    }
    int num = L->curNum;
    free(L->element);
    free(L);
    return num;
}
```

5. 顺序表的删除

```c
int deletePos_seq(PseqList L,int pos)
{//在顺序表L中删除与下标pos处的数据元素，若pos非法，则返回-1；否则返回1
    if(pos<0||pos>=L->curNum)
    {
      return -1;
    }
    int i;
    for(i=pos;i<L->curNum-1;i++)
    {
      L->element[i]=L->element[i+1]; 
    }
    L->curNum=L->curNum-1;
    return 1;
}
```

6. 将顺序表中数值的替换

```c
void replace_seq(PseqList L,int x,int y)
{//将顺序表L中值为x的数据元素替换为y
   int i;
   for(i=0;i<L->curNum;i++)
   {
     if(L->element[i]==x)
     {
       L->element[i]=y;
     }
   }

}
```



## 学习内容3：数据结构中栈的操作

***



时间： 2022年9月16日

**栈的基本概念**

**栈是一种特殊的线性表，它的所有的插入和删除操作都限制在表的同一端进行。表中允许进行插入、删除操作的一段叫做栈顶，另一端叫做栈底。当栈中没有元素时，称为空栈。栈的插入操作通常称为进栈或者入栈，栈的删除操作通常称为退栈或者出栈。**

1. 栈的数据结构定义

```c
struct SeqStack{
    int MAXNUM;//栈中最大元素个数
    int t;//t<MAXNUM，指示栈顶的位置，而不是元素个数
    DataTpye *s;
};
typedef struct SeqStack * PSeqStack;
```

2. 栈的链接表示

```c
struct Node;
typedef struct Node * PNode;
struct Node{
    DataType info;
    PNode link;
};
struct LinkStack
{
    PNode top;
};
typedef struct LinkStack * PLinkStack;
```

3. 创建一个空栈

```c
PlinkStack createEmptyStack_link(void)
{
    PlinkStack plstack;
    plstack=(PLinkStack)malloc(sizeof(struct LinkStack));
    if(plstack!=NULL)
    {
        plstack->top=NULL;
    }
    else
    printf("Out of space!\n");
    return plstack;
}
```

4. 进栈&&出栈

```c
void push_link(PLinkStack plstack,DataType x)
{
    PNode p;
    p=(PNode)malloc(sizeof(struct Node));
    if(p==NULL)
    {
        printf("Out of space!\n");
    }
    else
    {
        p->info=x;
        p->link=plstack->top;
        plstack->top=p;
    }
}
```

```c
void pop_link(PLinkStack plstack)
{
    PNode p;
    if(isEmptyStack_link(plstack))
    {
        printf("Empty stack pop.\n");
    }
    else
    {
        p=plstack->top;
        plstack->top=plstack->top->link;
        free(p);
    }
}

```



# 时间表（此处为1级标题）


| 学习内容               | 时间          |
| ---------------------- | ------------- |
| Git学习                | 2022年9月14日 |
| 数据结构中线性表的操作 | 2022年9月15日 |
| 数据结构中栈的操作     | 2022年9月16日 |
# 图片

![](assets/HarryPotter.md.jpeg)
=======
![HarryPotter1.md](assets/HarryPotter1.md.jpeg)



