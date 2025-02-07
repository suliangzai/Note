# Week 1

# Week 2

# Week 3

## Term Weighting Schemes 术语加权方案

- Term Weighting Schemes involves calculating and assigning a numerical value to each term, aiming to assess its significance in differentiating a specific document from the rest.
- 术语加权方案包括计算和分配每个术语的数值，目的是评估其在区分特定文档与其他文档方面的重要性。

▪ Term Weighting seeks to represent the importance of a chosen query term in the corpus.术语加权旨在表示所选查询术语在语料库中的重要性。

▪ Common term weighting schemes include 常见的术语加权方案包括

- TF-IDF
- BM25

### TF-IDF

Term Frequency-Inverse Document Frequency (TF- IDF)术语频率-反向文档频率

Term Frequency refers to how often a term appears across a particular document.术语频率是指术语在特定文档中出现的频率。

Inverse Document Frequency refers to the relative rarity of a term in the collection of documents.反向文档频率指的是术语在文档集合中的相对稀有程度。

▪ The final TF-IDF value is obtained by multiplying these values together. 将这些值相乘，就得到了最终的 TF-IDF 值。

▪ The higher the TF-IDF score, the more important or relevant the term is; as a term gets less relevant, its TF-IDF score will approach 0. TF-IDF 分数越高，说明术语越重要或越相关；随着术语的相关性降低，其 TF-IDF 分数将趋近于 0。

Term Frequency can be calculated in multiple ways:

- The raw count of how often a term appears in the document. 术语在文档中出现频率的原始计数。$tf_{t,d}$
- Term frequency adjusted for document length.根据文件长度调整的术语频率。$\frac{tf_{t,d}}{n.words}$
- Logarithmically Scaled.对数缩放。$1+log(tf_{t,d})$
- Boolean Frequency (1 if term appears in document, 0 if term does not appear in document).布尔频率（1 表示术语出现在文档中，0 表示术语未出现在文档中）。

Inverse document frequency can be defined as:

\[
    idf(t,D) = log(\frac{N}{count(d \in D:t \in d)})
\]

- Where N is the total number of documents (d) in the corpus (D).其中，N 是语料库（D）中的文档总数（d）。
- The denominator is the number of documents where the term t appears in.分母是术语 t 出现的文档数。
- If a term does not appear in the corpus, a divide by zero error may occur. This can be avoided using the following equation:如果一个术语没有出现在语料库中，可能会出现除以零的错误。使用下面的公式可以避免这种情况：

\[
    idf(t,D) = log(\frac{1+N}{1+count(d \in D:t \in d)})+1
\]

TF-IDF is simply defined as:

\[
    tf(t,D) · idf(t,D) 
\]

- The higher the TF-IDF score the more important or relevant the term is; as a term gets less relevant, its TF-IDF score will approach 0.TF-IDF 分数越高，表示该词越重要或越相关；随着词的相关性降低，其 TF-IDF 分数将趋近于 0。
- TF-IDF vectorization involves calculating the TF-IDF score for every word in your corpus relative to that document and then putting that information into a vector.TF-IDF 向量化涉及计算语料库中每个词相对于该文档的 TF-IDF 分数，然后将该信息放入一个向量中。
- Each document in the corpus would have its own vector, and the vector would have a TF-IDF score for every single word in the entire collection of documents.语料库中的每个文档都将有自己的向量，而向量中将包含整个文档集合中每个单词的 TF-IDF 分数。
- The similarity between the documents can be derived from the cosine similarity between the two vectors.文档之间的相似性可以通过两个向量之间的余弦相似性得出。

TF- IDF vectorization with SKLearn:

![alt text](image.png)

Words that appear more across each document have a higher TF-IDF score, while words that are unique to each document have a TF- IDF score of 0.在每篇文档中出现次数较多的词的 TF-IDF 分数较高，而每篇文档中独有的词的 TF-IDF 分数为 0。

![alt text](image-1.png)

Advantages：

