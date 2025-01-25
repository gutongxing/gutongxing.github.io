---
layout: post
title: "【题解】LOJ6565最假女选手"
date:   2025-1-25
tags: [题解][线段树][势能线段树][吉司机线段树][模板]
comments: true
author: gutongxing
---

[LibreOJ-6565 最假女选手](https://vjudge.net/problem/LibreOJ-6565)

吉司机线段树模板题，注重复习。

```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long
namespace gtx{
//	Fast IO
	char buf[1<<23],*p1=buf,*p2=buf,obuf[1<<23],*O=obuf;
#define getchar() (p1==p2&&(p2=(p1=buf)+fread(buf,1,1<<21,stdin),p1==p2)?EOF:*p1++)
	inline long long rd() {
		int x=0,f=1;char ch=getchar();
		while(!isdigit(ch)){if(ch=='-') f=-1;ch=getchar();}
		while(isdigit(ch)) x=x*10+(ch^48),ch=getchar();
		return x*f;
	}
	inline void read(int &x){
		x = rd();
	}
	inline void read(char &x){do{x=getchar();}while(x==' '||x=='\n'||x=='\r');}
	inline void write(char x){putchar(x);}
	inline void write(int x){
		if(x<0) putchar('-'),x=-x;int st[200]={0},tot=0;
		do st[++tot]=x%10,x/=10; while(x);
		while(tot){putchar(st[tot--]+'0');}
	}
	inline void write(int x,char y){write(x);write(y);}
#ifndef int
	inline void read(long long &x){
		x = rd();
	}
	inline void write(long long x){
		if(x<0) putchar('-'),x=-x;int st[200]={0},tot=0;
		do st[++tot]=x%10,x/=10; while(x);
		while(tot){putchar(st[tot--]+'0');}
	}
	inline void write(long long x,char y){write(x);write(y);}
#endif
	const int MAXN = 1e6+10;
	const int INF = 0x3f3f3f3f3f3f3f3f;
	struct segmentree{
		int l,r;
		int maxn;
		int totmaxn;
		int maxn2;
		int totmaxn2;
		int minn;
		int totminn;
		int minn2;
		int totminn2;
		int sum;
		int lazymaxn;
		int lazyminn;
		int lazymaxn2;
		int lazyminn2;
		int addminn;
		int addmaxn;
		int lazyadd;
	}tree[MAXN<<2];
	inline void maketagadd(int k,int x){
		tree[k].maxn += x;
		tree[k].minn += x;
		tree[k].maxn2 += x;
		tree[k].minn2 += x;
		tree[k].sum += x*(tree[k].r-tree[k].l+1);
		tree[k].lazyadd+=x;
	}
	inline void maketagaddmaxn(int k,int x,int y){
		tree[k].maxn += x;
		tree[k].sum += y*tree[k].totmaxn;
		tree[k].lazymaxn += x;
		tree[k].addmaxn += y;
	}
	inline void maketagaddminn(int k,int x,int y){
		tree[k].minn += x;
		tree[k].sum += y*tree[k].totminn;
		tree[k].lazyminn += x;
		tree[k].addminn += y;
	}
	inline void maketagaddmaxn2(int k,int x){
		tree[k].maxn2 += x;
		tree[k].lazymaxn2 += x;
	}
	inline void maketagaddminn2(int k,int x){
		tree[k].minn2 += x;
		tree[k].lazyminn2 += x;
	}
	inline void pushdown(int k){
		if(tree[k].lazyadd){
			maketagadd(k*2,tree[k].lazyadd);
			maketagadd(k*2+1,tree[k].lazyadd);
			tree[k].lazyadd = 0;
		}
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2].maxn)		maketagaddmaxn	(k*2,	tree[k].lazymaxn,tree[k].addmaxn);
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2+1].maxn)		maketagaddmaxn	(k*2+1,	tree[k].lazymaxn,tree[k].addmaxn);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2].minn)		maketagaddminn	(k*2,	tree[k].lazyminn,tree[k].addminn);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2+1].minn)		maketagaddminn	(k*2+1,	tree[k].lazyminn,tree[k].addminn);
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2].minn)		maketagaddminn	(k*2,	tree[k].lazymaxn,0);
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2+1].minn)		maketagaddminn	(k*2+1,	tree[k].lazymaxn,0);
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2].minn2)		maketagaddminn2	(k*2,	tree[k].lazymaxn);
		if(tree[k].maxn-tree[k].lazymaxn==tree[k*2+1].minn2)	maketagaddminn2	(k*2+1,	tree[k].lazymaxn);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2].maxn)		maketagaddmaxn	(k*2,	tree[k].lazyminn,0);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2+1].maxn)		maketagaddmaxn	(k*2+1,	tree[k].lazyminn,0);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2].maxn2)		maketagaddmaxn2	(k*2,	tree[k].lazyminn);
		if(tree[k].minn-tree[k].lazyminn==tree[k*2+1].maxn2)	maketagaddmaxn2	(k*2+1,	tree[k].lazyminn);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2].minn)		maketagaddminn	(k*2,	tree[k].lazyminn2,0);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2].minn2)	maketagaddminn2	(k*2,	tree[k].lazyminn2);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2+1].minn)	maketagaddminn	(k*2+1,	tree[k].lazyminn2,0);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2+1].minn2)	maketagaddminn2	(k*2+1,	tree[k].lazyminn2);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2].maxn)		maketagaddmaxn	(k*2,	tree[k].lazyminn2,0);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2].maxn2)	maketagaddmaxn2	(k*2,	tree[k].lazyminn2);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2+1].maxn)	maketagaddmaxn	(k*2+1,	tree[k].lazyminn2,0);
		if(tree[k].minn2-tree[k].lazyminn2==tree[k*2+1].maxn2)	maketagaddmaxn2	(k*2+1,	tree[k].lazyminn2);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2].maxn)		maketagaddmaxn	(k*2,	tree[k].lazymaxn2,0);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2].maxn2)	maketagaddmaxn2	(k*2,	tree[k].lazymaxn2);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2+1].maxn)	maketagaddmaxn	(k*2+1,	tree[k].lazymaxn2,0);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2+1].maxn2)	maketagaddmaxn2	(k*2+1,	tree[k].lazymaxn2);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2].minn)		maketagaddminn	(k*2,	tree[k].lazymaxn2,0);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2].minn2)	maketagaddminn2	(k*2,	tree[k].lazymaxn2);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2+1].minn)	maketagaddminn	(k*2+1,	tree[k].lazymaxn2,0);
		if(tree[k].maxn2-tree[k].lazymaxn2==tree[k*2+1].minn2)	maketagaddminn2	(k*2+1,	tree[k].lazymaxn2);
		tree[k].lazymaxn = tree[k].addmaxn = tree[k].lazyminn = tree[k].addminn = tree[k].lazymaxn2 = tree[k].lazyminn2 = 0;
	}
	inline void GXmax(int k,int a,int b){
		if(a>tree[k].maxn){
			tree[k].maxn2 = tree[k].maxn;
			tree[k].totmaxn2 = tree[k].totmaxn;
			tree[k].maxn = a;
			tree[k].totmaxn = b;
		}else if(a==tree[k].maxn) tree[k].totmaxn+=b;
		else if(a>tree[k].maxn2){
			tree[k].maxn2 = a;
			tree[k].totmaxn2 = b;
		}else if(a==tree[k].maxn2) tree[k].totmaxn2+=b;
	}
	inline void GXmin(int k,int a,int b){
		if(a<tree[k].minn){
			tree[k].minn2 = tree[k].minn;
			tree[k].totminn2 = tree[k].totminn;
			tree[k].minn = a;
			tree[k].totminn = b;
		}else if(a==tree[k].minn) tree[k].totminn+=b;
		else if(a<tree[k].minn2){
			tree[k].minn2 = a;
			tree[k].totminn2 = b;
		}else if(a==tree[k].minn2) tree[k].totminn2+=b;
	}
	inline void pushup(int k){
		tree[k].maxn = -INF;
		tree[k].totmaxn = 0;
		tree[k].maxn2 = -INF;
		tree[k].totmaxn2 = 0;
		tree[k].minn = INF;
		tree[k].totminn = 0;
		tree[k].minn2 = INF;
		tree[k].totminn2 = 0;
		tree[k].sum = tree[k*2].sum+tree[k*2+1].sum;
		GXmax(k,tree[k*2].maxn,tree[k*2].totmaxn);
		GXmax(k,tree[k*2].maxn2,tree[k*2].totmaxn2);
		GXmax(k,tree[k*2+1].maxn,tree[k*2+1].totmaxn);
		GXmax(k,tree[k*2+1].maxn2,tree[k*2+1].totmaxn2);
		GXmin(k,tree[k*2].minn,tree[k*2].totminn);
		GXmin(k,tree[k*2].minn2,tree[k*2].totminn2);
		GXmin(k,tree[k*2+1].minn,tree[k*2+1].totminn);
		GXmin(k,tree[k*2+1].minn2,tree[k*2+1].totminn2);
	}
	int a[MAXN];
	inline void build(int k,int l,int r){
		tree[k].l = l;
		tree[k].r = r;
		tree[k].maxn = -INF;
		tree[k].totmaxn = 0;
		tree[k].maxn2 = -INF;
		tree[k].totmaxn2 = 0;
		tree[k].minn = INF;
		tree[k].totminn = 0;
		tree[k].minn2 = INF;
		tree[k].totminn2 = 0;
		if(l==r){
			GXmax(k,a[l],1);
			GXmin(k,a[l],1);
			tree[k].sum = a[l];
			return;
		}
		int mid = (l+r)>>1;
		build(k*2,l,mid);
		build(k*2+1,mid+1,r);
		pushup(k);
	}
	inline void modify_minn(int k,int l,int r,int x){
		if(tree[k].l>r||tree[k].r<l) return;
		if(tree[k].l>=l&&tree[k].r<=r){
			if(x>=tree[k].maxn){
				return;
			}
			if(x>tree[k].maxn2){
				if(tree[k].minn2==tree[k].maxn){
					maketagaddminn2(k,x-tree[k].minn2);
					maketagaddmaxn(k,x-tree[k].maxn,x-tree[k].maxn);
				}else if(tree[k].minn==tree[k].maxn){
					maketagaddminn(k,x-tree[k].minn,0);
					maketagaddmaxn(k,x-tree[k].maxn,x-tree[k].maxn);
				}else{
					maketagaddmaxn(k,x-tree[k].maxn,x-tree[k].maxn);
				}
				return;
			}
		}
		pushdown(k);
		modify_minn(k*2,l,r,x);
		modify_minn(k*2+1,l,r,x);
		pushup(k);
		return;
	}
	inline void modify_maxn(int k,int l,int r,int x){
		if(tree[k].l>r||tree[k].r<l) return;
		if(tree[k].l>=l&&tree[k].r<=r){
			if(x<=tree[k].minn){
				return;
			}
			if(x<tree[k].minn2){
				if(tree[k].maxn2==tree[k].minn){
					maketagaddmaxn2(k,x-tree[k].maxn2);
					maketagaddminn(k,x-tree[k].minn,x-tree[k].minn);
				}else if(tree[k].maxn==tree[k].minn){
 					maketagaddmaxn(k,x-tree[k].maxn,0);
					maketagaddminn(k,x-tree[k].minn,x-tree[k].minn);
				}else{
					maketagaddminn(k,x-tree[k].minn,x-tree[k].minn);
				}
				return;
			}
		}
		pushdown(k);
		modify_maxn(k*2,l,r,x);
		modify_maxn(k*2+1,l,r,x);
		pushup(k);
		return;
	}
	inline void modify_add(int k,int l,int r,int x){
		if(tree[k].l>r||tree[k].r<l) return;
		if(tree[k].l>=l&&tree[k].r<=r){
			maketagadd(k,x);
			return;
		}
		pushdown(k);
		modify_add(k*2,l,r,x);
		modify_add(k*2+1,l,r,x);
		pushup(k);
	}
	inline int askmax(int k,int l,int r){
		if(tree[k].l>r||tree[k].r<l) return -INF;
		if(tree[k].l>=l&&tree[k].r<=r) return tree[k].maxn;
		pushdown(k);
		return max(askmax(k*2,l,r),askmax(k*2+1,l,r));
	}
	inline int askmin(int k,int l,int r){
		if(tree[k].l>r||tree[k].r<l) return INF;
		if(tree[k].l>=l&&tree[k].r<=r) return tree[k].minn;
		pushdown(k);
		return min(askmin(k*2,l,r),askmin(k*2+1,l,r));
	}
	inline int asksum(int k,int l,int r){
		if(tree[k].l>r||tree[k].r<l) return 0;
		if(tree[k].l>=l&&tree[k].r<=r) return tree[k].sum;
		pushdown(k);
		return (asksum(k*2,l,r)+asksum(k*2+1,l,r));
	}
	int n,m;
	signed main(){
		read(n);
		for(int i = 1;i<=n;i++){
			read(a[i]);
		}
		build(1,1,n);
		read(m);
		while(m--){
			int id,x,y,z;
			read(id);read(x);read(y);
			if(id==1){
				read(z);
				modify_add(1,x,y,z);
			}else if(id==2){
				read(z);
				modify_maxn(1,x,y,z);
			}else if(id==3){
				read(z);
				modify_minn(1,x,y,z);
			}else if(id==4){
				write(asksum(1,x,y),endl);
			}else if(id==5){
				write(askmax(1,x,y),endl);
			}else{
				write(askmin(1,x,y),endl);
			}
		}
		return 0;
	}
}
signed main(){
//	freopen("1.txt","r",stdin);
//	freopen("2.txt","w",stdout);
//	ios::sync_with_stdio(0);cin.tie(0);cout.tie(0);
	int T = 1;
//	gtx::read(T);
	while(T--) gtx::main();
	return 0;
}
```
