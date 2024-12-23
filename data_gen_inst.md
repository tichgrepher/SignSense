# Data Generation Instructions

## Hold vs. Non-hold
- if the sign involves a gesture it is a **non-hold**
- if the sign is simply a hand shape it is a **hold**

## Where to store the videos
Store videos in a directory named with the label of the signs. 

## Confirm the quality of the videos
At any point videos can be rewatched with a mp overlay to ensure the tracking is good using the following `holistic.py` command

`python holistic.py multi <video dir> <start index>`
* note this will create a folder in the video directory called `mp` with your videos with the mp overlay
* it will also display the tracking as it happens, press `q` on the video window to skip to the next vid.

for example if I want to verify my current vids are tracking well for a sign apple I would use
`python holistic.py multi C:\signs\apple 0`

or to start at the 10th video I would do 

`python holistic.py multi C:\signs\apple 9`

## Recording

**hold** videos should be done as follows:
    
- length in multiples of **10 + 1** second for setup at start to get mediapipe to recognize the hand
- data can be in as many videos as needed as long as the total recorded length is **>240** seconds
- in past I have done many 11 second videos with a few longer videos once I'm certain the gesture I'm making is tracking well in mediapipe

**non-hold** videos as follows:
- 1 video per sign iteration
- keep videos **at or below 2 seconds** including setup time
- in past I have recorded a **minimum 60** vids for these signs, but the more the better

store vids in the following structure
```
-> videos
    -> apple
        -> vid1.mp4
        -> vid2.mp4
        -> ...
    -> orange
    -> etc...
```

## Data Generation

once vids are recorded generate data using the following holistic.py command

`python holistic.py dataset <dir with sign subdirs> <output directory>`

using the structure above, the following command:
`python holistic.py dataset /path/to/videos /output`

will generate an output structure like this:
```
-> output
    -> apple
        -> vid1.npy
        -> vid2.npy
        -> ...
    -> orange
    -> etc...
```

this is the data, it can then be sorted into the hold and non hold directory

## Committing Your Changes
Please make the changes in a new branch with the following naming convention: `data/<signs separated by '-'>`.
Only commit the generated numpy data, **DO NOT** include the videos!
