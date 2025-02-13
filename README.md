# 使用 scikit-learn 进行 20newsgroups 分类任务

```python
from sklearn.datasets import fetch_20newsgroups
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline
from sklearn.metrics import accuracy_score

# 载入 20newsgroups 数据集
newsgroups_train = fetch_20newsgroups(subset='train')
newsgroups_test = fetch_20newsgroups(subset='test')

# 创建一个 Pipeline，用于文本特征提取和 logistic regression
pipeline = make_pipeline(CountVectorizer(), LogisticRegression())

# 使用训练集训练模型
pipeline.fit(newsgroups_train.data, newsgroups_train.target)

# 在测试集上进行预测
y_pred = pipeline.predict(newsgroups_test.data)

# 输出模型的准确率
print("Accuracy: %.2f" % accuracy_score(newsgroups_test.target, y_pred))

```

在这个代码中，我们首先使用 `fetch_20newsgroups()` 方法从 scikit-learn 自带的数据集中载入 20newsgroups 数据集。

然后，我们使用 `make_pipeline()` 方法创建了一个 Pipeline，其中包括了 CountVectorizer() 和 LogisticRegression()。

我们使用 `fit()` 方法在训练集上训练模型。之后，我们使用 `predict()` 方法对测试集进行预测，并使用 `accuracy_score()` 方法计算模型的准确率。

最后，我们打印出模型的准确率。

CountVectorizer() 是一个用于文本特征提取的方法，它将文本转换为单词计数的向量。

LogisticRegression() 是一种常用的分类算法，用于将输入特征映射到分类概率。

通过将 CountVectorizer() 和 LogisticRegression() 组合起来使用，我们可以很方便地完成文本分类任务。



`CountVectorizer`是scikit-learn中的一个文本特征提取方法，它将文本转换为单词计数的向量。其具体作用是将文本中的单词转换为特征向量，使得机器学习模型可以对文本进行分析和处理。

下面是一个例子，假设我们有以下三个文本：

```python
文本1: This is a sample text.
文本2: This text is another example text.
文本3: This is just another text.
```

我们可以使用`CountVectorizer`将它们转换为向量表示。首先，需要导入CountVectorizer：

```python
from sklearn.feature_extraction.text import CountVectorizer
```

然后，创建一个CountVectorizer对象，并将文本数据传递给它的`fit_transform()`方法：

```python
corpus = [
    'This is a sample text.',
    'This text is another example text.',
    'This is just another text.'
]

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)
```

`X`现在是一个稀疏矩阵，每一行代表一个文本，每一列代表一个单词。单词的出现次数则在矩阵中体现。我们可以使用以下代码查看向量的表示：

```python
print(X.toarray())
```

```python
[[1 1 1 0 0 0 1 0 0]
 [0 2 0 1 0 1 1 0 1]
 [1 0 0 1 1 0 1 1 0]]
```

可以看到，矩阵中的每一行都是一个向量，每一列都代表一个单词。例如，第一行表示的向量是[1, 1, 1, 0, 0, 0, 1, 0, 0]，这个向量的第一个元素代表单词“a”在这个文本中出现了1次，第二个元素代表单词“another”在这个文本中出现了1次，以此类推。

通过`CountVectorizer`，我们可以将文本数据转换为数字向量，从而可以使用机器学习算法对文本进行分析和处理。
