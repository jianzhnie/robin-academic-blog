---
title: Python 解析go的obo文件
subtitle: 

# Summary for listings and search engines
summary: 

# Link this post with a project
projects: []

# Date publiHed
date: '2022-04-13T00:00:00Z'

# Date updated
lastmod: '2022-04-13T00:00:00Z'

# Is this an unpubliHed draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - Robin

tags:
  - Python


---

### GO的obo文件解析Python代码

**介绍：**

在现在的组学研究中几乎离不开GO分析，那么GO是干什么的呢，GO的诞生主要目的是来归类统一生物学方言的（不同的生物学数据库可能会使用不同的术语），它是一个有向无环图（DAG）本体,主要形式是一term标记，每个GO term代表一种功能描述，都属于ontology. 

而GO总共分成三个ontology:molecular function, cellular component 和biological process；

在GO中GO term之间存在多种关系，常见的主要是 is_a 和 part_o f和两种关系，

- is_a：表示包含关系，如图中黑色箭头，需要强调的是“完全包含”；
- Part_of：表示一部分，如图蓝色箭头部分，简单的来说是A part_of_B意味着如果A出现，那么它就肯定是B的一部分或组成部分，但A不一定总会出现。比如叶绿体 part_of 细胞，叶绿体肯定是细胞的一部分，但有的细胞没有叶绿体。

[![attachments-2017-05-gTNS5jPL592d3f1a5bf0](https://www.shengxin.ren/image/show/attachments-2017-05-gTNS5jPL592d3f1a5bf07.)](https://www.shengxin.ren/image/show/attachments-2017-05-gTNS5jPL592d3f1a5bf07.)**使用：**

了解GO之后，怎么使用它是一个永远的话题，比如手头有一个基因序列但不知道它的功能，那么经常的做法是会进行GO注释，从 GO注释中来推断这个基因序列的功能，这篇文章主要是来分享一下对于GO的obo文件的解析的，obo文件是用来存储所有GO term关系的文件。

```python
#encoding:utf-8
'''
Created on 2017.5.29

@author: zhura
'''
class GOBase(object):
    def __init__(self,_id):
        self._id=_id
        self.alt_ids=[]
        self.name=''
        self.namespace=''
        self.parent=None
        self.level=-1 
        self.allParents=None 
        
class ObOs(object):
    def __init__(self,path):
        self.path=path
        self.map={}
        self.parseObO()
    def parseObO(self):
        f=open(self.path)
        lines=f.readlines()
        f.close()
        _goTxt=[]
        flag=False
        for line in lines:
            line=line.rstrip('\n').strip()
            if flag:
                _goTxt.append(line)
            if flag and line=='':
                self.parseGO(_goTxt)
                _goTxt=[]
                flag=False
            if line.find('[Term]')==0:
                flag=True
                
    def parseGO(self,_goText):
        _id=None
        _name=''
        _namespace=''
        _is_as=[]
        _alt_ids=[]
        for _txt in _goText:
            if _txt.find('id:')==0:
                _id=_txt[_txt.find('GO'):_txt.find('GO')+10]
            elif _txt.find('name:')==0:
                _name=_txt[5:len(_txt)].rstrip().lstrip()
            elif _txt.find('namespace:')==0:
                _namespace=_txt[10:len(_txt)].rstrip().lstrip()
            elif _txt.find('alt_id:')==0:
                _alt_ids.append(_txt[_txt.find('GO'):_txt.find('GO')+10]) 
            elif _txt.find('is_a:')==0 or _txt.find('relationship:')==0:
                _is_as.append(_txt[_txt.find('GO'):_txt.find('GO')+10]) 
        if _id:
            _go=None
            if self.map.has_key(_id):
                _go=self.map[_id]
            else:
                _go=GOBase(_id)   
            _go.name=_name
            _go.namespace=_namespace   
            _go.parent=self.parseParent(_is_as)
            _go.alt_ids=_alt_ids
            self.map[_id]=_go
            if len(_alt_ids)>0:
                for _alt in _alt_ids:
                    self.map[_alt]=_go 
                               
    def parseParent(self,is_as):
        __parent=[]
        for isa in is_as:
            if not self.map.has_key(isa):
                cGo=GOBase(isa)
                self.map[isa]=cGo
            __parent.append(isa)
        return __parent
    
    def getLevel(self,_id):
        _min=100000
        _go=self.map[_id]
        if _go.level>0:
            pass
        elif len(_go.parent)==0:
            _go.level=1
        else:
            for g in _go.parent:
                lev=self.getLevel(g)
                if _min>lev:
                    _min=lev
            _go.level=_min+1
        return _go.level
    
    def getAllParent(self,_id):
        _prs=[_id]
        _go=self.map[_id]
        if not _go.allParents is None:
            return _go.allParents
        if _go.parent is None or len(_go.parent)==0:
            _go.allParents=_prs
            return _go.allParents
        for g in _go.parent:
            ap=self.getAllParent(g)
            _prs.extend(ap)
        _go.allParents=list(set(_prs))
        return _go.allParents  

if __name__ == '__main__':
    obo='D:/bgDB/go-basic.obo.txt'
    ob=ObOs(obo)
    print ob.getAllParent('GO:0004322')
    print ob.getLevel('GO:0004322')
    print ob.getLevel('GO:0003824')
         
    
```