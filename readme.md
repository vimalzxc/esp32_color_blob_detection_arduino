## Quick start
1. Open http://10.0.0.69/
2. Set Resolution to QQVGA 160x120. It does not work for other resolutions
3. Click on start stream
4. Open COM port at 115200 baud rate
5. The example program is set to detect blobs that are RED in color
6. Whenever a blob is detected, `Found blob!` gets printed on the serial terminal

## Customization
Change `THRES_MIN_R`, `THRES_MAX_R`,`THRES_MIN_G`, `THRES_MAX_G`,`THRES_MIN_B`, `THRES_MAX_B` for the required color
Right now, it is optimized for RED color detection. Although, we are finding RED, there are a little bit of 
other colors as well.
R [90, 240]
G [0, 100]
B [0, 100]

If you want to find a bigger blob, increase BLOB_AREA_SZ
BLOB_AREA_SZ can have a max value of BLOB_WINDOW*BLOB_WINDOW

## Algorithm
Initially, we get a 160x120 image and it is downsampled by a factor of WINDOW_SZ (20) by averaging the neighboring pixels
Resulting matrix is of size, 8 x 6 and is called pooled_matrix
Now, each pixel is checked for the thresholds as mentioned in the previous section.
If the pixel is within the threshold, the corresding index in the bin_matrix is set to 1
Then, we traverse the bin_matrix with a window (BLOB_WINDOW*BLOB_WINDOW) and see if BLOB_AREA_SZ number of
pixels are 1. If yes, then it is a blob!

Looks for BLOB_AREA_SZ number of neighboring pixels which are 1
within BLOB_WINDOW(3) x BLOB_WINDOW(3)(\\)
    Sample bin_matrix
    0   0   0   0   \0   \0   \0   0    \
    0   0   0   0   \0   \1   \1   0    \
    0   0   0   0   \0   \1   \1   0    \
    0   0   0   0   0   0   0   0       \
    0   0   0   0   0   0   0   0       \
    0   0   0   0   0   0   0   0       \

## To Program
1. Connect 5V
2. Connect IO0 to GND
3. Click on the reset button on the board
4. Click Upload on arduino 

## To run application
1. Disconnect IO0 from GND, can be left floating
2. Click on the reset button on the board

## SSH quick links
ssh-agent /bin/bash
ssh-add /c/Users/vchandran/.ssh/id_rsa.pub