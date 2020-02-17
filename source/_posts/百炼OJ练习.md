---
title: 百炼OJ-C++练习
date: 2019-12-1 10:30:13
tags: 
- 编程
- OJ
- 练习
categories:
- 编程
- OJ
---
# 自己在百炼OJ上练习的一些算法题

## 1088
``` cpp
//http://bailian.openjudge.cn/practice/1088/
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
#include<cmath>
#include<string>
using namespace std;
const int dx[4]={1,-1,0,0};
const int dy[4]={0,0,1,-1};
int moun[105][105];
int cnt[105][105];
int R,C;
int dfs(int x,int y){
    if(cnt[x][y]>=0) return cnt[x][y];
    int ans=0;
    for(int i=0;i<4;++i){
        int nx=x+dx[i],ny=y+dy[i];
        if(nx>0&&nx<=R&&ny>0&&ny<=C&&moun[nx][ny]<moun[x][y]) 
            ans=max(ans,1+dfs(nx,ny));
    }
    return cnt[x][y]=ans;
}
int main(){
    scanf("%d%d",&R,&C);
    memset(cnt,-1,sizeof(cnt));
    for(int i=1;i<=R;++i) for(int j=1;j<=C;++j) scanf("%d",&moun[i][j]);
    int ans=0;
    for(int i=1;i<=R;++i) for(int j=1;j<=C;++j) 
        ans=max(ans,dfs(i,j));
    ++ans;
    printf("%d\n",ans);
    return 0;
}
```
## 1163

``` cpp

#include <iostream>    
#include <algorithm>   
#define MAX 101    
using namespace std;   
int D[MAX][MAX];    
int n;    
int MaxSum(int i, int j){      
    if(i==n)    
        return D[i][j];      
    int x = MaxSum(i+1,j);      
    int y = MaxSum(i+1,j+1);      
    return max(x,y)+D[i][j];    
}  
int main(){      
    int i,j;      
    cin >> n;      
    for(i=1;i<=n;i++)     
        for(j=1;j<=i;j++)          
            cin >> D[i][j];      
    cout << MaxSum(1,1) << endl;    
}    
```
## 1191
``` cpp
#include <iostream>
#include <cmath>
#include <iomanip>
#define inf 6400*6400*15
using namespace std;
int map[8][8],n;
double m=0,mn=inf;
double add(int x1,int x2,int y1,int y2){
    double sm=0;
    for(int i=x1;i<x2;i++)
        for(int j=y1;j<y2;j++)
            sm+=map[i][j];
    return sm;
}
double dfs(int u,int d,int l,int r,int dep,double sm){
    if(dep==n){
        double x=add(u,d,l,r);
        return (x-m)*(x-m);
    }
    for(int i=u+1;i<d;i++){
        double x=add(u,i,l,r);
        sm+=(x-m)*(x-m);
        if(sm>=mn){
            sm-=(x-m)*(x-m);
            continue;
        }
        double y=dfs(i,d,l,r,dep+1,sm);
        if(sm+y<mn) mn=sm+y;
        sm-=(x-m)*(x-m);
    }
    for(int i=u+1;i<d;i++){
        double x=add(i,d,l,r);
        sm+=(x-m)*(x-m);
        if(sm>=mn){
            sm-=(x-m)*(x-m);
            continue;
        }
        double y=dfs(u,i,l,r,dep+1,sm);
        if(sm+y<mn) mn=sm+y;
        sm-=(x-m)*(x-m);
    }
    for(int i=l+1;i<r;i++){
        double x=add(u,d,l,i);
        sm+=(x-m)*(x-m);
        if(sm>=mn){
            sm-=(x-m)*(x-m);
            continue;
        }
        double y=dfs(u,d,i,r,dep+1,sm);
        if(sm+y<mn) mn=sm+y;
        sm-=(x-m)*(x-m);
    }
    for(int i=l+1;i<r;i++){
        double x=add(u,d,i,r);
        sm+=(x-m)*(x-m);
        if(sm>=mn){
            sm-=(x-m)*(x-m);
            continue;
        }
        double y=dfs(u,d,l,i,dep+1,sm);
        if(sm+y<mn) mn=sm+y;
        sm-=(x-m)*(x-m);
    }
    return inf;
}
int main(){
    cin>>n;
    double sm=0;
    for(int i=0;i<8;i++)
        for(int j=0;j<8;j++){
            cin>>map[i][j];
            sm+=map[i][j];
        }
    m=sm/n;
    dfs(0,8,0,8,1,0);
    if(n==1)
        mn=0;
    cout<<fixed<<setprecision(3)<<sqrt(mn/n)<<endl;
    return 0;
}
```

