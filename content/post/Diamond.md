
---
title: Diamond
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
  caption: ''
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - Robin

tags:
  - 生信

---


> 将序列比对到nt、nr、uniprot、pfam等数据库是常有的事，blast无疑是最常用的比对软件，但是它的速度一直提不起来，非常耗费时间。估计比对等不到blast的结果了，于是想到了另一款软件Diamond

## Diamond简介

序列比对软件，能输出与BLAST类似的结果，但是速度快了数百倍。

对于长序列，支持Frameshift alignments；

占用资源更少，但只是相对blast来讲；

自定义多种输出格式

**记得引用：**

Buchfink B, Xie C, Huson DH, “Fast and sensitive protein alignment using DIAMOND”, *Nature Methods* **12**, 59-60 (2015). [doi:10.1038/nmeth.3176](https://doi.org/10.1038/nmeth.3176)

## Diamond使用

还是conda安装好diamond，说明书在此：https://github.com/bbuchfink/diamond/raw/master/diamond_manual.pdf

### 第一步: 准备数据集

先从NCBI上下载蛋白数据库。 NR库是NCBI的非冗余蛋白数据库，

```bash
wget ftp://ftp.ncbi.nlm.nih.gov/blast/db/FASTA/nr.gz
gunzip nr.gz
```

### 第二步: 建库

就两个参数，`--in nr`输入文件，`--db nr` 输出的数据库前缀

```shell
diamond makedb --in nr.faa -db nr -p 20
```

最近下载了一个nr数据库，解压完是110G，命名为nr.faa.

结果会生成一个nr.dmnd的索引文件

我用了20核构建了110G的nr数据库，用时5726.56s，作为参考

Pfam数据库7.1G，24核用时190.931s，还是非常快的

附带数据库下载地址：

**Nr**：http://mirrors.vbi.vt.edu/mirrors/ftp.ncbi.nih.gov/blast/db/FASTA/nr.gz

**Pfam**：ftp://ftp.ebi.ac.uk/pub/databases/Pfam/releases/Pfam32.0/Pfam-A.fasta.gz

**Uniprot:** [ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz](ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz)

### 第三步: 搜索

就两个子命令，blastp和blastx，前者比对蛋白，后者比对DNA序列

```shell
# 因为要将核酸序列比对到蛋白库，因此使用blastx功能
diamond blastx -d nr -q reads.fna -o nr.matches
```

默认输出格式是BLAST的tab结果，`-o`指定输出文件名

- -q/ --query输入检索序列
- --out/ -o输出文件，默认以--outfmt 6输出结果和BLAST+的--outfmt 6结果一致。

需要注意的是：

- 这个过程需要消耗大量的内存与硬盘（用于存放临时文件），如果资源不够，可以设置`-b`参数调整
- 默认的比对模式（fast模式）是针对短序列的，如果要比对的序列比较长，建议使用sensitive模式，设置`—sensitive`或者`--more-sensitive`
- 运行时间不与比对文件大小成正比，相反，文件越大（比如大于1M reads）比对速度越快
- 比对结果中的X表示Masked residues
- 默认的阈值是0.001而Blast是10，相比之下，diamond比对更严格，得到的weak hits会更少