▪ Efficiency:
It is computationally efficient to calculate TF-IDF scores for documents, especially compared to more complex natural language processing techniques.为文档计算 TF-IDF 分数的计算效率很高，尤其是与更复杂的自然语言处理技术相比。
▪ Language Agnostic:
TF-IDF can be applied to documents in any language, making it versatile for multilingual text analysis.TF-IDF 可应用于任何语言的文档，因此可用于多语言文本分析。
▪ No Supervised Training:
TF-IDF doesn't require a training phase with labeled data, making it readily applicable to various tasks without the need for extensive training data.TF-IDF 不需要标注数据的训练阶段，因此无需大量训练数据就能轻松完成各种任务。

Limitations：

▪ No Semantics:
TF-IDF treats words as independent units and doesn't consider the semantics or relationships between words.TF-IDF 将单词视为独立单元，不考虑单词之间的语义或关系。
▪ Term Frequency Bias:
Terms that appear more frequently tend to receive higher weights, which can lead to overemphasis on common words that are not very informative.出现频率较高的词往往会获得较高的权重，这可能会导致过分强调信息量不大的普通词。
▪ Vocabulary Size:
The size of the vocabulary (unique terms across the corpus) can become a computational challenge for large datasets, and rare terms might not receive accurate IDF values.对于大型数据集来说，词汇量（整个语料库中的唯一术语）的大小可能会成为计算上的一个挑战，罕见术语可能无法获得准确的 IDF 值。

### BM25

Best Match 25 (BM25)

BM25 is an algorithm that considers both term frequency (TF) and document length normalization to determine the relevance of a document to a given query.BM25 是一种同时考虑术语频率 (TF) 和文档长度归一化的算法，用于确定文档与给定查询的相关性。
▪ It follows the probabilistic retrieval framework, which assumes that relevant and non-relevant documents follow different statistical distributions.它遵循概率检索框架，该框架假定相关文档和非相关文档遵循不同的统计分布。

\[
    BM25(D,Q)=\sum_{i=1}^nIDF(q_i)\cdot \frac{TF(q_i,D)\cdot(k_1+1)}{TF(q_i,D)+k_1\cdot (1-b+b\cdot \frac{|D|}{avgdl})}
\]

Where:
▪ IDF(q) represents the inverse document frequency of the query term q. IDF(q) 表示查询词 q 的反文档频率。
▪ TF(q, D) denotes the modified term frequency of term q in document D.TF(q, D) 表示术语 q 在文档 D 中的修正词频。
▪ |D| represents the length of document D. |D| 表示文档 D 的长度。
▪ avgdl is the average document length in the corpus.avgdl 是语料库中文档的平均长度。
▪ Parameters k1 and b are tunable constants that control the impact of term frequency saturation and document length normalisation, respectively.参数 k1 和 b 是可调常数，分别控制词频饱和和文档长度归一化的影响。

![alt text](image-2.png)

请注意 BM25 是如何根据文件长度进行调整的。虽然句子 2 和 3 都包含 “will ”一词，但在较短的文档中，BM25 算法对该词赋予了更高的权重。

Advantages
▪ Information Retrieval:
BM25 is known to be effective in information retrieval tasks. It often outperforms traditional TF-IDF weighting, especially when dealing with large and diverse text corpora.众所周知，BM25 在信息检索任务中非常有效。它的性能往往优于传统的 TF-IDF 加权法，尤其是在处理大型和多样化的文本语料库时。
▪ Balanced Term Frequency:
BM25 addresses the issue of term frequency saturation by introducing the parameter 'k.' This makes it more robust in handling documents with varying term frequencies, preventing common terms from dominating the score.BM25 通过引入参数 “k ”来解决词频饱和的问题。这使得它在处理具有不同词频的文档时更加稳健，从而避免了常见词在得分中占主导地位。