## 2339

``` cpp
#include<iostream>
using namespace std;
int main()
{
	int M,N,T;
	cin>>M>>N>>T;
	char ch;
	char s[100][100]={0};
	for(int i=0;i<M;i++)
		for(int j=0;j<N;j++)
		cin>>s[i][j];
	for(int t=0;t<T;t++)
		for(int i=0;i<M-1;i++)
			for(int j=0;j<N-1;j++)
			if(s[i][j])	
	(ch=cin.get())=='R'
	return 0;
}
```
## 2682

``` cpp
#include<iostream>
#include<vector>
#include<map>
#include<algorithm>
using namespace std;
const int MAXSIZE=10000;
int main()
{
	int N,M;
	cin>>N>>M;
	int s[MAXSIZE]={0};
	for(int i=0;i<N;i++)
	cin>>s[i];
		for(int j=0;j<M;j++)
		*(s+N+j)=*(s+j+N-M);
		for(int j=0;j<N-M;j++)
		*(s+N+M+j)=*(s+j);
		for(int j=0;j<N;j++)
		*(s+j)=*(s+N+j);
	for(int i=0;i<N;i++)
	cout<<s[i]<<" ";
	return 0;
 } 
```

## 2694
``` cpp
#include<cstdlib>
#include<cstdio>
using namespace std;
char k[30];
double f(){
	scanf("%s",k);
	switch(k[0]){
		case '+':return f()+f();
		case '-':return f()-f();
		case '*':return f()*f();
		case '/':return f()/f();
		default:return atof(k);}}
int main(){
	printf("%f",f());
	return 0;}
```

## 2712
``` cpp
#include<iostream>
using namespace std;
const int mon[13]={0,31,28,31,30,31,30,31,31,30,31,30,31};
int interval(int m1,int d1,int m2,int d2)
{
	if(m1==m2)
	return d2-d1;
	else
	{
		int t=m2-m1;
		int sum=mon[m1]-d1;
		while(--t)
		sum=sum+mon[++m1];
		sum+=d2;
		return sum;
	}	
}
int main()
{
	int N,iter;
	cin>>N;
	int m1[10000]={0};
	int d1[10000]={0};
	int m2[10000]={0};
	int d2[10000]={0};
	long long c[10000]={0};
	for(int i=0;i<N;i++)
	{
		cin>>m1[i]>>d1[i]>>c[i]>>m2[i]>>d2[i];
		iter=interval(m1[i],d1[i],m2[i],d2[i]);
		for(int j=0;j<iter;j++)
		c[i]=2*c[i];
	}	
	for(int i;i<N;i++)
	cout<<c[i]<<endl;	
	return 0;
}
```

