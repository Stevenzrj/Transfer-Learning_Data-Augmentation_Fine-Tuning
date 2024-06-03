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

--------------------------------------------------------------------------------------------------
**简介**





--------------------------------------------------------------------------------------------------
**基本环境配置和数据集准备**    

安装PyTorch之前需先安装Python，推荐使用Miniconda搭建Python环境。Miniconda是最小的Conda安装程序，它提供了类似沙盒的环境，避免了在旧的Python环境中安装可能会遇到的库依赖冲突等问题。Miniconda本身包含Python，安装Miniconda后将获得Conda包管理工具和Python环境。
可在Miniconda官网（ https://docs.conda.io/en/latest/miniconda.html ）下载适合当前系统的、64位的、使用Python 3的Miniconda安装包。  

PyTorch分为CPU版本和GPU版本；GPU版本需有NVIDIA显卡硬件支持，可以利用NVIDIA GPU强大的计算加速能力，使PyTorch的运行更为高效，尤其是可以成倍提升模型训练的速度。如果计算机没有NVIDIA显卡硬件支持，请直接安装CPU版本，安装命令参考PyTorch官网：https://pytorch.org/get-started/locally/  

另外，Windows平台还需要安装Microsoft Visual C++(VC_redist.x64.exe)，可从微软网站（网址为： https://docs.microsoft.com/zh-CN/cpp/windows/latest-supported-vc-redist ）下载安装最新支持的Visual C++。在很多时候，计算机可能已经安装过Visual C++，如果安装时提示已经安装了其他版本，那就没有必要重复安装了。  

完成PyTorch库的安装后，还需要安装辅助库，如绘图库Matplotlib、数据分析库pandas以及开发编辑工具Jupyter Notebook等，可在Anaconda Prompt命令行或者终端执行：   
```bash
pip install pandas matplotlib notebook

数据集需提前从以下链接下载：https://www.microsoft.com/en-us/download/details.aspx?id=54765

--------------------------------------------------------------------------------------------------
**代码链接**


  
  
 