Limitations
▪ No Semantics:
Similarly to TF-IDF, BM25 does not take into account the semantics of a document.与 TF-IDF 类似，BM25 也不考虑文档的语义。
▪ Sparse Data:
BM25 may not perform as well when dealing with very sparse data or extremely short documents because it relies on term frequencies and document lengths to calculate scores. 当处理非常稀疏的数据或极短的文档时，BM25 的表现可能会不尽如人意，因为它依赖于术语频率和文档长度来计算分数。

## Topic Modeling 主题建模 

Topic Modeling is an unsupervised method for document classification, aiming to discover and extract hidden thematic structures within large collections of text data.主题建模是一种用于文档分类的无监督方法，旨在发现和提取大量文本数据集合中隐藏的主题结构。

▪ This is achieved by analysing word co-occurrence patterns within unstructured text data.这是通过分析非结构化文本数据中的词语共现模式来实现的。
▪ The hidden thematic structures can then be used to classify and summarise the available data.隐藏的主题结构可用于对现有数据进行分类和总结。
▪ Common Topic modelling techniques include:常见的主题建模技术包括:

- LDA
- LSA
- NMF

### LDA

Latent Dirichlet Allocation (LDA)潜在德里希勒分配

LDA aims to find the representative words for a topic and classify a document based on the occurrence of these wordsLDA 的目的是找到一个主题的代表词，并根据这些词的出现情况对文档进行分类

▪ LDA consists of 2 parts:
- Words belonging to a document.属于文档的词语。
- Words belonging to a topic.属于主题的词语。
▪ LDA works off a Bag-Of-Words approach – the order and semantics of a word is not consideredLDA 采用 “词袋 ”方法工作--不考虑词的顺序和语义
▪ LDA requires the user to set a predetermined number of topics, k.LDA 要求用户设置预定的主题数 k。

Algorithm:

Go through each document in the corpus and randomly assign each word in the document to one of k topics.浏览语料库中的每份文档，并将文档中的每个词随机分配给 k 个主题之一。

 For each document d, go through each word w and find:

▪ 𝒑(𝒕𝒐𝒑𝒊𝒄 𝒕|𝒅𝒐𝒄𝒖𝒎𝒆𝒏𝒕 𝒅): The proportion of words in document d that are assigned to topic t. Captures how many words belong to topic t in document d.文档 d 中分配给主题 t 的单词比例，反映文档 d 中属于主题 t 的单词数量。

▪ 𝒑(𝒘𝒐𝒓𝒅 𝒘|𝒕𝒐𝒑𝒊𝒄 𝒕): The proportion of assignments to topic t from all documents that come from word w. Captures how many documents are in topic t due to document w.来自单词 w 的所有文档中分配给主题 t 的比例，反映了有多少文档是由于文档 w 而进入主题 t 的。

▪ Update the probability of word w belonging to topic t using:

𝒑(𝒘𝒐𝒓𝒅 𝒘 𝒃𝒆𝒍𝒐𝒏𝒈𝒔 𝒕𝒐 𝒕𝒐𝒑𝒊𝒄 𝒕) = 𝒑 (𝒕𝒐𝒑𝒊𝒄 𝒕|𝒅𝒐𝒄𝒖𝒎𝒆𝒏𝒕 𝒅)∙𝒑(𝒘𝒐𝒓𝒅 𝒘|𝒕𝒐𝒑𝒊𝒄 𝒕)

LDA in gensim:
▪ For this demonstration, we will use a compilation of COVID tweets found at:在本演示中，我们将使用 COVID 推文汇编，网址为:
https://www.kaggle.com/datasets/datatattle/covid-19-nlp-text-classification
▪ We first filter out only the tweets:我们首先只筛选出推文：

![alt text](image-3.png)

To make the data easier to process, we remove all punctuation and convert all words to lowercase.为了便于处理数据，我们删除了所有标点符号，并将所有单词转换为小写。

![alt text](image-4.png)

As LDA is a BOW model, we want to remove stop words that don’t carry much semantic meaning.由于 LDA 是一种 BOW 模型，我们希望删除那些没有太多语义的停滞词。

![alt text](image-5.png)

