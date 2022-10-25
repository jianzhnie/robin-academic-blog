---
title: Protein 数据库
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
  - Protein 数据库


---


### GO数据库：

官网及详细说明：[http://geneontology.org/docs/download-ontology/](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dhttp%3A%2F%2Fgeneontology.org%2Fdocs%2Fdownload-ontology%2F)
具体GO数据库的搭建参考Blast2go文章详解

### Kegg数据库：

KEGG（Kyoto Encyclopedia of Genes and Genomes）京都基因和基因组百科全书，是研究Pathway代谢通路的最主要数据库，整合了基因组信息、化学信息、系统信息及疾病和健康信息。

### UniProt 数据库：

Unified Protein Database（简称UniProt）是信息最丰富、资源最广的蛋白质序列数据库，含蛋白质序列，功能信息，研究论文索引等信息, 整合了包括EBI（ European Bioinformatics Institute），SIB（the Swiss Institute of Bioinformatics），PIR（Protein Information Resource）三大数据库的资源。

**EBI（ European Bioinformatics Institute）：**

欧洲生物信息学研究所（EMBL-EBI）是欧洲生命科学旗舰实验室EMBL的一部分。位于英国剑桥欣克斯顿的惠康基因组校内，是世界上基因组学领域最强的存在之一。

**SIB（the Swiss Institute of Bioinformatics）：**

瑞士日内瓦的SIB维护着ExPASy（专家蛋白质分析系统）服务器，这里包含有蛋白质组学工具和数据库的主要资源。

**PIR（Protein Information Resource）：**

PIR是美国国家生物医学研究基金会（NBRF）于1984年创立，旨在协助研究人员识别和解释蛋白质序列信息。

Uniprot数据库主要子数据库组成：

以上子数据库间的关系如下：Uniprot会收集EMBL，GenBank，DDBJ等公共数据库中的蛋白质序列及功能信息等原始数据，处理后存入UniParc的非冗余蛋白质序列数据库；UniPrc作为数据仓库，再分别给UniProtKB，Proteomes，UNIRef提供可靠的数据集，其中在UniProtKB数据库中Swiss-Prot是由TrEMBL经过手动注释后得到的高质量非冗余数据库，也是我们最常用的蛋白质数据库之一。

[![attachments-2022-01-QRiCJpWl61e81e76a783e.jpg](Protein%20%E5%8A%9F%E8%83%BD%E6%B3%A8%E9%87%8A.assets/attachments-2022-01-QRiCJpWl61e81e76a783e.jpg)](https://www.omicsclass.com/image/show/attachments-2022-01-QRiCJpWl61e81e76a783e.jpg)

Uniprot数据库官方链接：https://www.uniprot.org/



#### **UniProtKB/Swiss-Prot**

高质量的、手工注释的、非冗余的数据集

Swiss-Prot旨在提供与高水平注释（例如，蛋白质功能，其域结构，翻译后修饰，变体等的描述）相关的可靠蛋白质序列，最小程度的冗余和高水平与其他数据库的集成级别。注释主要来自文献中的研究成果和E-value校验过计算分析结果，有质量保证的数据才被加入该数据库 。

Swiss-Prot由Amos Bairoch博士在1986年创建，由瑞士生物信息学研究所开发，随后由欧洲生物信息学研究所的Rolf Apweiler开发。也是说EBI和SIB共同制作了Swiss-Prot和TrEMBL数据库。

Swiss-Prot条目的注释中使用了一系列序列分析工具。包括手动评估，计算机预测，并选择结果包含在相应的条目中。这些预测包括翻译后修饰，跨膜结构域和拓扑，信号肽，结构域识别和蛋白质家族分类。

来自相同基因和相同物种的序列合并到相同的数据库条目中。确定序列之间的差异包含：可变剪接，自然变异，错误的起始位点，错误的外显子边界，移码，未识别的冲突。

注释会用相关出版物通过搜索数据库（例如PubMed）进行识别。阅读每篇论文的全文，然后提取信息并将其添加到条目中。科学文献中的注释包括但不限于：

- 蛋白质和基因名称
- 功能
- 特定于酶的信息，例如催化活性，辅因子和催化残基
- 亚细胞定位
- 蛋白质相互作用
- 表达方式
- 重要域和站点的位置和角色
- 离子，底物和辅因子结合位点
- 通过自然遗传变异，RNA编辑，替代剪接，蛋白水解加工和翻译后修饰产生的蛋白质变异形式

##### **常用的操作**

![img](Protein%20%E5%8A%9F%E8%83%BD%E6%B3%A8%E9%87%8A.assets/v2-ba9fb31690e924c4bc509b198a3924cc_720w.jpg)

<1>：这里输入基因名，UniProt ID，或者感兴趣的关键字

<2>：筛选：**Reviewed**：存储在Swiss-Prot数据库中经过验证的蛋白数据，**Unreviewed**：存储在TrEMBL数据库中没有经过验证的蛋白数据

<3>：筛选某个物种，点击就好切换到该物种

<4>：通过基因名或蛋白名来筛选

<5>：依次是Unprot ID，该蛋白数据库命名，蛋白质名，基因名，物种，序列长

<6>：如果需要Blast来查看某个蛋白有哪些序列相似的蛋白序列，先选中感兴趣蛋白前的方框，点击`Blast`

<7>：如果需要多序列比对，先选中感兴趣蛋白前的方框，点击`Align`

<8>：如果要下载信息，先选中感兴趣蛋白前的方框，点击`Download`下载。这里不选择序列，默认会下载全部序列

下面以 `PO5F1_HUMAN` 为例，下载对应的fasta序列来看看：

![img](Protein%20%E5%8A%9F%E8%83%BD%E6%B3%A8%E9%87%8A.assets/v2-4740580ba34951ab5fcd5baf7147b50c_720w.jpg)

下载到的序列：

```java
  >sp|Q01860|PO5F1_HUMAN POU domain, class 5, transcription factor 1 OS=Homo sapiens OX=9606 GN=POU5F1 PE=1 SV=1
  MAGHLASDFAFSPPPGGGGDGPGGPEPGWVDPRTWLSFQGPPGGPGIGPGVGPGSEVWGI
  PPCPPPYEFCGGMAYCGPQVGVGLVPQGGLETSQPEGEAGVGVESNSDGASPEPCTVTPG
  AVKLEKEKLEQNPEESQDIKALQKELEQFAKLLKQKRITLGYTQADVGLTLGVLFGKVFS
  QTTICRFEALQLSFKNMCKLRPLLQKWVEEADNNENLQEICKAETLVQARKRKRTSIENR
  VRGNLENLFLQCPKPTLQQISHIAQQLGLEKDVVRVWFCNRRQKGKRSSSDYAQREDFEA
  AGSPFSGGPVSFPLAPGPHFGTPGYGSPHFTALYSSVPFPEGEAFPPVSVTTLGSPMHSN
```

首先看 `>` 后的注释信息

- **sp**：Swiss-Prot数据库的简称，也就是上面说的验证后的蛋白数据库

- **Q01860**：UniProt ID号

- **PO5F1_HUMAN**：是UniProt 的登录名

- **POU domain, class 5, transcription factor 1**：蛋白质名称

- **OS=Homo sapiens**：OS是Organism简称，Homo sapiens为人的拉丁文分类命名，也就是这是人的蛋白质

- **OX=9606**：Organism Taxonomy，也就是物种分类数据库Taxonomy ID

- **GN=POU5F1**：Gene name，基因名为POU5F1

- **PE=1**：Protein Existence，蛋白质可靠性，对应5个数字，数字越小越可靠：

- - 1：Experimental evidence at protein level
  - 2：Experimental evidence at tranlevel
  - 3：Protein inferred from homology
  - 4：Protein predicted
  - 5：Protein uncertain

- **SV=1**：Sequence Version，序列版本号

#### **UniProtKB/TrEMBL**

在认识到序列数据的生成速度超过了Swiss-Prot的注释能力时，为了给不在Swiss-Prot中的那些蛋白质提供自动注释，UniProt创建了TrEMBL（翻译的EMBL核苷酸序列数据库）。在三大核酸数据库（EMBL-Bank/GenBank/DDBJ）中注释的编码序列都会被自动翻译并加入该数据库中。它也有来自PDB数据库的序列，以及Ensembl、Refeq和CCDS基因预测的序列。之前提到的PIR组织制作了蛋白质序列数据库（PIR-PSD）。

#### **UniParc**

UniProt Archive（UniParc）包含来自主要公共可用蛋白质序列数据库的所有蛋白质序列的非冗余数据集。蛋白质可能存在于几个不同的来源数据库中，并且在同一数据库中存在多个副本。 为了避免冗余，UniParc仅将每个唯一序列存储一次。 相同序列被合并，无论它们来自相同还是不同物种。 每个序列都有一个稳定且唯一的标识符（UPI），从而可以从不同的来源数据库中识别相同的蛋白质。

UniParc仅包含蛋白质序列，没有注释。 UniParc条目中的数据库交叉引用允许从源数据库检索有关该蛋白质的更多信息。 当源数据库中的序列发生更改时，UniParc将跟踪这些更改，并记录所有更改的历史记录。

#### **UniRef**

UniProt Reference Clusters（UniRef）：聚类序列可显著减小数据库大小，从而加快序列搜索的速度。用于计算的蛋白质序列来自UniProtKB和部分UniParc记录的序列。UniRef100序列将相同的序列和序列片段（来自任何生物）合并到一个UniRef条目中，用于显示代表性蛋白质的序列。 使用CD-HIT算法对UniRef100序列进行聚类，并构建UniRef90和UniRef50。UniRef90和UniRef50分别代表每个簇由与最长序列分别具有至少90％或50％序列同一性的序列组成。

### COG直系同源蛋白数据库：

COG (蛋白质直系同源簇) 数据库是 NCBI 开发的用于同源蛋白注释的数据库，是将细菌、藻类和真核生物的21个完整基因组的编码蛋白，根据系统进化关系分类构建而成。通过鉴定蛋白与数据库的比对，可以很好的预测蛋白质的功能。

```text
wget -c ftp://ftp.ncbi.nih.gov/pub/COG/COG2014/data/* 
```

- fun2003-2014.tab 保存了COG的分类信息，将所有的COG的功能分为了以下26个类别，每个类别用一个字母表示

- cognames2003-2014.tab 文件保存了COG的详细信息，包括编号，对应的分类，功能描述等信息

- cog2003-2014.csv 文件保存了蛋白和COG的对应关系
- prot2003-2014.fa.gz 保存了fasta格式的蛋白序列和注释信息，直接对蛋白序列文件构建索引blast比对。示例如下

```shell
>gi|103485499|ref|YP_615060.1| chromosomal replication initiation protein [Sphingopyxis alaskensis RB2256] 
MSGDAAALWPRVAEGLRRDLGARTFDHWLKPVRFADYCALSGVVTLETASRFSANWINERFGDRLELAWRQQLPAVRSVS VRGGVAATERAATLASVPLPTFDAPAAPAANPALLGFDP
RLSFDRFVVARSNILAANAARRMAMVERPQFNPLYLCSGTG QGKTHLLQAIAQDYAAAHPTATIILMSAEKFMLEFVGAMRGGDMMAFKARLRAADLLLLDDLQFVIGKNSTQEELLHT
ID DLMTAGKRLVVTADRPPAMLDGVEARLLSRLSGGLVADIEAPEDDLRERIIRQRLAAMPMVEVPDDVIAWLVKHFTRNIR ELEGALNKLLAYAALTGARIDLMLAEDRLAENVRSA
RPRITIDEIQRAVCAHYRLDRSDMSSKRRVRAVARPRQVAMYLA KELTPRSYPEIGRRFGGRDHSTVIHAVRTVEALRVADSELDAEIAAIRRSLNS 
```

### KOG数据库：

“KOG”是Clusters of orthologous groups for eukaryotic complete genomes（真核生物蛋白相邻类的聚簇）的缩写。构成每个KOG的蛋白都是被假定为来自于一个祖先蛋白，并且因此或者是orthologs或者是paralogs。Orthologs是指来自于不同物种的由垂直家系（物种形成）进化而来的蛋白，并且典型的保留与原始蛋白有相同的功能。Paralogs是那些在一定物种中的来源于基因复制的蛋白，可能会进化出新的与原来有关的功能。数据库链接：[ftp://ftp.ncbi.nih.gov/pub/COG/KOG/kyva](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dftp%3A%2F%2Fftp.ncbi.nih.gov%2Fpub%2FCOG%2FKOG%2Fkyva)。

```text
wget -c ftp://ftp.ncbi.nih.gov/pub/COG/* 
```

### EggNOG数据库：

EggNOG数据库是直源同系蛋白分组比对（evolutionary genealogy of genes: Non-supervised Orthologous Groups）数据库，由EMBL创建并维护，是对NCBI的COG数据库进行拓展，提供了不同分类水平蛋白的直系同源分组（Orthologous Groups，OG），包括真核物种、原核物种及病毒的数据信息。它扩展了COG数据库的分类方法，采用无监督聚类算法在全基因组范围内推导基因功能，更适用于谱系特征基因的分析。
**新版本EggNOG 5.0的主页地址：**[http://eggnog5.embl.de/#/app/home](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dhttp%3A%2F%2Feggnog5.embl.de%2F%23%2Fapp%2Fhome)

新版本另一个改进是不再使用物种名称缩写，而是使用更加规范的NCBI Taxid来进行物种分类，对应的数据下载地址如下：

```text
http://eggnog5.embl.de/download/eggnog_5.0/per_tax_level/
```

下载数据：

```text
wget -c http://eggnog5.embl.de/download/eggnog_5.0/e5.proteomes.faa
wget -c http://eggnog5.embl.de/download/eggnog_5.0/e5.taxid_info.tsv 
wget -c http://eggnog5.embl.de/download/eggnog_5.0/e5.og_annotations.tsv 
```

其中e5.proteomes.faa为所有的蛋白组序列，e5.taxid_info.tsv为Taxid对应的物种名称以及完整的谱系信息，e5.og_annotations.tsv为所有的NOG group信息，其第一列为Taxid，第二列为NOG groups，第三列为COG归属，第四列为Function。
但现在我们还不能完成注释，必须需要蛋白序列id与NOG group的对应信息，这个信息在per_tax_level下不同taxonomy level的members.tsv文件中，我们将下载好的所有物种的members.tsv文件合并。
members.tsv有五列（如下所示），其中第一列为Taxid，因为我们下载的是细菌bacteria所以第一列均为2，第二列为NOG group，第三列为该NOG group所包含的蛋白序列数目，第四列为该NOG group所包含的物种数目，第五列为该NOG group所包含的蛋白序列id，第六列为该NOG group所包含的物种的Taxid。结合该members.tsv文件与前面的e5.og_annotations.tsv，就可知道比对上的蛋白序列所属的NOG group、COG categories、Function。

### Pfam数据库：

Pfam数据库是蛋白质家族的数据库，根据多序列比对结果和隐马尔可夫模型，将蛋白质分为不同的家族。网址如下： [http://pfam.xfam.org/](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dhttp%3A%2F%2Fpfam.xfam.org%2F)

1. 安装HMMer
2. 从[ftp://ftp.ebi.ac.uk/pub/databases/Pfam/releases/](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dftp%3A%2F%2Fftp.ebi.ac.uk%2Fpub%2Fdatabases%2FPfam%2Freleases%2F)下载pfam数据库Pfam-A.hmm
3. 得到 PFAM 数据库的 HMM 文件。 HMM 文件是文本文件，需要将其变成二进制格式，以加快运算速度，同时进行压缩，并建立成索引数据库。 命令：

```text
hmmpress Pfam-A.hmm  
```

1. 使用 hmmscan 进行 Pfam 注释示例：

```text
hmmscan -o out.txt --tblout out.tbl --noali -E 1e-5 Pfam-A.hmm file.fasta 
```

附 hmmscan [-options]几个主要选项含义

> -h 显示帮助信息 -o FILE 将结果输出到指定的文件中。默认是输出到标准输出。
> --tblout FILE 将蛋白质家族的结果以表格形式输出到指定的文件中。默认不输出该文件。
> --domtblout FILE 将蛋白结构域的比对结果以表格形式输出到指定的文件中。默认不输出该文件。该表格中包含query序列起始结束位点与目标序列起始结束位点的匹配信息。
> --acc 在输出结果中包含 PF 的编号，默认是蛋白质家族的名称。
> --noali 在输出结果中不包含比对信息。输出文件的大小则会更小。
> -E FLOAT default:10.0 设定 E_value 阈值，推荐设置为 1e-5 。
> -T FLOAT 设定 Score 阈值。
> --domE FLOAT default:10.0 设定 E_value 阈值。该参数和 -E 参数类似，不过是 domain 比对设定的值。

###  String数据库：

STRING数据库（[https://string-db.org/](https://link.zhihu.com/?target=https%3A//links.jianshu.com/go%3Fto%3Dhttps%3A%2F%2Fstring-db.org%2F)）是一个搜寻已知蛋白质之间和预测蛋白质之间相互作用关系的系统。这种作用关系既可以是蛋白质之间的物理作用，也可以是间接的功能相关性。它基于染色体临近、系统进化谱、基因融合和基因芯片数据等生物学信息来计算基因或者蛋白的共表达。

```text
wget -c https://stringdb-static.org/download/protein.links.v11.0.txt.gz #protein network data (scored links between proteins) 
wget -c https://stringdb-static.org/download/protein.actions.v11.0.txt.gz #interaction types for protein links  
perl data_extract_by_ids.pl -idfile ../Nr/Archaea.list -destfile protein.actions.v11.0.change.txt -out Archaea.actions.v11.0.change.txt & 
perl data_extract_by_ids.pl -idfile ../Nr/Archaea.list -destfile protein.links.v11.0.change.txt -out Archaea.links.v11.0.txt & 
perl data_extract_by_ids.pl -idfile ../Nr/Bacteria.list -destfile protein.actions.v11.0.change.txt -out Bacteria.actions.v11.0.change.txt &
perl data_extract_by_ids.pl -idfile ../Nr/Bacteria.list -destfile protein.links.v11.0.change.txt -out Bacteria.links.v11.0.txt & 
perl data_extract_by_ids.pl -idfile ../Nr/Eukaryota.list -destfile protein.actions.v11.0.change.txt -out Eukaryota.actions.v11.0.change.txt 
perl data_extract_by_ids.pl -idfile ../Nr/Eukaryota.list -destfile protein.links.v11.0.change.txt -out Eukaryota.links.v11.0.txt & 
```

**10.1. 动物转录因子数据AnimalTFDB3.0简介**

动物转录因子数据库AnimalTFDB3.0]对97个动物基因组的转录因子（Transcription Factor）和转录辅助因子（Transcription cofactor）进行了归纳整理。基于DNA结合结构域，将动物转录因子分成了73个基因家族，将转录辅助因子分成了83个基因家族。此外，动物转录因子分为六大类（Basic Domain Group、Zinc-Coordinating Group、Beta-Scaffold Factors、Helix-turn-helix、Other Alpha-Helix Group和Unclassified Structure），动物转录辅助因子也分为六大类（Co-activator/repressors、Chromatin Remodeling Factors、General Cofactors、Histone-modifying Enzymes、Cell Cycle和Other Cofactors）。
动物转录因子数据库AnimalTFDB3.0提供了[网页工具] 进行转录因子分析。该网页工具一次仅支持上传不超过1000条蛋白序列，不利于动物全基因组的转录因子分析。以下讲解下载AnimalTFDB3.0数据库FASTA文件，并自行编写程序进行转录因子和转录辅助因子注释。

1. 下载14个hmm文件并合并

```text
wget -c http://bioinfo.life.hust.edu.cn/static/AnimalTFDB3/download/hmm/* 
```

1. 下载97个物种的蛋白序列、转录因子、转录辅助因子、转录辅助因子序列

```text
wget http://bioinfo.life.hust.edu.cn/static/AnimalTFDB3/download/Ailuropoda_melanoleuca_TF_protein.fa 
wget http://bioinfo.life.hust.edu.cn/static/AnimalTFDB3/download/Ailuropoda_melanoleuca_TF 
wget http://bioinfo.life.hust.edu.cn/static/AnimalTFDB3/download/Ailuropoda_melanoleuca_TF_cofactors 
wget http://bioinfo.life.hust.edu.cn/static/AnimalTFDB3/download/Ailuropoda_melanoleuca_Cof_protein.fa  
```

**参考：**[http://www.chenlianfu.com/?p=2759]

**10.2. 植物转录因子数据AnimalTFDB3.0简介**
PlnTFDB [http://plntfdb.bio.uni-potsdam.de/v3.0/] 是一个植物转录因子数据库，该数据库收录了大部分植物模式物种，包括拟南芥，水稻等20个物种的84个转录因子家族，包含28193 protein models, 26184 distinct protein sequences。它支持在线blast进行比对，也可以将数据下载后进行本地blast。
**分析工具：iTAK** :[http://itak.feilab.net/cgi-bin/itak/index.cgi]

```text
wget ftp://itak.feilab.net/pub/program/itak/old/iTAK-1.7.tar.gz 
```

软件内部内置了PlantTFDB的数据库数据，可以直接用于预测植物转录因子，使用方法非常简单，只需要输入您需要鉴定的蛋白序列fasta格式即可。

其中classification.txt就是我们得到的植物转录因子预测结果：

1. alignment.txt：输入序列和数据库比对结果
2. classification.txt：输入序列鉴定结果，ID 1：输入序列，ID 2：Family 鉴定的家族名称
3. Type Family 类型，包含 TF，TR，PK TF: transcription factors TR: transcription regulator PK: protein kinases.
4. Sequence.fasta：输入序列比对上家族的氨基酸序列

**10.3. 真菌转录因子数据库Fungal TFDB简介**
真菌转录因子数据库Fungal TFDB1.2([http://ftfd.snu.ac.kr/index.php?a=view])
对249个真菌（包含6个卵菌）基因组的转录因子和228个非真菌系的转录因子进行了归纳整理。基于转录因子家族分类，共获得61个家族，包含18563个真菌转录因子序列。