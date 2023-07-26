# semantic-segmentation
import os
dir=os.chdir('/content/sample_data/Segmentation/')
dirname="/content/sample_data/Segmentation/"
for i, filename in enumerate(os.listdir(dirname)):
  print(filename)
  os.rename(dirname + "/" + filename, dirname + "/" + str(i) + ".jpg")
  
# folder path
dir_path = r'/content/sample_data/Segmentation'
count = 0
# Iterate directory
for path in os.listdir(dir_path):
    # check if current path is a file
    if os.path.isfile(os.path.join(dir_path, path)):
        count += 1
print('File count:', count)

#install libraries
!pip --version
!pip install --upgrade mxnet
!ip install torch==1.6.0+cpu torchvision==0.7.0+cpu -f https://download.pytorch.org/whl/torch_stable.html
!pip install --upgrade gluoncv
import mxnet as mx
from mxnet import image
from mxnet.gluon.data.vision import transforms
import gluoncv

# using cpu/gpu
ctx = mx.cpu(0)
cwd = os.getcwd()
print("Current working directory: {0}".format(os.getcwd()))
import numpy as np
import mxnet as mx
from mxnet import gluon, autograd
import gluoncv
from matplotlib import pyplot as plt
import os
from gluoncv.data.transforms.presets.segmentation import test_transform
from gluoncv.utils.viz import get_color_pallete
import matplotlib.image as mpimg
from gluoncv.utils import TrainingHistory
model = gluoncv.model_zoo.get_model('psp_resnet101_ade', pretrained=True)
ctx = mx.cpu(0)
cwd = os.getcwd()
print("Current working directory: {0}".format(os.getcwd()))

# Run pretrained model
dir=os.chdir('/content/sample_data/wongtaisin/segmentation')
folder_data=(os.listdir(dir))
for i in range(0,len(folder_data)):
     if '.jpg' in folder_data[i]:
          print(folder_data[i])
          img = image.imread(folder_data[i])
          plt.imshow(img.asnumpy())
          plt.show()
          img = test_transform(img, ctx)
          output = model.predict(img)
          #print(output.labels)
          predict = mx.nd.squeeze(mx.nd.argmax(output, 1)).asnumpy()
          mask = get_color_pallete(predict, 'ade20k')
          print(mask)
          folder_data[i]=folder_data[i].replace(".jpg","")
          output_name=folder_data[i] + "_out.png"
          mask.save('/content/sample_data/wongtaisin/output/' +  output_name)
          mmask = mpimg.imread('/content/sample_data/wongtaisin/output/' +  output_name)
          plt.imshow(mmask)
          plt.show()
# save output
import os
dirname="/content/sample_data/wongtaisin/segmentation/"
#for dirname in os.listdir("."):
    #print(dirname)
#if os.path.isdir(dirname):
for i, filename in enumerate(os.listdir(dirname)):
            print(filename)
           # os.rename(dirname + "/" + filename, dirname + "/" + str(i) + ".jpg")