注意：“https ”和 “tco ”是推文中共享超链接的一部分。在本示例中，它们将被删除。

With k =7, we can generate the LDA scores for each word in a tweet and classify them into a topic.在 k =7 的情况下，我们可以为推文中的每个单词生成 LDA 分数，并将其归入一个主题。

![alt text](image-6.png)

Create a dictionary of all words in the corpus 为语料库中的所有单词创建词典

![alt text](image-7.png)

Visualisation:

![alt text](image-8.png)

Advantages
▪ Dimensionality Reduction:
LDA reduces the dimensionality of the data by representing documents as mixtures of topics. This simplifies data representation.LDA 将文档表示为主题的混合物，从而降低了数据的维度。这简化了数据表示。
▪ Interpretability: 
The topics generated by LDA are typically represented as lists of words, making them interpretable.LDA 生成的主题通常以单词列表的形式表示，因此具有可解释性。

Limitations
▪ No Semantics:
LDA treats words independently of their context in a document. Hence, the semantics of a word are not captured with LDA.LDA 处理单词时与单词在文档中的上下文无关。因此，LDA 无法捕捉单词的语义。
▪ Preprocessing Sensitivity:
LDA is highly sensitive to the preprocessing used on data, such as stop word removal and stemming.LDA 对数据的预处理非常敏感，如删除停滞词和词干。

### LSA

Latent Semantic Analysis (LSA):潜在语义分析

LSA aims to uncover the underlying semantic structure of text data and transform it into a lower-dimensional space.LSA 旨在发掘文本数据的潜在语义结构，并将其转换为低维空间。

▪ LSA works by generating a document-term matrix.LSA 的工作原理是生成一个文档-词矩阵。
▪ The matrix is typically populated with the TF-IDF scores for each word.该矩阵通常包含每个词的 TF-IDF 分数。
▪ The matrix is then decomposed (typically with SVD) into sub-matrixes.然后将矩阵分解（通常使用 SVD）为子矩阵。

![alt text](image-9.png)

Steps

Generate a document-term matrix of shape mxn:生成 mxn 形的文档词矩阵：
The column entries can be filled by a raw count of the number of times a word appears in the document, but the TF-IDF score is usually used as it gives a better representation of the significance of the word.列项可由文档中单词出现次数的原始计数填充，但通常使用 TF-IDF 分数，因为它能更好地反映单词的重要性。

![alt text](image-10.png)

By applying SVD (explained in detail later), break the matrix down into 通过应用 SVD（稍后将详细解释），将矩阵分解为

▪ Document-Topic Matrix 𝑼𝒌文档-主题矩阵 𝑼𝒌
- Document vectors expressed in terms of topics用主题表示的文档向量

▪ Term-Topic Matrix 𝑽𝒌𝑻术语-主题矩阵 𝑽𝒌𝑻
- Term vectors in terms of topics用主题表示的术语向量

![alt text](image-11.png)

LSA in gensim

Using the same COVID dataset
▪ Stem words to reduce noise删除词干以减少噪音

![alt text](image-12.png)

![alt text](image-13.png)

We can then build the LSA model and extract the top 10 relevant keywords.然后，我们就可以建立 LSA 模型，并提取前 10 个相关关键词。

![alt text](image-14.png)

Advantages
▪ Dimensionality Reduction:
LSA reduces the dimensionality of the data by representing documents as mixtures of topics. This simplifies data representation.LSA 将文档表示为主题的混合物，从而降低了数据的维度。这简化了数据表示。
▪ Semantic Understanding:
LSA captures the underlying semantic structure of text, allowing it to identify and measure semantic similarities between words and documents, even when they don't share exact word overlap.LSA 可捕捉文本的基本语义结构，从而能够识别和测量单词与文档之间的语义相似性，即使它们没有完全的单词重叠。

