---------------------------------------------------------------------------------------------------
 
 # 迁移学习、数据增强、微调的中文自学笔记
 
深度学习往往需要大量算力和数据，但在很多情况下经济实力不允许，大算力遥不可及；另外，当数据集比较小，而且没有办法获取更多数据或制作标注数据比较困难时，如何获取更高的正确率呢？迁移学习、数据增强和微调将给出破题之道。  

一、所谓迁移学习，就是使用在大规模数据集上训练好的模型来解决小数据集问题。这种在大规模数据集上训练好的模型一般称为预训练模型。思路是利用预训练模型的卷积部分（也称卷积基）提取数据集的特征，然后重新训练最后的全连接部分（也称分类器）。在这个特征提取过程中，要确保预训练模型的特征提取部分（也就是卷积基的参数）不能发生变化。迁移学习的思路有以下3步：  
 
(1)冻结预训练模型的卷积基；  
 
(2)根据具体问题重新设置分类器；  
 
(3)用自己的数据集训练设置好的分类器；  
 
不冻结卷积基的话，可以不可以呢？如果卷积部分的参数不冻结，在训练刚开始，由于分类器部分的参数是随机的，这会给整个网络带来巨大的梯度震荡，破坏已经训练好的卷积部分的参数，使得卷积基特征提取能力大大下降。
  
二、数据增强主要是对现有的数据集进行微小的改变，如随机裁剪部分、随机左右或上下翻转、随机旋转一个角度、随机明暗变化等微小的改变。通过将现有的图片进行改变，人为地生成多样化的图片，这样就相当于增大了数据集。当然，数据集本身并没有改变，我们只是将现有数据做了一些微小的更改送进了网络。当数据集比较小，难以获取新的训练数据时，可以考虑使用数据增强的方法来进一步提高正确率、抑制过拟合。  

三、微调是指在使用预训练模型训练完成后，将冻结的卷积基解冻，允许其参数计算梯度进行优化，这样继续训练模型可以得到更高的正确率。微调的关键步骤如下：  

(1)冻结预训练模型卷积基，训练分类器，其实就是前面刚刚讲过的迁移学习所做的；  

(2)分类器训练完毕后，解冻卷积基，继续模型训练；  

这里需要注意的是，一定要冻结卷积基训练好分类器之后，再解冻卷积基进行微调。如果没有训练好分类器就解冻卷积基，这样由于分类器的参数是随机初始化的，在训练刚开始会引入较大的梯度，导致卷积基参数发生较大的震荡，破坏其原有的特征提取能力。

---------------------------------------------------------------------------------------------------
<span style="font-size:140px;">简介</span>

  
  
 

