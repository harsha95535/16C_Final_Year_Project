#Real Time OCR
Perform text detection in a variety of languages with your computer webcam using Google Tesseract OCR and OpenCV. 
This script achieves a real-time OCR effect by incorporating multi-threading.

The CV2 video stream is instantiated in a dedicated class, in a dedicated thread, so it's always reading live frames from the webcam and storing the most recent frame as an instance attribute. The video display can access these frames and show them in real-time. Meanwhile, pytesseract OCR has its own dedicated class, running in a dedicated thread, and it simply grabs the most recent frame from the video stream class, processes it, and outputs the data. The result is a capable real-time OCR. True, the bounding boxes might lag if the text is moved around quickly, and sometimes it needs a moment to detect the text, but this is an astronomical improvement from the ultra-slow, bottlenecked video stream you get from processing in a single thread.


### USE

This a command-line script. The only required argument is a full path to the Tesseract executable from the Tesseract install (see DEPENDENCIES below for more info)

`python Main.py -t '<full_path_to_your_tesseract_executable>' [-c ] [-v] [-sv] [-l] [-sl] [-s]`


required named arguments:
  -t , --tess_path   path to the cmd root of tesseract install (see docs for further help)


The crop area allows OCR to be performed on a smaller frame and therefore improves speed. A box is automatically drawn around the crop so it's clear where to position text for detection.

#### View Mode

This script implements four view modes, which stylize the way text is detected. To specify a view mode, use -v <int mode> after the Main.py call

<img src="https://user-images.githubusercontent.com/79942554/114243131-ebebfc00-9940-11eb-808e-51179cd4139e.gif" width="700">

_(View mode 1: Draws boxes on text with >75 confidence level)_

<br />



<img src="https://user-images.githubusercontent.com/79942554/114243144-f1e1dd00-9940-11eb-88e7-a32572ebacc1.gif" width="700">

_(View mode 2: Draws red boxes on low-confidence text and green on high-confidence text)_

<br />



<img src="https://user-images.githubusercontent.com/79942554/114243169-fc9c7200-9940-11eb-9788-dc6894cb9db9.gif" width="700">

_(View mode 3: Color changes according to each word's confidence; brighter indicates higher confidence)_

<br />



<img src="https://user-images.githubusercontent.com/79942554/114243187-01f9bc80-9941-11eb-9384-3e2b983b2498.gif" width="700">

_View mode 4: Draws a box around detected text regardless of confidence_

<br />


If no view mode is specified, the OCR will run with mode 1.

To see the view options and their descriptions in the command line, evoke -sv or --show_views


#### SRC Video Source

In the case of multiple camera ports, the src for the desired video input can be specified with the -s command-line arguemnt. Without specification, the src defaults to 0, which for most users is a built-in webcam.

Using SRC source 0:

`python Main.py -t '<full_path_to_your_tesseract_executable>' -s 0`

Using SRC source 1:

`python Main.py -t '<full_path_to_your_tesseract_executable>' -s 1`

#### Language

Tesseract can detect a variety of langauges since version 4+. A language can be specified to the OCR by appending the Main.py call with "-l <language code>"


Multiple languages can be simultaneously detected by appending the codes with '+'. To detect both simplified chinese and traditional chinese, use:

`python Main.py -t '<full_path_to_your_tesseract_executable>' -l chi_sim+chi_tra`

A list of all language codes can be printed in the command line by evoking '-sl'.