Limitations
▪ Lack of Interpretability:
The reduced semantic space created by LSA lacks human interpretability. While it captures semantic relationships, it may not provide direct insights into the meaning of specific dimensions.LSA 创建的缩小语义空间缺乏人类可解释性。虽然它能捕捉语义关系，但可能无法直接洞察特定维度的含义。
▪ Preprocessing Sensitivity:
LSA is highly sensitive to the preprocessing used on data, such as stop word removal and stemming.LSA 对数据预处理非常敏感，如删除停滞词和词干。

### pLSA

Probabilistic Latent Semantic Analysis (pLSA):概率潜语义分析

pLSA is an extension of LSA that operates on a probabilistic framework.pLSA 是 LSA 的扩展，在概率框架内运行。

▪ Assumes documents are generated from a mixture of latent topics.假设文档由潜在主题混合生成。
▪ Each topic is associated with a distribution over words, and each document is assumed to be generated by selecting a topic from this mixture and then choosing words from the selected topic's word distribution.每个主题都与词的分布相关联，每个文档都被假定为通过从该混合物中选择一个主题，然后从所选主题的词分布中选择词来生成。

The goal of pLSA is to find a model that can generate the data observed within a term-document matrix.pLSA 的目标是找到一个能够生成术语-文档矩阵中观察到的数据的模型。

This means we want a function P(w,d) that will generate the corresponding entry in the word-document matrix given the word w and document d.这意味着我们需要一个函数 P(w,d)，它能在给定单词 w 和文档 d 的情况下生成单词-文档矩阵中的相应条目。

\[
    P(w,d)=P(d)\sum _tP(w|t)P(t|d)
\]

Intuitively, this means the probability of seeing a particular word in a document should be given by the product of probability of the document P(d) and sum over all topics for the conditional distribution of words given topic P(w|t) and P(t|d).直观地说，这意味着在文档中看到某个特定单词的概率应该是文档概率 P(d) 与所有主题的单词条件分布总和 P(w|t) 和 P(t|d) 的乘积。

LSA vs pLSA

LSA
▪ SVD based decomposition:
LSA is a relatively straightforward technique that relies on singular value decomposition (SVD) for dimensionality reduction. As a result, LSA is easily scalable.LSA 是一种相对简单的技术，它依靠奇异值分解（SVD）来降低维度。因此，LSA 易于扩展。
▪ Interpretability:
While LSA can reveal semantic relationships between words and documents, it may not provide human- interpretable topics, as it doesn't explicitly model topics in a probabilistic way.虽然 LSA 可以揭示单词和文档之间的语义关系，但它可能无法提供人类可解释的主题，因为它没有明确地以概率方式为主题建模。

pLSA
▪ Probabilistic modelling:
pLSA views the generation of a document as a probabilistic mixture of topics. This means pLSA is less scalable than LSA due to its higher complexity.pLSA 将文档的生成视为主题的概率混合物。这意味着 pLSA 因其更高的复杂性，其可扩展性不如 LSA。
▪ Interpretability:
pLSA is more interpretable as it explicitly defines topics as probability distributions over words, allowing users to interpret topics based on their word distributions.pLSA 的可解释性更强，因为它将主题明确定义为词的概率分布，允许用户根据词的分布来解释主题。

### NMF

Non-negative Matrix Factorisation (NMF):非负矩阵因式分解

NMF aims to find latent topics within a document by factorising a term-document matrix.NMF 的目的是通过对术语-文档矩阵进行因式分解，找到文档中的潜在主题。

The term-document matrix is factorised into 2 parts:
▪ A word-topic matrix词-主题矩阵
▪ A topic document matrix主题文档矩阵

These matrices can then be used to infer the semantic relations of words with each sentence.这些矩阵可用于推断单词与每个句子的语义关系。

Steps:

▪ Similar to LSA, a term-document matrix of size 𝒏×𝒎 normalised using TF-IDF needs to be generated.与 LSA 类似，需要生成一个大小为 𝒏×𝒎 的术语-文档矩阵，并使用 TF-IDF 进行归一化。