## 2943
``` cpp
#include<iostream>
#include<algorithm>
#include<vector>
#include<string>
#include<map>
using namespace std;

bool compare(int a,int b)
{
	return a>b;
}

int main()
{
	int N;
	cin>>N;
	vector<int> weight;
	int temp;
	string s1;
	map<int,string> mapcolor;
	for(int i=0;i<N;i++)
	{
		cin>>temp;
		weight.push_back(temp);
		cin>>s1;
		mapcolor[temp]=s1;
	}
	sort(weight.begin(),weight.end(),compare);
	vector<int>::iterator it=weight.begin();
	for(int i=0;i<N;i++)
	{
		cout<<mapcolor[*it++]<<endl;
	}
	return 0;
}	
```
## 2975
``` cpp
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
#include<cmath>

using namespace std;
char key[30]="VWXYZABCDEFGHIJKLMNOPQRSTU";
char buf[20];
int main(){
    while(1){
        gets(buf);
        if(strlen(buf)>7) break;
        char ch;
        while(1)
		{ch=getchar();
        if(ch=='\n') break;
        if(ch>='A'&&ch<='Z') putchar(key[ch-'A']);
        else putchar(ch);
        }
        putchar('\n');
        gets(buf);
    }
}
```
## 4148
``` cpp
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	int s[10000][4]={0};
	int k[1000]={0};
	int M=0;
	for(int i=0;i<10000;i++)
	{
		for(int j=0;j<4;j++)
		cin>>s[i][j];
		if(s[i][0]==-1&&s[i][1]==-1&&s[i][2]==-1&&s[i][3]==-1)
		break;
		k[i]=1;
		while(!(((k[i]-s[i][0])%23==0)&&((k[i]-s[i][1])%28==0)&&((k[i]-s[i][2])%33==0)))
		{
			if(k[i]==21252) break;
		 	k[i]++;
		}
		k[i]=k[i]-s[i][3];
		M++;		
	}
	for(int i=1;i<=M;i++)
	cout<<"Case "<<i<<": the next triple peak occurs in "<<k[i-1]<<" days."<<endl;
	return 0;	
 } 

```

# 往年考试题
## A
``` cpp
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
	int N;
	cin>>N;
	int flag=0;
	int b[101]={0};
	for(int i=2;i<=100;i++)
	while(N%i==0)
	{
		N=N/i;
		b[i]++;
	}
	for(int i=2;i<=100;i++)
	{
		if(b[i]>=2&&flag==0)
		{cout<<i<<"^"<<b[i];flag=1;}
		else if(b[i]==1&&flag==0)
		{cout<<i;flag=1;}
		else if(b[i]>=2&&flag==1)
		cout<<"*"<<i<<"^"<<b[i];	
		else if(b[i]==1&&flag==1)
		cout<<"*"<<i;
		else continue;		
	}	
	return 0;
}
```
## B
``` cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
	string s1;
	char s[12]={0};
	int sum=0;
	int b[12]={0};
	cin>>s1;
	for(int i=0;i<12;i++)
	{cin>>s[i];
	b[i]=(int)(s[i]-('0'));}	
	cout<<s1<<endl;
	sum=b[0]*1+b[2]*2+b[3]*3+b[4]*4+b[6]*5+b[7]*6+b[8]*7+b[9]*8+b[10]*9;
	sum=sum%11;
	if(sum==b[12])
	cout<<"Right";
	else
	{
		for(int i=0;i<12;i++)
		cout<<s[i];
		cout<<sum;
	}	
	return 0;	
}
```

