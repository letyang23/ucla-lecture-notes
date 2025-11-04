# 8/25/2025 Lecture 1

- COURSE GRADE DECISION
  - One Term Exam – 35 % (Monday Nov 10th 2025)
  - Assignments, Project 65%
    - 2 to 3 Theory/Programming Assignments (35%)
    - Project, done in a group of 2-3 students (30%)
    - Project demo dates: Wed Dec 10th - Fri Dec 12th
    - Attendance – potentially 5%

- Introduction (Question: which are Examples and not Examples of Multimedia)
  - Reading a newspaper
  - Describing a Picture to your friend
  - Video Game Playing and Multiplayer Games
  - Riding a bicycle
  - Video Conferencing
  - Visiting your doctor
  - Watching Television
  - Assembling a car in a garage
  - Listening to Radio
  - Having a telephone conversation

- Historical Perspective
  - When was the word multimedia created?
  - Timeline of information creation and distribution
- Multimedia Data and Information
  - Contains a mixture different type of media – text, images, video, audio, graphics
  - Definition and media types have been changing 
- Multimedia Systems
  - Generation & Capture
  - Processing and Content Creation
  - Storage
  - Distribution
  - Rendering and Consumption

<img src="Lecture Notes.assets/image-20250903180024154.png" alt="image-20250903180024154" style="zoom:80%;" />

###### Multimedia Processing Pipeline

- Audio  
- Image  
- Video  
- Text  
- Tactile  
- 2D graphics  
- 3D graphics  

---

##### **Authoring → Compression → Distribution → Devices** 

#### Authoring

Digital:

- Capture  
- Editing  
- ...  

#### Compression

Methods:

- Software
- Hardware
- Compression

Examples of formats:

- MP3  
- HEVC  
- MP4 ...

> Storage (CD, DVD are kinds of storage) happens between *Authoring* and *Compression*.  

#### Distribution

- Satellite  
- Radio tower  
- Ethernet, Network'
- Wires ...

> Business Logic like advertising, encryption/DRM, subscriber management happen between Compression and Distribution

#### Devices

- TV
- Computers
- Laptops
- Speakers
- Cellphone
- Projectors
- Radio receiver
- Printers
- VR devices...

---

#### Media Types - An "In"complete Taxonomy

- Current Media Types
  - Text – Hypertext
  - Images – Static & Dynamic
  - Audio – Speech, Music
  - Video – Movies, Documentaries
  - 2D Graphics – Vector Graphics, 2D Sprites
  - 3D Graphics – Games

- Future Media Types `like hologram`

##### Image - Gray and Color

`Represent color by RGB in text`

##### Video - How do you describe video?

- Bitstreams

##### Audio

- Audio Media is of various kinds
- CD Quality (uncompressed)
- Mp3 compressed audio (.mp3)
- Speech (.wav)
- MIDI example (.mid)
- How do you describe audio?

##### 2d-graphic and 3d-graphic vector representation

- Vector representation

##### Media Types - Conclusion

- We have seen a lot of media types that are currently used; there may be others in future depending on
  - Need for information
  - Capture device technologies
  - Rendering devices and technologies
- Need for standards
  - Many media types, having many formats
  - Information has to be easily interchanged and displayed

#### Examples in Multimedia

- ImmersiveMedia – Interactive Video `you can move around 360 during the video`
- Augmented/Virtual Reality – Oculus VR, Holoportation
- Deep Learning with media – GAUGAN, DALL-E 2, Synthesizing Obama,
- Movies, Animation & VFX Pipeline
- Performance capture technologies
- Display Technologies- Auto stereoscopic Displays,
- Institute for Creative Technologies
- InFORM – Make the digital physical
- Research Progress – the Visual Microphone, Cocktail
- Party, NERFs

##### Inherent Qualities of Multimedia

- Digital Always
- Mixture of different media types
- Interactive
- Multimedia Data is huge
- Real Time Issues
- Synchronization Issues
  - Intra media Time dependencies `Intra is within the video itself`
  - Inter media Time dependencies `Inter media is between media types`
    - `example: How to makesure the video and audio is synchronized`

##### Introduction (Question: which are Examples and not Examples of Multimedia) - Revisit - Everything can be multimedia

- Reading a newspaper - 
- Describing a Picture to your friend
- Video Game Playing and Multiplayer Games
- Riding a bicycle
- Video Conferencing
- Visiting your doctor
- Watching Television
- Assembling a car in a garage
- Listening to Radio
- Having a telephone conversation

# 9/8 Lecture 2

### Digital Data Acquisition & Media Basics

<img src="Lecture Notes.assets/image-20250917163634567.png" alt="image-20250917163634567" style="zoom:80%;" />

##### Digital Data Acquisition

`Take the physical world to recreate it into the digital medium`

Example: Camera

What does the camera capture? - Light

How does it works? 

- A lens at front and capture all rays of light coming from the world and focus onto an image plane.
- Image plane is a 2D plane. 
- Analog signal -> Digital signal (probably convert back to analog)

<img src="Lecture Notes.assets/image-20250917164626007.png" alt="image-20250917164626007" style="zoom:80%;" />

Sampling & quantization in A->D process

y = x(t) 

$X_s[n] = x(nT)$

T = sampling period

1/T = f = sampling frequency