▪ The matrix is then factorised into two matrixes, one of n-words by k-topics and the other of k-topics by m-original documents.然后将矩阵分解为两个矩阵，一个是由 k 个主题组成的 n 个词矩阵，另一个是由 m 个原始文档组成的 k 个主题矩阵。

![alt text](image-15.png)

▪ Intuitively, 𝑾+ represents every topic and the terms found within the topic.直观地说，𝑾+ 表示每个主题和在主题中找到的术语。

▪ 𝑯+ represents every document and the topics found within the document.𝑯+ 代表每个文档和在文档中找到的主题。

It is assumed that all elements of matrices W and H are positive given the elements of A are positive.假设矩阵 W 和 H 的所有元素都是正数，因为 A 的元素都是正数。

When factorising the matrix, the two main cost functions that can be used are:在对矩阵进行因式分解时，可以使用两种主要的成本函数：

Generalised Kullback–Leibler Divergence广义库尔巴克-莱伯勒离差

![alt text](image-16.png)

As the value of the KL-divergence reaches zero, the closeness of corresponding words increases.当 KL-发散值为零时，相应词语的接近度增加。

Frobenius Norm弗洛贝尼斯规范

![alt text](image-17.png)

Defined as the square root of the sum of the absolute squares of its elements, the Frobenius Norm is a method of measuring how good an approximation is.Frobenius Norm 定义为其元素绝对平方和的平方根，是一种衡量近似程度的方法。

Implementation with Scikit-Learn:

![alt text](image-18.png)

![alt text](image-19.png)

![alt text](image-20.png)

Advantages
▪ Parts-Based Representation:
NMF naturally produces parts-based representations, which is valuable in applications like image processing and text mining. It can discover fundamental components or topics within data.NMF 自然生成基于部件的表示，这在图像处理和文本挖掘等应用中非常有价值。它可以发现数据中的基本组成部分或主题。

▪ Noise Reduction:
NMF can help reduce the impact of noise in data because it focuses on capturing underlying patterns and structures rather than specific noisy details.NMF 可以帮助减少数据中噪声的影响，因为它侧重于捕捉基本模式和结构，而不是特定的噪声细节。

Limitations
▪ Non-convex Optimization:
NMF is based on non-convex optimisation, which means it may converge to local minima rather than the global minimum. The quality of results can be sensitive to initialisation.NMF 基于非凸优化，这意味着它可能会收敛到局部最小值，而不是全局最小值。结果的质量可能对初始化很敏感。
▪ Preprocessing Sensitivity:
NMF is highly sensitive to the preprocessing used on data, as well as the choice of cost function for the model.NMF 对用于数据的预处理以及模型成本函数的选择非常敏感。

Summary:

LDA
▪ A probabilistic generative model used for topic modeling in text data.用于文本数据主题建模的概率生成模型。
▪ Used to discover latent topics in text data, categorise documents into topics, or perform content recommendation based on topics. Suited for clustering tasks用于发现文本数据中的潜在主题，将文档归类为主题，或根据主题进行内容推荐。适用于聚类任务

LSA
▪ A linear algebra-based technique that uses singular value decomposition (SVD) for dimensionality reduction.一种基于线性代数的技术，使用奇异值分解（SVD）进行降维。
▪ Used to capture semantic relationships between terms and documents, improve information retrieval, or perform dimensionality reduction on text data.用于捕捉术语和文档之间的语义关系，改进信息检索，或对文本数据进行降维处理。

NMF
▪ Factorises a term- document matrix into two lower-dimensional non- negative matrices.将术语-文档矩阵析构为两个低维非负矩阵。
▪ Used to create parts-based representations to discover interpretable topics in text. NMF is valuable in scenarios where non-negativity and sparsity constraints are important.用于创建基于部分的表示法，以发现文本中可解释的主题。NMF 在非负性和稀疏性约束非常重要的情况下非常有价值。

## Dimensionality Reduction降维

Why do we need dimensionality reduction?

