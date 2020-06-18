#include<bits/stdc++.h>
using namespace std;
char str[100005];
struct suffix {
    int index,first,second;
};
bool cmp(struct suffix a, struct suffix b)
{
    if(a.first == b.first) return a.second<b.second;
    else return a.first<b.first;
}
int *buildSuffixArray(char *text, int n)
{
    struct suffix suffixes[n+3];
    for(int i=0;i<n;i++)
    {
        suffixes[i].index=i;
        suffixes[i].first=text[i]-'a';
        suffixes[i].second=((i+1)<n) ? (text[i+1]-'a') : -1;
    }
    sort(suffixes,suffixes+n,cmp);
    int idx[n+3];
    for(int k=4;k<2*n;k*=2)
    {
        int rank=0;
        int prev_rank=suffixes[0].first;
        suffixes[0].first=rank; /// 0 assign to first suffix rank
        idx[suffixes[0].index]=0;
        for(int i=1;i<n;i++)
        {
            if(suffixes[i].first == prev_rank && suffixes[i].second == suffixes[i-1].second)
            {
                prev_rank=suffixes[i].first;
                suffixes[i].first=rank;
            }
            else
            {
                prev_rank=suffixes[i].first;
                suffixes[i].first= ++rank;
            }
            idx[suffixes[i].index]=i;
        }
        for(int i=0;i<n;i++)
        {
            int next_index=suffixes[i].index+k/2;
            suffixes[i].second=(next_index<n)?suffixes[idx[next_index]].first: -1;
        }
        sort(suffixes,suffixes+n,cmp);
    }
    int *suffixArr=new int[n+3];
    for(int i=0;i<n;i++) suffixArr[i]=suffixes[i].index;
    return suffixArr;
}
vector<int> kasai(string txt, int suffixArr[],int n)
{
    vector<int> lcp(n, 0);
    vector<int> invSuff(n, 0);
    for (int i=0; i < n; i++) invSuff[suffixArr[i]] = i;
    int k = 0;
    for (int i=0; i<n; i++)
    {
        if (invSuff[i] == n-1)
        {
            k = 0;
            continue;
        }
        int j = suffixArr[invSuff[i]+1];
        while(i+k<n && j+k<n && txt[i+k]==txt[j+k]) k++;
        lcp[invSuff[i]] = k;
        if (k>0) k--;
    }
    return lcp;
}
int main()
{
    int t;
    scanf("%d",&t);
    for(int cs=1;cs<=t;cs++)
    {
        int p,q,k;
        int ans=0;
        scanf("%s %d %d",str,&p,&q);
        int n=strlen(str);
        int *suffixArr=buildSuffixArray(str,n);
        vector<int>lcp=kasai(str,suffixArr,n);
        for(int i=0;i<n;i++)
        {
            k=min(n-suffixArr[i],q)-max(lcp[i],p-1);
            ans+=max(k,0);
        }
        printf("Case %d: %d\n",cs,ans);
    }
    return 0;
}
