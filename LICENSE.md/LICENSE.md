#include<iostream>
#include<queue>
using namespace std;
int n,mid,ans=9999999,d,m,p,a[500001],l,r;
struct node
{
    int r;
    long long s;
    bool operator < (node a)const
    {
        return s<a.s;
    }
}f[500001];
priority_queue <node> q;
void dp()
{
    int L=d-mid,R=d+mid;
    long long maxx=0;
    if(L<=0)
        L=1;
    for(int i=L;i<=p;i++)
    {
        while(q.top().r<i-R&&!q.empty())
            q.pop();
        q.push(f[i-L]);
        f[i].s=q.top().s+a[i];
        maxx=max(maxx,f[i].s);
    }
    if(maxx<m)
        l=mid+1;
    else
    {
        r=mid-1;
        ans=min(ans,mid);
    }
}
int main()
{
    cin>>n>>d>>m;
    for(int i=1;i<=n;i++)
    {
        cin>>p;
        cin>>a[p];
    }
    r=p-d;
    mid=(l+r)/2;
    for(int i=1;i<=p;i++)
        f[i].r=i;
    while(l<=r)
    {
        dp();
        mid=(l+r)/2;
    }
    cout<<ans;
}
