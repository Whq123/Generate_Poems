# Generate_Poems
Automatically write poems based on user keywords
自动写诗APP项目、基于python+Android实现（技术：LSTM+Fasttext分类+word2vec+Flask+mysql) 
一 、诗歌分类：
首先，在古诗文网上爬取五类诗歌（边塞征战，写景咏物，山水田园，思乡羁旅，咏史怀古）各600首作为分类模型的训练数据。 训练生成FastText分类模型。然后用此分类模型为近30万首诗歌分类。
二、用户主题词分类： 事先分别为五类诗歌设置15个关键词，然后以维基百科为语料训练得到维基百科的word2vec模型。 根据用户输入的主题词，来与各类诗歌的关键词做相似度计算，判断主题词最可能所属的诗歌类别 
三、用户主题词的相似词生成： 之后以分好类的五类诗歌为语料，训练得到各自的word2vec模型。判断主题词类别后，以其所属类别的word2vec模型， 生成6个与主题词最相似的词，作为后续生成诗歌时，每句开头字的候选集合。
四、建立模型 采用深度学习框架tensorflow为五类诗歌分别建立长短期记忆网络模型（LSTM）。 把主题词最相似的6个词作为每句诗的开头字的候选集合，并将LSTM模型生成的每个候选字通过《诗学含英》进行概率权重计算，最终选择概率最大的字作为生成字。 在生成2/4/6/8句诗歌时，对最后一个字按照《汉字押韵字表》进行押韵筛选过滤，实现诗歌的押韵机制。 
五、前端展示 以APP的形式与用户进行移动端展示。服务器端用的Flask框架，连接的MySQL数据库，用于保存用户注册的基本信息。 在APP的主界面下，用户输入主题词，可选择生成此主题下的五言绝句、五言律诗、七言绝句、七言律诗，随后服务器将生成的诗歌返回到APP的主界面进行展示。


Android端代码在目录：Android/LoginDemo/app/src/main/java/com/example/logindemo/
使用的是，AndroidStudio编程
Python端代码在Python目录下；
python端应用环境：
tensorflow
fasttext
flask
numpy
pandas

项目介绍链接：https://mp.csdn.net/postedit/92379563
项目的应用数据：
链接：https://pan.baidu.com/s/1xg7LPObdx2vbi28vqsjrwg 
提取码：1wg2 
data_dir目录，是5类诗歌生成此类诗的相似词的word2vec模型 + 数据
generate_poem目录，是用于生成5类诗歌的LSTM模型
train_jar目录，是诗歌前期fasttext分类模型 + 数据
wiki_model目录，是判别关键词所属类别的维基百科的word2vec模型