▪ Text data is often high-dimensional, sparse and complex.文本数据通常是高维、稀疏和复杂的。
▪ Computational requirements increase exponentially with the number of dimensions.计算要求随着维数的增加而呈指数增长。
▪ It is hence necessary to condense this data into a more usable form.因此，有必要将这些数据浓缩为更可用的形式。
▪ Vector dimensionality reduction in Natural Language Processing (NLP) is the process of reducing the number of features (dimensions) in a vector representation of text data.自然语言处理（NLP）中的矢量降维是减少文本数据矢量表示中特征（维度）数量的过程。
▪ Dimensionality Reduction techniques include:
- PCA
- SVD

### PCA
Principal Component Analysis (PCA):主成分分析

PCA is a linear technique that finds orthogonal axes in the data that capture the most variance.PCA 是一种线性技术，它能在数据中找到捕捉方差最大的正交轴。

▪ PCA aims to project the data onto a lower-dimensional space while minimizing information loss.PCA 旨在将数据投射到低维空间，同时尽量减少信息丢失。
▪ PCA works by transforming the original data to a new set of variables called the principal components (PCs), which are uncorrelated and can be ordered so that the first few PCs can retain most of the variation present in all the original variables of the dataset.PCA 的工作原理是将原始数据转换为一组新的变量，称为主成分（PC），这些主成分互不相关，可以排序，因此前几个 PC 可以保留数据集所有原始变量中存在的大部分变化。

![alt text](image-21.png)

How it works:

▪ PCA aims to construct lines (2D), planes (3D) or hyperplanes (>3D) which are unit vectors orthogonal to the original features.PCA 的目的是构建与原始特征正交的单位向量线（2D）、平面（3D）或超平面（>3D）。
▪ To do this, we want to minimize the mean perpendicular distance from the PC line for all points through min 为此，我们希望通过最小值
\[
    min(\frac{1}{n}\sum _i^n(x_i^Tx_i-(u_1^Tx_1)^2))
\]
▪ The function reaches a minimum when 𝒖_𝟏= the eigenvector of the covariance matrix of x.当 𝒖_𝟏= x 的协方差矩阵的特征向量时，函数达到最小值。

![alt text](image-22.png)

The goal is to maximize 𝐷1and minimize 𝐷2while keeping 𝐷3 constant.目标是最大化𝐷1，最小化𝐷2，同时保持𝐷3 不变。

PCA can be done manually using the following steps:

1 Standardise the data.将数据标准化。
2 Compute the covariance matrix of the dataset.计算数据集的协方差矩阵。
3 Derive the corresponding eigenvalues and eigenvectors on the normalised dataset.在标准化数据集上推导出相应的特征值和特征向量。
4 PCs can be calculated using the dot product of the eigenvectors and the standardised columns.可以使用特征向量和标准化列的点积计算 PC。

PCA in Scikit-Learn:

![alt text](image-23.png)

![alt text](image-24.png)

在该数据框中，每列代表一条推文。即使删除了停顿词，原始 TF-IDF 向量仍有 1078 个维度。

![alt text](image-25.png)

![alt text](image-26.png)

Advantages

▪ Visualisation:
PCA is valuable for visualising high-dimensional data. It projects data onto lower-dimensional spaces, making it easier to plot and analyse in 2D or 3D.PCA 对于高维数据的可视化很有价值。它可以将数据投射到低维空间，使其更易于绘制和分析二维或三维图形。
▪ Feature Engineering:
PCA can be used for feature engineering by creating new features as linear combinations of the original features. These new features may have improved discriminative power.PCA 可用于特征工程，将原始特征线性组合为新特征。这些新特征可能具有更好的判别能力。

Limitations
▪ Lack of Interpretability:
While PCA simplifies data representation, the new features (principal components) are linear combinations of the original features and may not have clear semantic meaning.虽然 PCA 简化了数据表示，但新特征（主成分）是原始特征的线性组合，可能没有明确的语义。
▪ Linearity Assumption:
PCA assumes that relationships between variables are linear. If the data contains non-linear relationships, PCA may not capture them effectively.PCA 假定变量之间的关系是线性的。如果数据包含非线性关系，则 PCA 可能无法有效捕捉这些关系。

