# smart elevator system
# smart elevator system which will reduce the power consumption and saves precious time. 
# python program that will count the no of faces by using haar cascade and will return the floor with highest no of people
# then according to that priority the lift will go to that floor.

from firebase import firebase  # for updateing the data on the server

import numpy as np

import cv2

face_cascade= cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

eye_cascade=cv2.CascadeClassifier('haarcascade_eye_default.xml')

cap = cv2.VideoCapture(0)

count=0
i=1
highest=0

while 1:
   for level_1 in range(0,255):    #for no of people in floor 1
       no_of_people_1=face_count

   for level_2 in range(0,255):     #for no of people in floor 2
       no_of_people_2=face_count

    for level_3 in range(0,255):     #for no of people in floor 3
       no_of_people_3=face_count

    for level_4 in range(0,255):      #for no of people in floor 4
       no_of_people_4=face_count

    for level_5 in range(0,255):        #for no of people in floor 5
       no_of_people_5=face_count

    highest=max(no_of_people_1,no_of_people_2,no_of_people_3,no_of_people_4,no_of_people_5)
    
def face_count():     # for counting no of faces
    ret, img = cap.read()
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)
    count=len(faces)
    print("Number of faces is:",count)

    for (x,y,w,h) in faces:
        cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),3)

        roi_gary=gray[y:y+h,x:x+w]
        roi_color=img[y:y+h,x:x+w]
        eyes=eye_cascade.detectMultiScale(roi_gary)
        for(ex,ey,ew,eh) in eyes:
            cv2.rectangle(roi_color,(ex,ey),(ex+ew,ey+eh),(0,255.0),2)
    cv2.imshow('img',img)

    return count    # returns the no of faces in the loop
    
    
 firebase=firebase.FirebaseApplication("https://first-file42.firebase.com")
 
 data=('faces':count)
 
 result=firebase.put("https://first-file42.firebase.com/'*'/data")  #update the value on the firebase

cap.release()

cv2.distroyAllWindows()   
    
