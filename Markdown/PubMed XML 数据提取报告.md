## 数据分析
### 整体概述

| 项目         | 详情                  |
| ---------- | ------------------- |
| **根元素**    | `PubmedArticleSet`  |
| **子元素数量**  | 30,000 个            |
| **一级元素标签** | `PubmedArticle`     |
| **数据格式**   | PubMed MEDLINE 文献记录 |

### 原始结构

整体结构如下，其中摘要信息位于 `/PubmedArticleSet/PubmedArticle/MedlineCitation/Article/Abstract/AbstractText`

```
PubmedArticleSet (根元素)
├── PubmedArticle [第1条记录]
│   ├── MedlineCitation (文献引用信息)
│   │   ├── PMID (文章唯一标识)
│   │   ├── Article (文章内容)
│   │   │   ├── ArticleTitle (文章标题)
│   │   │   ├── Abstract (摘要部分)
│   │   │   │   └── AbstractText (摘要文本)
│   │   │   ├── AuthorList (作者列表)
│   │   │   └── ... (其他文章信息)
│   │   ├── MeshHeadingList (主题词列表)
│   │   │   ├── MeshHeading (主题词1)
│   │   │   └── MeshHeading (主题词2...)
│   │   └── ... (其他元数据)
│   └── PubmedData (PubMed特定数据)
│       ├── ArticleIdList (标识符列表)
│       │   ├── ArticleId IdType="pubmed" (PubMed ID)
│       │   ├── ArticleId IdType="doi" (DOI标识)
│       │   └── ArticleId IdType="pii" (出版社标识)
│       ├── History (历史记录)
│       │   ├── PubMedPubDate PubStatus="pubmed"
│       │   ├── PubMedPubDate PubStatus="medline"
│       │   └── PubMedPubDate PubStatus="entrez"
│       ├── PublicationStatus (发布状态)
│       └── ... (其他PubMed信息)
├── PubmedArticle [第2条记录]
│   └── ... (同上结构)
└── ... (共30,000条)
```

### 目标结构

- **格式：** `ID|||摘要内容`
- **思考：** 删除所有空白部分，缩短后续检索以及保存/读取时间

## 设计思路

预计后续`xml`文件会以存放在同一个文件夹的形式存在，所以首先读取输入文件夹中所有`xml`文件后，按照上述摘要信息位置读取后，整理成`txt`格式，并按照先前的命名习惯分别村放入输出文件夹中