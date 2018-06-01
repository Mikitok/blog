title: Trie Tree（字典树）
date: 2017-03-27 21:13:04
tags:
  - C++
  - 算法
  - hihoCoder
categories:
  - hihoCoder
---

&emsp;&emsp;之前有看到过这个概念，但是没有认真了解过，这次刷hihoCoder的题目看到了这个。
&emsp;&emsp;Trie Tree，也就是常说的字典树。它利用了空间换时间的思想，用字符串的公共前缀来减少查询时间，最大限度地减少无谓的字符串比较，提高查询效率。它是一种多叉树的结构，对它来说，每一个结点由值域和链域两部分组成，值域保存这个结点对应的字符数和以到这个结点的所有的字符组成的字符串为前缀的字符串个数，链域则是指向该结点后继的结点。树的形式极大地减少了比较的次数，便于查找。
&emsp;&emsp;对于一个结点来说，链域的存储方式有很多种，我想到了以下几种：

> 1. 增加一个指针采用，表示该结点的兄弟结点，即“左儿子右兄弟”的形式。（这也是我一开始采用的方法，但是后来逻辑没有理清楚，放弃了）
> 2. 增加一个指针数组，数组不同位置对应不同的字符。（这是很常用的一种方法，但是我一开始没有看到字符的类别数，也没有采用，但是比第一种简单很多）
> 3. 增加一个表示指针的map，不同的键值对应不同的结点。（这也是我最后采用的一种方法，用起来也不复杂）

&emsp;&emsp;下面的代码是实现hihoCoder的[#1014 : Trie树][1]，所以说对于Trie Tree的功能我只实现了插入和查询的部分，具体见下面代码（已AC）。

  [1]: http://hihocoder.com/problemset/problem/1014

```C++
    #include <iostream>
    #include <string>
    #include <map>
    using namespace std;
    
    class trieNode {
    private:
    	int ccount;
    	char letter;
    public:
    	map <char, trieNode*> nodemap;
    	trieNode() { ccount = 0; }
    	trieNode(char c);
    	void inccount() { ccount++; }
    	int getcount() { return ccount; }
    };
    
    trieNode::trieNode(char c)
    {
    	ccount = 1;
    	letter = c;
    }
    
    class trieTree {
    private:
    	trieNode* head;
    
    public:
    	trieTree() { head = new trieNode(); }
    	void trieTreeInsert(string s);
    	int countPrefix(string s);
    };
    
    void trieTree::trieTreeInsert(string s)
    {
    	trieNode *p, *q;
    	int len = s.length();
    	int i;
    	if (len > 0) {
    		p = head;
    		for (i = 0; i < len; i++) {
    			if (p->nodemap.find(s[i]) == p->nodemap.end()) {
    				p->inccount();
    				break;
    			}
    			else {
    				p->inccount();
    				p = p->nodemap[s[i]];
    			}
    		}
    		if (i == len) {
    			p->inccount();
    		}
    		for (; i < len; i++) {
    			q = new trieNode(s[i]);
    			p->nodemap.insert(make_pair(s[i], q));
    			p = q;
    		}
    	}
    }
    
    int trieTree::countPrefix(string s) {
    	int len = s.length();
    	int count = 0;
    	trieNode *p = head;
    	bool f = true;
    	for (int i = 0; i < len; i++) {
    		if (p->nodemap.find(s[i]) == p->nodemap.end()) {
    			f = false;
    			break;
    		}
    		else {
    			p = p->nodemap[s[i]];
    		}
    	}
    	if (f) {
    		count = p->getcount();
    	}
    	return count;
    }
    
    int main()
    {
    	int n, m, count;
    	string s;
    	trieTree tr;
    
    	cin >> n;
    	for (int i = 0; i < n; i++) {
    		cin >> s;
    		tr.trieTreeInsert(s);
    	}
    
    	cin >> m;
    	for (int i = 0; i   < m; i++) {
    		cin >> s;
    		count=tr.countPrefix(s);
    		cout << count << endl;
    	}
    	return 0;
    }
```