## C
``` cpp
#include "stdafx.h"  
#include "iostream"  
#include "queue"  
using namespace std;  
  
template<class DistType/*边的权值的类型*/>   
class Edge//边的定义  
{  
public:  
    Edge(int dest, DistType weight)  
    {  
        m_nposTable=dest;  
        m_distWeight=weight;   
        m_pnext=NULL;  
    }  
    ~Edge()  
    {  
  
    }  
public:  
    int m_nposTable;//该边的目的顶点在顶点集中的位置  
    DistType m_distWeight;//边的权重值  
    Edge<DistType> *m_pnext;//下一条边（注意不是下一个顶点，因为m_nposTable已经知道了这个顶点的位置）  
};  
//声明  
template<class NameType/*顶点集名字类型*/, class DistType/*距离的数据类型*/> class Graph;  
  
template<class NameType/*顶点集名字类型*/, class DistType/*距离的数据类型*/>   
class Vertex//顶点的定义  
{  
public:  
    Vertex()  
    {  
        padjEdge=NULL;  
        m_vertexName=0;  
    }  
    ~Vertex()  
    {  
        Edge<DistType> *pmove = padjEdge;  
        while (pmove)  
        {  
            padjEdge = pmove->m_pnext;  
            delete pmove;  
            pmove = padjEdge;  
        }  
    }  
  
private:  
    friend class Graph<NameType,DistType>;//允许Graph类任意访问  
    NameType m_vertexName;//顶点中的数据内容  
    Edge<DistType> *padjEdge;//顶点的邻边  
  
};  
  
  
template<class NameType/*顶点集名字类型*/, class DistType/*距离的数据类型*/>   
class Graph  
{  
public:  
    Graph(int size = m_nDefaultSize/*图顶点集的规模*/)  
    {  
        m_pVertexTable = new Vertex<NameType, DistType>[size];  //为顶点集分配内存  
        if (m_pVertexTable == NULL)  
        {  
            exit(1);  
        }  
        m_numVertexs=0;  
        m_nmaxSize=size;  
        m_nnumEdges=0;  
    }  
  
    ~Graph()  
    {  
        Edge<DistType> *pmove;  
        for (int i=0; i < this->m_numVertexs; i++)  
        {  
            pmove = this->m_pVertexTable[i].padjEdge;  
            if (pmove){  
                this->m_pVertexTable[i].padjEdge = pmove->m_pnext;  
                delete pmove;  
                pmove = this->m_pVertexTable[i].padjEdge;  
            }  
        }  
        delete[] m_pVertexTable;  
    }  
    int GetNumEdges()  
    {//获得边的数目  
        return m_nnumEdges/2;  
    }  
    int GetNumVertexs()  
    {//获得顶点数目  
        return m_numVertexs;  
    }  
  
    bool IsGraphFull() const  
    {     //图满的?  
        return m_nmaxSize == m_numVertexs;  
    }  
    //在顶点集中位置为v1和v2的顶点之间插入边  
    bool InsertEdge(int v1, int v2, DistType weight=m_Infinity);   
    //插入顶点名字为vertex的顶点  
    bool InsertVertex(const NameType vertex);    
    //打印图  
    void PrintGraph();     
    //顶点v到其他各个顶点的最短路径（包括自身）  
    void Dijkstra(int v, DistType *shotestpath);  
    //获取顶点集中位置为v1和v2的顶点之间边的权重值  
    DistType GetWeight(int v1, int v2);   
    //获得在顶点集中的位置为v的顶点的名字  
    NameType GetVertexValue(int v);  
    //用该顶点的名字来寻找其在顶点集中的位置  
    int GetVertexPosTable(const NameType vertex);    
  
  
    //深度搜索优先  
    void DFS(int v, int *visited);        
    void DFS();  
    //广度优先搜索  
    void BFS(int v, int *visited);  
    void BFS();  
    //获取第v个顶点的名字（或者说内容）  
    NameType GetVertexName(int v);     
    //获得顶点v的第一个相邻顶点，如果没有就返回-1  
    int GetFirst(int v);         
    //获得顶点v1的邻点v2后的邻点  
    int GetNext(int v1, int v2);  
  
private:  
    Vertex<NameType, DistType> *m_pVertexTable;   //顶点集  
    int m_numVertexs;//图中当前的顶点数量  
    int m_nmaxSize;//图允许的最大顶点数  
    static const int m_nDefaultSize = 10;       //默认的最大顶点集数目  
    static const DistType m_Infinity = 65536;  //边的默认权值（可以看成是无穷大）  
    int m_nnumEdges;//图中边的数目  
      
};  
  
  
//返回顶点vertexname在m_pVertexTable(顶点集)中的位置  
//如果不在顶点集中就返回-1  
template<class NameType, class DistType>   
int Graph<NameType, DistType>::GetVertexPosTable(const NameType vertexname)  
{  
    for (int i=0; i < this->m_numVertexs; i++)  
    {  
        if (vertexname == m_pVertexTable[i].m_vertexName)  
        {  
            return i;  
        }  
    }  
    return -1;  
}  
  
//打印图中的各个顶点及其链接的边的权重  
template<class NameType, class DistType>   
void Graph<NameType, DistType>::PrintGraph()  
{  
    Edge<DistType> *pmove;  
    for (int i=0; i<this->m_numVertexs; i++)  
    {  
        cout << this->m_pVertexTable[i].m_vertexName << "->";  
        pmove = this->m_pVertexTable[i].padjEdge;  
        while (pmove)  
        {  
            cout << pmove->m_distWeight << "->" << this->m_pVertexTable[pmove->m_nposTable].m_vertexName << "->";  
            pmove = pmove->m_pnext;  
        }  
        cout << "NULL" << endl;  
    }  
}  
//获得在顶点集中的位置为v的顶点的名字  
template<class NameType, class DistType>   
NameType Graph<NameType, DistType>::GetVertexValue(int v)  
{  
    if (v<0 || v>=this->m_numVertexs)  
    {  
        cerr << "查找的顶点位置参数有误，请检查！" <<endl;  
        exit(1);  
    }  
    return m_pVertexTable[v].m_vertexName;  
  
}  
//返回顶点v1和v2之间的边权值，  
//如果没有直接相连（即不是一条边直接相连）则返回无穷大  
template<class NameType, class DistType>   
DistType Graph<NameType, DistType>::GetWeight(int v1, int v2)  
{  
    if (v1>=0 && v1<this->m_numVertexs && v2>=0 && v2<this->m_numVertexs)  
    {  
        if (v1 == v2)  
        {  
            return 0;  
        }  
        Edge<DistType> *pmove = m_pVertexTable[v1].padjEdge;  
        while (pmove)  
        {  
            if (pmove->m_nposTable == v2)  
            {  
                return pmove->m_distWeight;  
            }  
            pmove = pmove->m_pnext;  
        }  
    }  
      
    return m_Infinity;    
}  
  
//顶点依次插入到分配好的顶点集中  
template<class NameType, class DistType>   
bool Graph<NameType, DistType>::InsertVertex(const NameType vertexname)  
{  
    if (IsGraphFull())  
    {  
        cerr<<"图已经满，请勿再插入顶点！"<<endl;  
        return false;  
    }else  
    {  
        this->m_pVertexTable[this->m_numVertexs].m_vertexName = vertexname;  
        this->m_numVertexs++;  
    }  
      
    return true;  
}  
  
//在顶点集位置为v1和v2的顶点之间插入权值为weght的边（务必保持输入的准确性，否则.....）  
template<class NameType, class DistType>   
bool Graph<NameType, DistType>::InsertEdge(int v1, int v2, DistType weight)  
{  
    if (v1 < 0 && v1 > this->m_numVertexs && v2 < 0 && v2 > this->m_numVertexs)  
    {  
        cerr<<"边的位置参数错误，请检查！ "<<endl;  
        return false;  
    }  
    else  
    {  
        Edge<DistType> *pmove = m_pVertexTable[v1].padjEdge;  
        if (pmove == NULL)//如果顶点v1没有邻边  
        { //建立顶点v1的第一个邻边(该邻边指明了目的顶点)  
            m_pVertexTable[v1].padjEdge = new Edge<DistType>(v2, weight);  
            m_nnumEdges++;//图中边的数目  
            return true;  
        }else//如果有邻边  
        {  
            while (pmove->m_pnext)  
            {  
                pmove = pmove->m_pnext;  
            }  
                pmove->m_pnext = new Edge<DistType>(v2, weight);  
                m_nnumEdges++;//图中边的数目  
                return true;  
        }  
    }  
}  
  
  
template<class NameType, class DistType>  
void Graph<NameType, DistType>::Dijkstra(int v, DistType *shPath)  
{  
    int num =GetNumVertexs();  
    int *visited = new int[num];  
    for (int i=0; i < num; i++)  
    {//初始化  
        visited[i] = 0;//未访问  
        shPath[i] = this->GetWeight(v, i);//顶点v（当前中间点）到各个相邻顶点的边权值，其他情况返回无穷大  
    }  
  
    visited[v] = 1;//第v个顶点初始化为被访问，并以他为中点点开始找最短路径  
  
    for (int i = 1; i < num; i++)  
    {  
        DistType min = this->m_Infinity;  
        int u=0;  
          
        //寻找新的中间点u，依据就是数组中权值最小的那个点的位置（且没被访问过）  
        for (int j=0; j < num; j++)  
        {     
            if (!visited[j])  
            {  
                if (shPath[j]<min)  
                {  
                    min = shPath[j];//获得当前shPath数组中的最小边权重  
                    u = j;//用u来记录获取最小值时的顶点位置,即新的中间点  
                }  
            }  
        }  
  
        visited[u] = 1;//已经确定的最短路径  
  
        //以u为中间点寻找顶点v到顶点w的最短路径  
        for (int w=0; w < num; w++)  
        {    
            DistType weight = this->GetWeight(u, w);//顶点u（当前中间点）到各个相邻顶点的边权值，其他情况返回无穷大  
            if (!visited[w] && weight != this->m_Infinity )  
            {  
                if ( shPath[u]+weight < shPath[w] )  
                {  
                    shPath[w] = shPath[u] + weight;//更新顶点v到w的最短路径值  
                }  
            }  
        }  
    }  
    delete[] visited;  
}  
//获得顶点v1的邻点v2后的邻点  
template<class NameType, class DistType>   
int Graph<NameType, DistType>::GetNext(int v1, int v2)  
{  
    if (-1 != v1)  
    {  
        Edge<DistType> *pmove = this->m_pVertexTable[v1].padjEdge;  
        while (NULL != pmove->m_pnext)  
        {  
            if (pmove->m_nposTable==v2)  
            {  
                return pmove->m_pnext->m_nposTable;  
            }  
            pmove = pmove->m_pnext;  
        }          
    }  
    return -1;  
}  
  
//从第v个顶点开始深度遍历  
template<class NameType, class DistType>   
void Graph<NameType, DistType>::DFS(int v, int *visited)  
{  
    cout << "->" << this->GetVertexName(v);  
    visited[v] = 1;  
    int firstVertex = this->GetFirst(v);//获得顶点v的第一个相邻顶点，若没有则返回-1  
    while (-1 != firstVertex)  
    {  
        if (!visited[firstVertex])//如果没有访问过  
        {  
            cout << "->" << this->GetWeight(v, firstVertex);//获得顶点v及其邻点firstVertex之间的权值  
            DFS(firstVertex, visited);  
        }  
        firstVertex = this->GetNext(v, firstVertex);//获得顶点v的邻点firstVertex后的邻点，如果没有就返回-1  
    }  
}  
  
template<class NameType, class DistType>   
void Graph<NameType, DistType>::DFS()  
{  
    int *visited = new int[this->m_numVertexs];  
    for (int i=0; i<this->m_numVertexs; i++)  
    {  
        visited[i] = 0;  
    }  
    cout << "head";  
    DFS(0, visited);//从第一个顶点开始遍历  
    cout << "--->end";  
}  
  
template<class NameType, class DistType>   
void Graph<NameType, DistType>::BFS()  
{  
    int *visited = new int[this->m_numVertexs];  
    for (int i=0; i<this->m_numVertexs; i++)  
    {  
        visited[i] = 0;  
    }  
    cout << "head";  
    BFS(0, visited);//从第一个顶点开始遍历  
    cout << "--->end";  
}  
  
//从第v个顶点开始广度遍历  
template<class NameType, class DistType>   
void Graph<NameType, DistType>::BFS(int v, int *visited)  
{  
    cout << "->" << this->GetVertexName(v);  
    visited[v]=1;  
    queue<int> que;//=new queue<int>[this->GetNumVertexs()];  
    que.push(v);//进队（队列的末端）  
    while (!que.empty())  
    {  
        v=que.front();//出队首元素  
        que.pop();//删除队首元素  
        int firstvertex=GetFirst(v);  
        while(firstvertex != -1)  
        {  
            if (!visited[firstvertex])  
            {  
                cout << "->" << this->GetWeight(v, firstvertex);//获得顶点v及其邻点firstVertex之间的权值  
                que.push(firstvertex);  
                visited[firstvertex]=1;  
                cout << "->" << this->GetVertexName(firstvertex);  
            }  
            firstvertex=GetNext(v,firstvertex);  
        }  
    }  
}  
  
//获得在顶点集中的位置为v的顶点的名字  
template<class NameType, class DistType>   
NameType Graph<NameType, DistType>::GetVertexName(int v)  
{  
    if (v<0 || v>=this->m_numVertexs)  
    {  
        cerr << "查找的顶点位置参数有误，请检查！" <<endl;  
        exit(1);  
    }  
    return m_pVertexTable[v].m_vertexName;  
  
}  
  
//获得顶点v的第一个相邻顶点，如果没有就返回-1  
template<class NameType, class DistType>   
int Graph<NameType, DistType>::GetFirst(int v)  
{  
    if (v<0 || v>=this->m_numVertexs)  
    {  
        return -1;  
    }  
    Edge<DistType> *ptemp = this->m_pVertexTable[v].padjEdge;  
    return m_pVertexTable[v].padjEdge ? m_pVertexTable[v].padjEdge->m_nposTable : -1;  
}  
```
## D
``` cpp
http://bailian.openjudge.cn/practice/2386/
#include<iostream>
using namespace std;

	int M,N;
	char s[100][100];
void dfs(int x,int y)
{
	s[x][y]='.';
	for(int dx=-1;dx<=1;dx++)
	{
		for(int dy=-1;dy<=1;dy++)
		{
			int nx=x+dx,ny=y-dy;
			if(0<=nx&&nx<N&	&0<=ny&&ny<M&&s[nx][ny]=='W')
			dfs(nx,ny);
		}	
	}
	return;
}
int main()
{
	cin>>N>>M;
	for(int i=0;i<N;i++)
	for(int j=0;j<M;j++)
	cin>>s[i][j];
	int res=0;
	for(int i=0;i<N;i++)
	{
		for(int j=0;j<M;j++)
		{
			if(s[i][j]=='W')
			{
				dfs(i,j);
				res++;
				}				
		}
	}	
	cout<<res;
	return 0;
}

```
## E
``` cpp
#include<iostream>
using namespace std;
int main(){
	int d,p,e,i,x;
	int count=0;
	while(cin>>p>>e>>i>>d&&p!=-1&&i!=-1&&e!=-1&&d!=-1){
		count++;
		if(p==0||e==0||i==0){
			cout<<"Case "<<count<<": the next triple peak occurs in "<<21252-d<<" days."<<endl;
		}
		else{
			for(x=i;x<21252;x+=33){
				if(x%23==p%23&&x%28==e%28){
					break;
				}	
			}
			cout<<"Case "<<count<<": the next triple peak occurs in "<<x-d<<" days."<<endl;	
		}
	}
	return 0;
} 
```
## practice
``` cpp
//stack
#include<iostream>
#include<stack>
using namespace std;
int main()
{
	stack<int> s;
	s.push(1);
	s.push(2);	
	s.push(3);	
	cout<<s.top()<<endl;
    int u;
	u=s.pop();	
	cout<<u<<endl;
	return 0;
}

```