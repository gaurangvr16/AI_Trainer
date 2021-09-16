import cv2
import time
import numpy as np
from AI_Trainer_Project import PoseEstimationModule as pm

detector = pm.PoseDetector()
cap = cv2.VideoCapture(0)

count = 0
dir = 0

prevTime = 0
while True:
    success, img = cap.read()
    img = detector.findPose(img, False)
    lmList = detector.findPosition(img, False)
    if len(lmList) != 0:
        # Right arm
        angleRight = detector.findAngle(img, 12, 14, 16)
        # Left Arm
        #angleLeft = detector.findAngle(img, 11, 13, 15)

        perRight = np.interp(angleRight, (40,175), (0, 100))
        #perLeft = np.interp(angleLeft, (210, 310), (0, 100))

        #bar = np.interp(angleRight, (40, 175), (650, 100))

        # to check and count the curls
        color = (255, 0, 255)

        if perRight == 100:
            color= (0,255, 0)
            if dir == 0:
                count += 0.5
                dir = 1
        if perRight == 0:
            color= (0, 255, 0)
            if dir == 1:
                count+=0.5
                dir = 0


        # to show count of bicep curls
        cv2.putText(img, str(int(count)), (50, 100), cv2.FONT_HERSHEY_PLAIN, 10, (255,0, 0), 20)

    curTime = time.time()
    fps = 1/(curTime-prevTime)
    prevTime = curTime
    #cv2.putText(img, str(int(fps)), (50, 100), cv2.FONT_HERSHEY_PLAIN, 5, (255, 0, 0), 5)
    cv2.imshow("Image", img)
    cv2.waitKey(1)