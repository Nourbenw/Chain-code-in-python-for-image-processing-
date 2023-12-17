# Chain-code-in-python-for-image-processing-
Chain code in python for image processing 
import cv2
import numpy as np
from matplotlib import pyplot as plt

image= cv2.imread('88.jpg')
img_gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
ret,thresh = cv2.threshold(img_gray, 127, 255, cv2.THRESH_BINARY )


contours= cv2.findContours(image=thresh, mode=cv2.RETR_TREE, method=cv2.CHAIN_APPROX_NONE)
contours,HIRARACY= cv2.findContours(image=thresh, mode=cv2.RETR_TREE, method=cv2.CHAIN_APPROX_NONE)

object=np.array(contours[0])


boundary=np.empty((len(object),2),int)
for i in range((len(contours[0]))):
    boundary[i]=object[i,:,:]
print('coordinates =  ',boundary)


chaincode=[]
k=0
while k<len(boundary)-1:
    x,z=boundary[k]
    l=k+1
    next_x,next_z=boundary[l]
    if(x==next_x and z+1==next_z):
        code=0
    elif(x-1==next_x and z+1==next_z):
        code=1
    elif(x-1==next_x and z==next_z):
        code=2
    elif(x-1==next_x and z-1==next_z):
        code=3
    elif(x==next_x and z-1==next_z):
        code=4
    elif(x+1==next_x and z-1==next_z):
        code=5
    elif(x+1==next_x and z==next_z):
        code=6
    elif(x+1==next_x and z+1==next_z):
        code=7
    k=k+1
    chaincode.append(code)

print("chain =  ",chaincode)
