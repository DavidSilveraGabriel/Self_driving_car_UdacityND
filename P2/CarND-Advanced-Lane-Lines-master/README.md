## Advanced Lane Finding
### In this project, the goal is to write a software pipeline to identify the lane boundaries in a video

![Lanes Image](./output_images/giphy.gif)


# Navigation 
[camera_cal/](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/tree/master/P2/CarND-Advanced-Lane-Lines-master/camera_cal)  Directory with calibration images

[output_images/](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/tree/master/P2/CarND-Advanced-Lane-Lines-master/output_images) Directory with output images

[test_images/](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/tree/master/P2/CarND-Advanced-Lane-Lines-master/test_images) Directory of images used to test the code

[Examples/](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/tree/master/P2/CarND-Advanced-Lane-Lines-master/examples) Directory with examples of images and code



Main notebook 
---

Steps of this project are the following:

* The camera calibration 
* Apply a distortion correction to raw images.
* Create a thresholded binary image.
* Apply a perspective transform ("birds-eye view").
* Detect lane pixels 

### Pipeline

* Determine the curvature and vehicle position with respect to center.
* Draw in the image the detected lines
* Output visual display

The images for camera calibration are stored in the folder called `camera_cal/`.  The images in `test_images/` are for testing the pipeline on single frames. 

The `challenge_video.mp4` video is an extra (and optional) challenge 
The `harder_challenge.mp4` video is another optional challenge and is brutal!

# Step by step development

## The camera calibration 
Calibrate the camera to correct for image distortions. For this we use a set of chessboard images, knowing the distance and angles between common features like corners, we can calculate the tranformation functions and apply them to the video frames.

- Define corners and the arrays to store object points and image points from all the images.
```
nx = 9 # number of corners in x direction
ny = 6 # number of corners in Y direction
##################
objpoints = [] # 3d points in real world space
imgpoints = [] # 2d points in image plane.
```
- Prepare grid and points to display
```
objp = np.zeros((np.prod(nx*ny),3),dtype=np.float32)
objp[:,:2] = np.mgrid[0:ny, 0:nx].T.reshape(-1,2)
```
- Make a list of calibration images
```images = glob.glob('camera_cal/calibration*.jpg')```

- Step through the list and search for chessboard corners
```for fname in images:
      img = cv2.imread(fname)
      # Converting an image, imported by cv2 or the glob API, to grayscale
      gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)

      # Find the chessboard corners
      ret, corners = cv2.findChessboardCorners(gray, (nx,ny),None)

      # If found, add object points, image points
      if ret == True:
          objpoints.append(objp) #<--- the important we will use later:D 
          imgpoints.append(corners) #<--- the important we will use later:D
```

- send that objpoints and imgpoints to the cv2 function 
```
def cal_undistort(img, objpoints, imgpoints):
    # calibrate camera 
    ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(objpoints, imgpoints, img.shape[0:2], None, None)
    
    # Undistorting the image
    undist = cv2.undistort(img, mtx, dist, None, mtx)
        
    return undist
```