### SVD

Singular Value Decomposition (SVD)奇异值分解

SVD aims to factorise a given matrix into three separate matrices to uncover hidden patterns and structure within the data.SVD 的目的是将给定矩阵因式分解为三个独立的矩阵，以揭示数据中隐藏的模式和结构。

Given an input matrix (a term-document matrix for NLP), SVD decomposes the matrix into 3 separate matrices:给定一个输入矩阵（NLP 的术语-文档矩阵），SVD 将矩阵分解为 3 个独立的矩阵：
▪ 𝑼: Left singular vectors matrix, representing relationships between rows in the original data. This often represents the relationship between terms and topics.左奇异向量矩阵，表示原始数据中各行之间的关系。这通常代表术语和主题之间的关系。
▪ 𝜮: Diagonal matrix of singular values, capturing the importance of each singular vector (higher values indicate more significance).奇异值对角矩阵，表示每个奇异向量的重要性（数值越大表示越重要）。
▪ 𝑽𝑻 : Right singular vectors matrix, representing relationships between columns in the original data. This often represents the relationship between documents and terms.右奇异向量矩阵，表示原始数据中列之间的关系。这通常代表文档和术语之间的关系。

A variation of SVD, k-SVD only takes into account the k largest singular values to approximate the data.作为 SVD 的一种变体，k-SVD 只考虑 k 个最大奇异值来逼近数据。

![alt text](image-27.png)

SVD in Scikit-Learn:

![alt text](image-28.png)

![alt text](image-29.png)

![alt text](image-30.png)

Advantages
▪ Semantic Relationships:
SVD captures semantic relationships between terms and documents. The resulting low-dimensional representations often contain meaningful information about the underlying structure of the data.SVD 可捕捉术语和文档之间的语义关系。由此产生的低维表示通常包含有关数据基本结构的有意义信息。
▪ Interpretability:
The reduced dimensions are often more interpretable, making it easier to understand and analyse the data. It aids in tasks like topic modeling and sentiment analysis.缩减后的维度通常更具可解释性，更易于理解和分析数据。它有助于主题建模和情感分析等任务。

Limitations
▪ Scaling Sensitivity:
SVD is sensitive to the scaling of features. It is essential to standardise or scale features appropriately before applying SVD.SVD 对特征的缩放很敏感。在应用 SVD 之前，必须对特征进行适当的标准化或缩放。
▪ Choosing Dimensionality:
Deciding the appropriate number of dimensions (singular values) to retain can be subjective. An incorrect choice may lead to information loss or overfitting.决定要保留的适当维数（奇异值）可能是主观的。不正确的选择可能会导致信息丢失或过度拟合。

## Summary

Term weighting schemes:
▪ Term weighting involve assigning numerical values to words in a document based on their importance, facilitating tasks like information retrieval and text analysis.术语加权涉及根据文档中词语的重要性为其分配数值，从而为信息检索和文本分析等任务提供便利。
▪ Helps prioritise relevant terms and improve the accuracy of various NLP tasks.有助于优先处理相关术语，提高各种 NLP 任务的准确性。

Topic Modeling:
▪ Topic modeling uncovers hidden thematic structures in large text collections, enabling automated discovery of topics and patterns within documents.主题建模可发现大型文本集合中隐藏的主题结构，从而自动发现文档中的主题和模式。
▪ Used for tasks like document clustering, content recommendation, and understanding the content of unstructured text data.用于文档聚类、内容推荐和理解非结构化文本数据内容等任务。

Vector Dimensionality Reduction:
▪ Vector dimensionality reduction simplifies high-dimensional data representations, improving computational efficiency and interpretability while retaining essential information.矢量降维简化了高维数据表示，提高了计算效率和可解释性，同时保留了基本信息。
▪ Transforms data into lower-dimensional spaces, aiding in visualisation, noise reduction, and data analysis.将数据转换到低维空间，有助于可视化、降噪和数据分析。