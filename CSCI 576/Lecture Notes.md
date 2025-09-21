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