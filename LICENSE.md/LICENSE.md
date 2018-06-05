#include<iostream>
using namespace std;
int n,m,head[100001],f[100001];
struct edge
{
	int next,to;
}k[200001];
int dp(int x)
{
	if(f[x])
		return f[x];
	f[x]=1;
	if(!head[x])
		return f[x];
	int p=head[x];
	do
	{
		f[x]=max(f[x],dp(k[p].to)+1);
		p=k[p].next;
	}while(k[p].next);
	return f[x];
}
int main()
{
	int a,b;
	cin>>n>>m;
	for(int i=1;i<=m;i++)
	{
		cin>>a>>b;
		if(head[b])
		{
			k[i].next=head[b];
			head[b]=i;
		}
		else
			head[b]=i;
		k[i].to=a;
	}
	for(int i=1;i<=n;i++)
		cout<<dp(i)<<endl;
}