$T++$ -> $ f--$

T-- -> f++



Quantization

$[X_s[n]]$

- **Function of a Camera**:
  - Captures **light** and measures its energy per unit area.
  - Converts this into a **pixel value** in digital representation.
- **How it Works**:
  1. **Lens**: Collects rays of light from the environment and focuses them on an **image plane** (2D surface).
  2. **Image Plane**: Contains an array of sensors arranged row by row.
  3. **Sensors**: At each location, light falling on the sensor produces an **electrical charge**.
     - The amount of charge depends on the intensity of incident light (analog signal).
- **Signal Conversion**:
  - The analog signal (electrical charge) is passed through an **Analog-to-Digital Converter (ADC)**.
  - This generates a **digital signal** that can be stored, processed, or transmitted.
  - A **snapshot** captures either a still image or a sequence of frames (video).
- **Editing and Transmission**:
  - Digital signals can be used for editing (e.g., video editing, adding graphics).
  - Before reaching the user, the signal often undergoes **compression/decompression**.
  - Consumer devices (monitors, TVs, etc.) may require conversion **back to analog** for display.
- **Overall Goal**:
  - Ensure that what the **human eye perceives** is faithfully captured, digitized, transmitted, and finally displayed.
  - The process is **iterative and two-way**, aiming for minimal loss of information.

<img src="Lecture Notes.assets/image-1758518925262-1.jpg" alt="img" style="zoom:80%;" />

<img src="Lecture Notes.assets/image-1758518941943-4.jpg" alt="img" style="zoom:80%;" />

### Example Signals

<img src="Lecture Notes.assets/image-20250921222952584.png" alt="image-20250921222952584" style="zoom:80%;" />

### Quantization Example in 1D

<img src="Lecture Notes.assets/image-20250921223025751.png" alt="image-20250921223025751" style="zoom:80%;" />

### Quantization Example in 2D

<img src="Lecture Notes.assets/image-20250921223049799.png" alt="image-20250921223049799" style="zoom:50%;" />

<img src="Lecture Notes.assets/image-20250921223056387.png" alt="image-20250921223056387" style="zoom:50%;" />

<img src="Lecture Notes.assets/image-20250921223130497.png" alt="image-20250921223130497" style="zoom:50%;" />

### Bit Rate

<img src="Lecture Notes.assets/image-20250921223153116.png" alt="image-20250921223153116" style="zoom:80%;" />

**The Nyquist Theorem:** To perfectly reconstruct a signal without loss, the sampling frequency must be **at least twice the maximum frequency** present in the original signal.

**Fourier Analysis:** The Fourier transform is a mathematical tool used to break down a signal into its constituent frequencies, which allows us to identify its maximum frequency.

**Aliasing:** If a signal is sampled below the Nyquist rate, errors called **aliasing artifacts** occur. This can manifest as jagged edges in images (**2D aliasing**), strange patterns on clothing (**moiré patterns**), or the illusion of wagon wheels spinning backward (**temporal aliasing**).

##### Aliasing Examples

- Spatial Aliasing in one dimension
  - Example of a sinusoidal function in 1D
  - Audio aliasing (single frequency)
  - Audio without aliasing –
    - and with aliasing
- Spatial Aliasing in two dimensions

<img src="Lecture Notes.assets/image-20250921230439366.png" alt="image-20250921230439366" style="zoom:80%;" />

- Spatial aliasing, moiré lines in patterns
- Temporal Aliasing
  - Wagon Wheel
  - A real example

<img src="Lecture Notes.assets/Screenshot 2025-11-02 at 9.27.23 PM.png" alt="Screenshot 2025-11-02 at 9.27.23 PM" style="zoom:80%;" />

- Signal is the number of circles coming in
- Sampling is the screen resolution.
- The screen resolution is not high enough to match the frequencies of the circle coming in, then you see some kind of aliasing effects.

<img src="Lecture Notes.assets/Screenshot 2025-11-02 at 9.30.10 PM.png" alt="Screenshot 2025-11-02 at 9.30.10 PM" style="zoom:80%;" />

- Signal is the rate of the revolution.
- Sampling is the display
- If the screen is diplaying at twice the frequency of the revolution, we can read the direction it's supposed to go.
- If the speed is more than half of the refresh rate, it will create aliasing.

Subsampling

- Happened in uploading process to rescale the image to something which is bandwidth appropriate.
- Meaning throwing away

Filters

- Processes that limit frequencies in your signals.

A high frequency shirt, if we want to resample to smaller image, you will see all kinds of aliasing effects on the shirt (watering)



##### Media Representations

- Audio Signals – Time Varying Signals (amp @ t) 
- Images – 2D Signal (color @ x, y) 
- Video Signals – 3D Signals (color @ x, y, t) 
- Graphics
  - Inherently Digital 
  - 2D graphics objects 
  - 3D graphical objects

###### Video Signals 

- Video is obtained via raster scanning, which transforms a 3-D color signal (function of x, y and t) into a one dimensional signal for transmission. 
- Scanning is a sampling operation: 
  - Samples in time: Frames 
  - Samples along y (vertical direction): Lines 
  - Samples along x (horizontal direction): Pixels 
- Scanning is done using two formats. 
  - Progressive Scanning 
  - Interlaced Scanning

TV Signal

