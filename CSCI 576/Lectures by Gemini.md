## CSCI 576: Lecture 2 - Data Acquisition & Media Basics

### 1. The Multimedia Pipeline & Acquisition

* **End-to-End Pipeline:** The lecture aims to understand the full multimedia pipeline: **Acquisition** $\rightarrow$ **Authoring** $\rightarrow$ **Encoding/Compression** $\rightarrow$ **Streaming** $\rightarrow$ **Consumption**.
* **Core Concepts:** Multimedia is **digital** (represented by 1s and 0s), which allows different media types (video, audio, graphics) to be combined into interactive content. It is also **voluminous**, which necessitates compression.
* **Goal of Acquisition:** To take the analog, physical world and "recreate the same sensation and interactivity in a digital medium".
* **Why Acquisition is Key:** This first step is core to system design because it defines two critical factors:
    1.  **Quality** of the data captured.
    2.  **Quantity** of the data captured.

---

### 2. Analog to Digital Conversion (ADC)

The process of converting a continuous analog signal into a discrete digital signal is achieved by two main steps: **Sampling** and **Quantization**.

#### Sampling (Discretizing Time)

* **Definition:** The process of converting a continuous-time signal (e.g., $x(t)$) into a discrete-time signal ($x_s(n)$) by taking "snapshots" at specific time intervals.
* **Key Parameters:**
    * **$T$ (Sampling Period):** The time interval between samples.
    * **$f_s$ (Sampling Frequency/Rate):** The number of samples taken per second, calculated as $f_s = 1/T$.
* **Trade-off:**
    * **High $f_s$ (Low $T$):** More data (bad for storage/compression), but higher fidelity and less risk of quality loss. Can lead to redundant data if *too* high.
    * **Low $f_s$ (High $T$):** Less data (good for storage), but high risk of losing signal quality.

#### Quantization (Discretizing Amplitude)

* **Definition:** The process of converting a continuous-amplitude sample ($x_s(n)$) into a discrete value ($x_q(n)$) represented by a fixed number of bits. This is essentially a rounding function.
* **Key Parameter:**
    * **$B$ (Bit Depth):** The number of bits used to represent each sample. This determines the number of available levels (e.g., 3 bits = $2^3 = 8$ levels).
* **Trade-off:**
    * **High $B$:** More data (bad), but more quantization levels, smaller intervals, and thus **less error** and higher precision.
    * **Low $B$:** Less data (good), but fewer levels, larger intervals, and thus **more error** and lower quality.
* **Quantization Error:**
    * An error is **always** introduced because the true signal value rarely falls exactly on a predefined level.
    * By rounding to the *nearest* level (as opposed to flooring or ceiling), the **maximum error** is minimized to **half the interval size**.

#### Bitrate

* **Definition:** The total amount of data (bits) required per unit of time (second).
* **Formula:** **Bitrate = (Bits / Sample) $\times$ (Samples / Second)**.
* This is the product of quantization and sampling: **Bitrate = $B \times f_s$**.
* **Examples**:
    * **Speech:** 8 bits/sample $\times$ 8,000 samples/sec (8 kHz) = 64,000 bps (64 kbps)
    * **Audio CD (Mono):** 16 bits/sample $\times$ 44,100 samples/sec (44.1 kHz) = 705,600 bps (706 kbps)

---

### 3. The Science of Sampling

#### LTI (Linear Time-Invariant) Systems

* Sampling and quantization principles rely on the assumption that the systems (e.g., sensors, circuits) are **LTI**.
* **Linearity:** A system is linear if $f(x_1 + x_2) = f(x_1) + f(x_2)$.
    * $y = kx$ is **linear**.
    * $y = x^2$ is **NOT linear**.
    * $y = x + a$ (a constant offset) is **NOT linear**.
* **Time Invariance:** The system's output depends *only* on the input at that time, not on past or future inputs (i.e., it has no memory).

#### Nyquist-Shannon Sampling Theorem

This theorem answers the question: "What should the sampling frequency ($f_s$) be?".

* **The Theorem:** To perfectly reconstruct an analog signal, you must sample at a frequency ($f_s$) that is **at least twice the maximal frequency ($f_{max}$)** present in the signal.
* **Formula:** **$f_s \geq 2 \times f_{max}$**.
* **Finding $f_{max}$ (Fourier Transform):**
    * The **Fourier Transform** is a tool that breaks down any signal into the sum of its constituent sine and cosine frequencies.
    * It treats the signal as a point in a "function space," where basis functions ($\cos(i\omega t)$) are the axes and the coefficients ($b_i$) are the coordinates (amplitudes) for each frequency.
    * To find $f_{max}$, you take the Fourier Transform of the signal, look at its frequency spectrum, and find the **highest non-zero frequency**.
* **Practical $f_{max}$ (Human Perception):**
    * **Human Voice:** The larynx has a physical limit of $\approx 4$ kHz. Therefore, $f_s$ for speech is $2 \times 4 \text{ kHz} = 8$ kHz.
    * **Human Hearing:** The audible range is 20 Hz to 20 kHz. To capture everything we can hear, $f_s$ must be $\geq 2 \times 20 \text{ kHz} = 40$ kHz.
    * **CD Audio:** Uses **44.1 kHz**, which is slightly above 40 kHz to provide a "guard band" or margin for error.

#### The "Why $B$?" Question (Quantization)

* The choice of bit depth ($B$) is determined by **human perception**.
* The goal is to use *just enough* bits so that the quantization error is **imperceptible** to our eyes or ears.
* **Example:** For human voice, **8 bits** is sufficient. At 7 bits, the error is noticeable, but at 9 or 10 bits, it sounds the same as 8, so the extra bits are wasted data. High-fidelity music uses 16 bits for a wider dynamic range.

---

### 4. Aliasing (The Cost of Undersampling)

* **Definition:** Aliasing is the introduction of errors or artifacts when a signal is reconstructed from samples that were taken *below* the Nyquist rate ($f_s < 2 \times f_{max}$). The reconstructed signal has different frequencies than the original.
* **Examples:**
    * **1D (Audio):** The "aliased" signal loses its high-frequency components, sounding muffled or distorted.
    * **2D (Spatial Aliasing):**
        * **"Jaggies":** Smooth diagonal lines in an image appear as jagged steps.
        * **Moiré Patterns:** Occur when sampling a high-frequency pattern (like a checkered shirt) with a display or sensor that has a lower sampling frequency (pixel grid).
    * **3D (Temporal Aliasing):**
        * **Wagon Wheel Effect:** A classic example where a wheel (signal) spinning at a high RPM (frequency) is filmed by a camera (sampler) with a fixed frame rate. If the wheel's rotation frequency exceeds half the frame rate, it can appear to spin slowly, stop, or even spin backward.
        * **Helicopter Blades:** Can appear to be frozen in place if the blade's rotation frequency (or a multiple of it) exactly matches the camera's shutter rate (sampling frequency).

#### Anti-Aliasing & Filters

* Aliasing can also be introduced *after* capture, during processing, such as **resampling** or **subsampling** (resizing an image). Throwing away pixels (e.g., every other row/column) is effectively lowering the sampling frequency, which can cause aliasing in high-frequency areas (like textures or patterns).
* **Solution (Anti-Aliasing):** Use a **filter** to remove the aliasing artifacts.
* **Process:**
    1.  Apply a **low-pass filter** (e.g., averaging or blurring) to the *original, high-resolution* signal.
    2.  This filter removes the high frequencies that would cause aliasing.
    3.  **Then**, subsample (resize) the blurred image.
* **Result:** The final image is slightly softer/blurrier, but it is free of the noisy aliasing artifacts.

---

### 5. Video Signal Basics & Evolution

The history of analog video created standards that are still relevant in digital media today.

#### Problem 1: Synchronization
* **Challenge:** How to synchronize the capture frame rate (at the studio) and the display frame rate (at the home TV) without digital clocks?
* **Solution:** Use the **AC power grid frequency** as a universal clock.
    * **North America (NTSC):** 60 Hz power $\rightarrow$ 30 frames/second (fps) video.
    * **Europe/Asia (PAL):** 50 Hz power $\rightarrow$ 25 frames/second (fps) video.

#### Problem 2: Flicker
* **Challenge:** On old phosphor (CRT) screens, the image was drawn scanline by scanline. By the time the electron gun reached the bottom, the phosphor at the top had started to decay, causing a noticeable **flicker**.
* **Solution:** **Interlaced Scanning**.
    * Instead of scanning lines 1, 2, 3, 4... (called **Progressive Scan**).
    * The scanner captures/draws all **odd lines** (1, 3, 5...) as an "odd field," then scans all **even lines** (2, 4, 6...) as an "even field".
    * This breaks 30 fps into 60 *fields* per second. This higher refresh rate minimized the perceived decay and reduced flicker.

#### Problem 3: The Introduction of Color
* **Challenge 1 (Bandwidth):** A color signal (R, G, B) required **3x the bandwidth** of the existing Black & White (B&W) signal.
* **Challenge 2 (Compatibility):** The new color broadcasts had to be viewable on *both* new color TVs and existing B&W TVs.
* **Solution:** **YUV Color Space** + **Color Subsampling**.
    * **YUV Space:** Convert RGB into YUV.
        * **Y = Luminance** (Luma): The brightness/intensity information (this is the B&W signal).
        * **U, V = Chrominance** (Chroma): The color-difference information.
    * **How this Solved the Problems:**
        1.  **Compatibility:** B&W TVs could just receive the YUV signal and *display the Y channel*, ignoring U and V. Color TVs would receive YUV and convert it back to RGB for display.
        2.  **Bandwidth:** Based on the perceptual fact that human eyes are **far more sensitive to luminance (Y) than to chrominance (UV)** (due to having $\approx$100M rods (luma) vs. $\approx$10M cones (color)), engineers decided to **throw away color information** to save space. This is **Color Subsampling**.
* **Color Subsampling Schemes:**
    * **YUV 4:4:4:** (No subsampling). For every 4 pixels, you keep 4 Y samples, 4 U samples, and 4 V samples.
        * $(4*8+4*8+4*8) / 4 = 24$
        * **Average: 24 bits/pixel**.
    * **YUV 4:2:2:** For every 4 pixels, you keep 4 Y samples, 2 U samples, and 2 V samples (throws away half the color).
        * $(4*8+2*8+2*8)/4 = 64 / 4 = 16$
        * **Average: 16 bits/pixel** (33% bandwidth saving).
    * **YUV 4:2:0 / 4:1:1:** For every 4 pixels, you keep 4 Y samples, 1 U sample, and 1 V sample (throws away 75% of the color).
        * $(4*8+2*8 + 0*8)/4 = 48/4 = 12$
        * **Average: 12 bits/pixel** (50% bandwidth saving).

#### Problem 4: Aspect Ratios
* **Challenge:** Media is created in various aspect ratios (e.g., 4:3, 16:9, Cinemascope 47:20). Displaying content from one aspect ratio on a screen of another causes problems.
* **Solutions:**
    * **Stretching:** Distorts the image. `Not good effects`
    * **Letterboxing:** Adds black bars; maintains aspect ratio but wastes screen space.
    * **Seam Carving (Content-Aware Resizing):** A modern, intelligent solution. It identifies the "least important" connected path of pixels (a "seam") in an image (e.g., a path through the sky or background) and removes it. It repeats this process, removing low-energy seams to resize the image without distorting the important content (like faces). It can also insert seams to enlarge an image.

---

### 6. Assignment 1 Overview

* **Part 1:** Theory questions on YUV subsampling, quantization, and temporal aliasing.
* **Part 2:** Programming assignment (C, C++, or Java only).
* **Goal:** Implement an image quantization program that takes an input image and 6 parameters.
* **Parameters:** `(input_image, color_mode, quant_mode, q1, q2, q3)`.
* **`color_mode`:** Process in **RGB** (`1`) or **YUV** (`2`) space. (A matrix for RGB $\leftrightarrow$ YUV conversion is provided).
* **`quant_mode`:**
    * `1`: **Uniform Quantization**. Divide the 0-255 range into $2^q$ equal-sized regions.
    * `2`: **Smart Quantization**. Devise a non-uniform method (e.g., based on histograms) to place quantization levels more intelligently where most pixel values are concentrated, to reduce error.
* **Analysis:** For a fixed total number of bits $N = q1+q2+q3$, run experiments to find the optimal distribution of bits between the three channels (e.g., for $N=6$, is 2,2,2 better or is 4,1,1 better?) that minimizes the total error.



## CSCI 576: Lecture 3 - Color Theory

### 1. Assignment 1 Clarifications

* **Data Types:** The provided code reads pixel data as `unsigned char` (C++) or `byte` (Java). For internal processing, like converting RGB to YUV, you can use whatever data type you want (e.g., `float`). You just need to convert it back to the standard format for display.
    * Be mindful of your data type conventions. An `unsigned char` (0 to 255) behaves differently than a `char` (-128 to 127). The best practice is to stick with one convention.
* **Grading:** Grading is primarily based on the **results and output** of your code. While good code is a factor, the main focus is the correctness of the output.
* **Analysis Goal:** The core idea is to see how you would distribute a **fixed bit budget** (e.g., 6 bits total instead of 24) among the three color channels. The analysis should explore if trends emerge based on the color space (RGB vs. YUV) or image content.

---

### 2. The Problem of Color 🎨

* **Goal:** To achieve **color consistency** across the entire multimedia pipeline.
* **The Challenge:** A color captured by a camera (e.g., Sony) must look the *same* when displayed on a projector (e.g., Hitachi), a TV (e.g., Sony), or a printer (e.g., Epson). This requires calibration and a deep understanding of what "color" is.
* **Physics of Color:**
    * A light source emits a ray of light, which is composed of multiple **wavelengths** (frequencies).
    * This light hits an object, which **absorbs** certain wavelengths and **reflects** others based on its surface properties.
    * The reflected light (a spectrum) enters your eye.
* **Color is Perception, Not Reality:**
    * The ray of light itself has **no color**.
    * **Color is a sensation that exists only in your mind**. It is the brain's interpretation of a light spectrum.
    * The visible spectrum for humans is roughly **400nm (violet) to 780nm (red)**. Other frequencies (like X-rays or UV) do not trigger a color sensation.

---

### 3. The Human Visual System (HVS) & Trichromaticity

The key to solving the engineering problem of color lies in understanding how our eyes work.

* **Sensors in the Eye:** The retina contains two types of sensors:
    1.  **Rods:** $\approx$100-110 million; sense **intensity (luminance/brightness)**.
    2.  **Cones:** $\approx$6-10 million; sense **color**.
* **Trichromatic Theory:** We have **three different types of cones** ($C_1, C_2, C_3$). (This was theorized by Thomas Young and Hermann von Helmholtz and later experimentally proven by James Clerk Maxwell).
* **Cone Sensitivity ($S_1, S_2, S_3$):** Each cone type is sensitive to different, overlapping parts of the visible spectrum (short, medium, and long wavelengths).

#### Metamerism: The Breakthrough 💡

* **The Problem:** An incoming light ray is a full **spectrum** ($f$), which is a continuous function of energy at infinite wavelengths. Capturing and reproducing this *exact* spectrum is an impossible engineering challenge.
* **The Solution (How the Eye Works):** The eye does *not* send the full spectrum to the brain. It sends only **three values** ($C_1, C_2, C_3$).
* Each value is the integral (or, in discrete terms, the summation) of the incoming spectrum ($f$) multiplied by that cone's sensitivity curve ($S$).
* **Formula (Discrete):** $[C_1, C_2, C_3]^T = \mathbf{S}^T \mathbf{f}$.
* **Metamers:** This is a **many-to-one mapping**. Many completely different-looking spectra ($f_1, f_2, ...$) can all produce the *exact same* $C_1, C_2, C_3$ values. These different spectra that look like the "same color" are called **metamers**.
* **New Engineering Goal:** We **do not** need to make the captured spectrum ($f$) equal to the displayed spectrum ($g$). We **only** need to ensure their *color sensations* match: $\mathbf{S}^T \mathbf{f} = \mathbf{S}^T \mathbf{g}$.

---

### 4. Device Calibration & Standardization

To make any camera work with any display, we must standardize the capture and display processes to mimic the HVS.

#### Step 1: Model Device Capture (Camera) 📸

* A camera sensor mimics the eye by using **three different filters** ($M_1, M_2, M_3$).
* An incoming spectrum $f$ passes through these three filters, producing three distinct values ($A_1, A_2, A_3$) for that pixel. These are the **RGB values**.
* **Formula:** $[A_1, A_2, A_3]^T = \mathbf{M}^T \mathbf{f}$.

#### Step 2: Model Device Display (TV/Projector) 📺

* A display generates color using **three "primaries"** ($P_1, P_2, P_3$), such as three electron guns or LEDs.
* It applies **voltage gains** ($V_1, V_2, V_3$) to these primaries to create a new, combined spectrum $G$ that the eye sees.
* **Formula:** $G = P_1 V_1 + P_2 V_2 + P_3 V_3$.

#### Step 3: The CIE Color Matching Experiment 🔬

* **Goal:** Connect capture and display by standardizing $M$ and $P$.
* **The Process:**
    1.  A standards body (like the International Color Commission) **fixes the $P$ primaries** ($P_1, P_2, P_3$) for all display manufacturers (Sony, Hitachi, etc.).
    2.  They run an experiment to **solve for the $M$ filters** ($M_1, M_2, M_3$).
    3.  A "standard observer" is shown a target spectrum $f$.
    4.  The observer adjusts three dials ($V_1, V_2, V_3$, which are our $A$ values) on a device with the fixed $P$ primaries until the generated spectrum $g$ *perceptually matches* the color of $f$.
    5.  At this point, we know $f$ (measured with a spectrometer) and $A$ (the dial readings). We can now solve the linear equation $A = M^Tf$ for the unknown $M$ filters.
    6.  This $M$ matrix is given to all camera manufacturers.

* **Result:** A captured $A$ value (RGB) from any standard camera will, when fed as the $V$ value to any standard display, produce a spectrum $g$ that has the same color sensation as the original spectrum $f$.

---

### 5. Color Spaces & Chromaticity

* **RGB Primaries:** The $M$ filters solved for in the experiment are the **RGB primaries**. One filter ($M_3$, blue) actually has a *negative* response curve, which is physically impossible to build.
* **XYZ Color Space:** Because of the negativity, RGB is transformed into a standard, all-positive "imaginary" primary space called **XYZ**. This space is the foundation of all color science and can encode all visible colors.
* **Color Gamut:** The 3D volume of all colors a device can produce or the eye can see.
* **Chromaticity Diagram (2D Projection):**
    * To visualize just the **chroma** (hue and saturation) without luminance, the 3D XYZ space is projected onto a 2D plane ($x+y+z=1$).
    * This creates the famous **CIE 1931 "horseshoe" diagram**. The area inside the horseshoe represents all colors humans can perceive.
    * A device's $P$ primaries form a **triangle** on this diagram. The device can *only* reproduce colors *inside* this triangle (this is its gamut).
    * **Why is Brown not on the chart?** Brown is a 3D color concept; it is simply a **dark orange**. It projects onto the same 2D chromaticity coordinate as orange.

---

### 6. Additive vs. Subtractive Color 💡

* **Additive (Light) - RGB:** Used for displays (TVs, projectors) that *emit* light.
    * Blue Light (0, 0, 1) + Yellow Light (1, 1, 0) = **White Light** (1, 1, 1).
* **Subtractive (Pigment) - CMY(K):** Used for printing. Pigments *absorb* (subtract) light from a white source (paper).
    * $C = 1-R$ (Cyan absorbs Red)
    * $M = 1-G$ (Magenta absorbs Green)
    * $Y = 1-B$ (Yellow absorbs Blue)
    * **Blue Pigment + Yellow Pigment:**
        1.  **Blue Pigment** *absorbs* Red and *reflects* Green and Blue.
        2.  **Yellow Pigment** *absorbs* Blue and *reflects* Red and Green.
        3.  When mixed, the Yellow Pigment *absorbs* the Blue reflection from the blue pigment. The Blue Pigment *absorbs* the Red reflection from the yellow pigment.
        4.  The *only* wavelength that **both** pigments reflect (and neither absorbs) is **Green**. That is why the mix looks green.

---

### 7. Practical Device Implementations

* **High-End Cameras (3-CCD):** Use three separate sensors, one for R, one for G, and one for B, for *every single pixel*. This gives perfect color but is expensive and results in lower spatial resolution.
* **Consumer Cameras (1-CCD) & the Bayer Pattern:**
    * To save cost and increase resolution, most cameras use a single sensor with a **Bayer Pattern** (a mosaic of filters).
    * Each pixel location *only* captures one color value: R *or* G *or* B (typically in a GRGB pattern).
    * The missing two color values are **interpolated** (filtered) from their neighbors in post-processing.
    * This is cheaper and allows higher spatial resolution, but can cause **color artifacts** ("wishy-washy" effects) at crisp edges.
* **Gamma Correction:**
    * A correction applied to account for the non-linear response of old phosphor (CRT) screens.
    * The input voltage was passed through an amplifier (e.g., $V_{out} = V_{in}^{1/2.2}$) to ensure the brightness displayed was perceptually linear. Modern LED/LCDs use lookup tables instead.



## CSCI 576: Lecture 4 - Compression Fundamentals

### 1. Assignment 1: Dynamic Quantization Tip

The professor provided a key hint for implementing "smart" or dynamic quantization (mode 2):

* **The Problem with Uniform Quantization:** If you use 4 uniform buckets (2 bits) but 75% of all pixel values fall into just *one* of those buckets, you are wasting the other 3 buckets, and the 75% region has a large error.
* **The Goal:** The ideal "smart" quantization algorithm adjusts the bucket boundaries so that each bucket contains (roughly) the **same number of pixels**.
* **Example:** For 4 buckets (2 bits), if you have 100 total pixels with 75 in one region and 25 in another, you should:
    1.  Divide the region with 75 pixels into **3 buckets** (25 pixels each).
    2.  Use the 4th bucket for the region with 25 pixels.
    3.  This results in 4 non-uniform buckets, each representing 25 pixels, which minimizes the error.
* **The Hard Part:** The challenge is finding the *boundaries* for these new, non-uniform buckets.

---

### 2. The Need for Compression 📦

Raw multimedia data is massive, far exceeding practical storage or streaming capabilities.

* **Example:** A high-definition (HDTV) signal requires a massive amount of data.
    * **Resolution:** 1920 x 1080 pixels
    * **Bit Depth:** $\approx$ 12 bits per pixel
    * **Frame Rate:** 29.97 frames per second
    * **Total Bitrate:** (1920 $\times$ 1080 $\times$ 12 $\times$ 29.97) $\approx$ **750 Mbps**.
* This bitrate is too large for most current networks, demonstrating the critical need for compression.

---

### 3. Information Theory 🧠

Compression is rooted in the "Information Theory" developed by **Claude Shannon**. His work split the problem into two parts:

1.  **Channel Coding (Reliability):** How to transmit information *reliably* across a noisy channel (e.g., by sending redundant bits to correct errors).
2.  **Source Coding (Efficiency):** How to transmit information *efficiently*. This is **compression**.

#### Data vs. Information

* **Data:** Raw bits. A stream of 80,000 bits is just data; it's meaningless without context.
* **Information:** Data that is *organized*. If you know those 80,000 bits are organized as 10,000 symbols of 8 bits each, and those are organized as a 100x100 matrix, you now have the *information* that this is an image.

#### Entropy ($H$)

* **Vocabulary:** The set of unique symbols a source can produce (e.g., a source with 4 symbols S1, S2, S3, S4).
* **The Key Insight:** Instead of using the same number of bits for every symbol (e.g., 2 bits for S1, S2, S3, S4), we can achiexve compression by assigning **fewer bits to more frequent symbols** and **more bits to less frequent symbols**.
    * For S = {S1, S2, S3, S4}
        * $S1 = 00, S2 =11, S3 =10, S4= 10$
        * $S1 = 1, S2 = 001, S3 = 01, S4 = 000$

* **Entropy ($H$):** The theoretical **lowest possible limit** for the average number of bits needed to represent one symbol from a source.
    * **Formula:** $H = -\sum p_i \log_2(p_i) = \sum p_i\log(1/p_i)$ (where $p_i$ is the probability of symbol $Si$).
* **Entropy and Randomness:**
    * **High Entropy:** Occurs when the source is highly **random** (all symbols are equally probable). This is the *worst case* for compression.
    * **Low Entropy:** Occurs when the source is highly **structured** or *biased* (some symbols are very probable, others are not). This has the most potential for compression.
    * **The Golden Rule:** Our world is **not random; it is structured**. Compression algorithms work by finding and exploiting this structure.

---

### 4. Lossless vs. Lossy Compression

All compression algorithms fall into two categories:

| Feature | Lossless Compression | Lossy Compression |
| :--- | :--- | :--- |
| **Goal** | Information is **perfectly preserved**. The decoded file is identical to the original. | Throws away data. The decoded file is *not* identical to the original. |
| **Bitrate** | Produces a **Variable Bitrate (VBR)**. A "difficult" (random) section will cause the bitrate to spike. | Can achieve a **Constant Bitrate (CBR)**, which is ideal for streaming. |
| **Compression** | Not guaranteed                                               | guaranteed                                                   |
| **Challenge** | Hard to design algorithms that can reach the theoretical entropy limit. | Hard to design because it requires a deep understanding of **human perception** to know what data to throw away without affecting *perceived* quality. `Lossy is harder than lossless` |

---

### 5. Lossless Compression Techniques

#### Repetition Removal (Run-Length Encoding - RLE)

* **How it works:** Replaces consecutive runs of the *same* symbol with a single symbol and a count.
* **Example:** `S = {A, B}` `AAAAABBBBAA` $\rightarrow$ `(A, 5), (B, 4), (A, 2)`
* **Best for:** Low-entropy (structured) sources with long repetitions. Fails on random data (e.g., `ABABAB` becomes `(A,1)(B,1)(A,1)(B,1)...`, doubling the size).

#### Dictionary-Based (Lempel-Ziv-Welch - LZW)

<img src="Lectures by Gemini.assets/image-20251104233316464.png" alt="image-20251104233316464" style="zoom:50%;" />

* **How it works:** Dynamically builds a "dictionary" (or codebook) of repeating *patterns* or strings. It then replaces occurrences of that pattern with its shorter dictionary index.
  * Example: S = {A, B}
  * a, b, b, a, a, b, b, a, a, b, a, b, b, a,....
    * a = 0, b = 1

  * 0, 1, b, a,...
    * ab = 2, bb = 3, ba = 4, aa = 5
  * 0, 1, 1, 0, 
    * abb = 6, bba = 7, 
  * 0, 1, 1, 0, 2, 4, 2, 6

* **Streaming:** The dictionary does *not* need to be sent first. The decoder can perfectly regenerate the *exact same* dictionary on its end as it processes the incoming encoded stream.
* **Used in:** **ZIP** and **GIF**.

#### Statistical (Huffman Coding)

<img src="Lectures by Gemini.assets/image-20251104233242440.png" alt="image-20251104233242440" style="zoom:80%;" />

* **How it works:** Builds a binary tree from the bottom up based on symbol probabilities.
    1.  It repeatedly combines the two *least probable* symbols into a new node.
    2.  This ensures that the **most frequent** symbols (like H, G, F) are *shallow* (close to the root) and get the **shortest codes**.
    3.  The **least frequent** symbols (like A, B) are *deepest* in the tree and get the **longest codes**.
* **Key Property:** It creates a **prefix code** (no code is a prefix of another code), which makes it uniquely decodable.
* **Optimality:** Huffman is good, but **not always optimal**. It only achieves the perfect entropy limit ($L_{avg} = H$) if all symbol probabilities are negative powers of two (e.g., 1/2, 1/4, 1/8...).

#### Arithmetic Coding

<img src="Lectures by Gemini.assets/image-20251104233345511.png" alt="image-20251104233345511" style="zoom:50%;" />

* **How it works:** Maps an *entire* string of symbols to a single, high-precision floating-point number between 0 and 1. It recursively divides the 0-1 range based on symbol probabilities.
* **Performance:** On a practical basis, it performs **better than Huffman** (gets closer to the true entropy $H$) but is more computationally expensive.

---

### 6. Lossy Compression Techniques

#### Differential PCM (DPCM) 📉

<img src="Lectures by Gemini.assets/Screenshot 2025-11-04 at 11.34.52 PM.png" alt="Screenshot 2025-11-04 at 11.34.52 PM" style="zoom:50%;" />

* **How it works:** A **prediction-based** method. It assumes the next sample will be similar to the previous one.
    1.  **Predict** the next sample (e.g., predict it's the same as the last one).
    2.  Compute the **difference (error)** between the *actual* sample and the *predicted* sample.
    3.  **Transmit only the error**.
* **Why is it Lossy?** The *differences* have a much smaller range (lower entropy) than the original signal. This stream of differences can then be **re-quantized** with fewer bits (e.g., 3 bits instead of 8). This re-quantization is the lossy step.
* **Open-Loop DPCM (Bad):** The decoder's quantization error from the first sample ($E_1$) gets added to the error from the second sample ($E_2$), and so on. The errors **accumulate** ($E_{total} = E_1+E_2+E_3...$), causing massive distortion.
* **Closed-Loop DPCM (Good):** The *encoder* simulates the decoder. To calculate the *next* difference, it uses the *previous quantized value* (the same one the decoder has) instead of the original value. This prevents the errors from accumulating.

#### Vector Quantization (VQ)

* **How it works:** Instead of quantizing one sample (a scalar) at a time, it quantizes a "vector" (a group of samples) at a time.
    1.  A "codebook" is created containing a small set of representative vectors (e.g., 4 common 2x2 pixel blocks).
    2.  The encoder takes an input vector (e.g., a 2x2 block from the image).
    3.  It finds the *closest matching* vector from the codebook.
    4.  It transmits **only the index** of that matching vector (e.g., 2 bits to represent 1 of the 4 codebook vectors).

#### Transform Coding (Frequency Domain) 🌌

* This is the most powerful lossy technique and the basis for **JPEG** and **MPEG**.
* **How it works:**
    1.  **Transform:** A mathematical transform (like the **Discrete Cosine Transform, or DCT**) is applied to a block of pixels, converting the signal from the spatial (pixel) domain to the **frequency domain**.
    2.  **Exploit Structure:** Because our world is structured, the transform "compacts" most of the signal's energy into just a few low-frequency coefficients. Most of the high-frequency coefficients become zero or near-zero.
    3.  **Exploit Perception:** The *key* step. Human perception is less sensitive to high-frequency changes. We can aggressively **quantize** (throw away) these high-frequency coefficients without the viewer noticing.
    4.  **Inverse Transform:** The decoder uses an inverse transform (IDCT) to convert the quantized frequencies back into pixels.
* **The Loss:** The transform itself (DCT/IDCT) is lossless. The information is lost *only* during the perceptual **quantization** step in the middle.



# Lecture 5 - 9/29/2025 - Image Compression

## 📝 Assignment 1 & Exam Notes

### Assignment 1 Grading

* **Submissions:** The latest submitted version will be graded.
* **Typo Correction:** A typo in the YUV to RGB conversion matrix (specifically, the value `0.147` was mistyped as `0.417`) was announced. Graders will check outputs for *both* values, and you will receive full marks as long as your output is correct for the value you used.
* **Theory Questions:** The "relevant portion" (theory questions) will not be graded, but solutions will be provided for you to check your work.
* **Programming Tests:** Your submitted code will be compiled and run against several (5-6) test inputs, which are typically generated gradients, not natural images. As long as the output is qualitatively similar, you will get full credit.
* **Error Metric:** For the analysis, as long as you used a correct error metric (like **sum of absolute differences** or **sum of squared differences**) and *not* a simple difference (which would cancel out), your values will be accepted. The graders are more interested in the **pattern** you observed in the results.

### Exam Format

* **No Notes:** The exam will **not** allow any books, notes, or formula sheets.
* **Calculators:** Calculators **are** allowed.
* **Structure:** The exam will likely have three sections:
    1.  **Short Answer:** Easy questions that require a logical, two-sentence answer.
    2.  **Computation:** A section requiring you to perform calculations.
    3.  **Challenging:** A final, more difficult question requiring deeper thought.

---

## 🖼️ Image Compression Overview

This lecture begins the section on media-specific compression, starting with images.

### Image Types

* Images can be grayscale or color. Color images typically have three channels (like **RGB** or **YUV**).
* Bit depth can vary (8-bit, 12-bit, 16-bit) depending on the application (e.g., consumer vs. professional film).
* **Alpha Channel:** A fourth channel is sometimes included to represent **opacity**.
    * This is crucial for **compositing** and **blending** foreground and background images.
    * It's typically an 8-bit value, not just binary (0 or 1). This allows for partial transparency at object boundaries, which creates a more natural blend by simulating light diffraction.

### The Goal of Compression: Removing Redundancy

The core principle of compression is to **remove redundancy**. Images have a lot of structure and are not random. Redundancy can be found in:

* **Spatial Domain (Pixels):** Images often have large, flat areas (like a blue sky) or slowly changing gradients where pixels are highly correlated with their neighbors.
* **Spectral Domain (Frequencies):** This is where we analyze the *rate of change* in an image. Perception-based compression works in this domain.

---

## 🔁 The General Lossy Compression Pipeline

Most modern lossy compression standards (like JPEG) follow this general pipeline:

1.  **Transform (T):** The image $f(x,y)$ is moved from the spatial (pixel) domain to a **transform domain** $F(u,v)$.
    * **Why?** Because real-world signals are structured, their representation in the frequency domain has **less entropy** (i.e., fewer non-zero values are needed to represent the same signal).
    * This transform (e.g., DCT) is mathematically **lossless** and **invertible** ($T^{-1}$).
2.  **Quantization (Q):** This is the **main lossy step** and the **hardest part** to design.
    * Based on human perception, we **"quantize"** the transformed coefficients.
    * This means we assign *more* bits (high precision) to "important" frequencies (usually low frequencies) and *fewer* bits (or zero bits) to "unimportant" frequencies (usually high frequencies).
3.  **Entropy Coding:** The resulting quantized coefficients (which now contain many zeros) are compressed using a **lossless statistical** method (like Huffman coding) to create the final, small bitstream.

The decoder simply reverses this process: Entropy Decoding $\rightarrow$ Inverse Quantization ($Q^{-1}$) $\rightarrow$ Inverse Transform ($T^{-1}$) to get the reconstructed image, $f\_hat(x,y)$.

---

## 🔣 Fourier & The Transform Domain

The Discrete Cosine Transform (DCT) is a relative of the Fourier Transform. It's a way of representing a signal in the frequency domain.

* **Vector Analogy:** Think of a 3D vector $\vec{v}$. It can be described as coordinates ($x,y,z$) multiplied by standard basis vectors ($\mathbf{i}, \mathbf{j}, \mathbf{k}$).
    * $\vec{v} = x\mathbf{i} + y\mathbf{j} + z\mathbf{k}$
* **Function Analogy:** The Fourier/DCT transform does the same for a function (like a signal or an image block) $f(t)$. It's represented by **coefficients** ($b_0, b_1, ...$) multiplied by standard **basis functions** (cosine waves of different frequencies).
    * $f(t) = b_0\cos(0\omega t) + b_1\cos(1\omega t) + b_2\cos(2\omega t) + ...$
* **The Compression Insight:** A complex-looking *structured* signal $f(t)$ can be represented by just a **few non-zero coefficients** ($b_i$). A purely *random* (noisy) signal would require *all* coefficients to be present.
* 2D Dimension: $f(xy) = \sum_{i = 0}^n \sum_{j=0}^n b_{ij}\cos i \omega x \cdot \cos j \omega y$

---

## 📸 The JPEG Pipeline Explained

<img src="Lectures by Gemini.assets/image.png" alt="image" style="zoom:67%;" />

JPEG (Joint Photographic Experts Group) is a DCT-based lossy standard. Here is the exact encoding process:

1. **Color Space Conversion:** The input RGB image is converted to **YCrCb** (or YUV). This separates luminance (Y, brightness) from chrominance (CrCb, color).

2. **Chroma Subsampling:** Because human perception is less sensitive to color detail than brightness, we "subsample" the color channels (e.g., **4:2:0**), keeping only 1/4 of the Cr and Cb samples while keeping all of the Y samples.

3. **Blocking:** Each channel is divided into **8x8 pixel blocks**. (This was an empirical choice to maximize local redundancy on computers of the mid-1990s).

4.  **Apply DCT:** A 2D DCT is applied to *each* 8x8 block, converting the 64 pixel values into **64 frequency coefficients**.
    * The top-left coefficient (0,0) is the **DC coefficient** (the average brightness of the block).
    * The other 63 are **AC coefficients** (representing frequencies from low to high).
    
5.  **Quantization:** This is the primary lossy step. Each of the 64 DCT coefficients is divided by a corresponding value from a standard 8x8 **Quantization Table** and rounded.
    
    * This table is designed based on perception: it has **small numbers in the top-left** (preserving important low frequencies) and **large numbers in the bottom-right** (aggressively quantizing, or zeroing-out, unimportant high frequencies).
    
      * <img src="Lectures by Gemini.assets/image-2414155.png" alt="image" style="zoom:80%;" />
    
    * The **"Quality" slider** (0-100) in image editors is just a **multiplier for this table**. Low quality = higher multiplier = more quantization.
    
      `after this step, we are done compressing. The rest is use stats to figure out how to use least space to save this`
    
6. **Entropy Coding (DC):** The quantized DC coefficient is encoded using **DPCM** (Differential Pulse Code Modulation). This means we store the *difference* between the current block's DC value and the *previous* block's DC value, which is more efficient.

7.  **Entropy Coding (AC):**
    
    * **Zig-Zag Scan:** The 63 AC coefficients are read in a **zig-zag order**. This is done because quantization created many zeros, and this scan pattern groups all the zeros together at the *end* of the stream.
    * **RLE:** A special Run-Length Encoding is applied, creating tuples of `<RUN_LENGTH, SIZE>,<AMPLITUDE>`.
        * `RUN_LENGTH`: Number of *zeros* before this non-zero value.
        * `AMPLITUDE`: The actual non-zero value (e.g., -2, -1).
        * `SIZE`: The *category* or number of bits needed to represent the AMPLITUDE.
    * **Prefix/Non-Prefix Trick:** The `(RUN_LENGTH, SIZE)` pair is encoded using a **prefix code** (like Huffman). This code tells the decoder *exactly* how many (non-prefix) bits to read next for the `AMPLITUDE`. This clever mix is more efficient than using one giant prefix table for all values.
    * **EOB:** An "End of Block" marker is placed after the last non-zero coefficient, saving space by not encoding all the trailing zeros.
    
    ###### Entropy Coding Example
    
    <img src="Lectures by Gemini.assets/image0.jpg" alt="image0" style="zoom:67%;" />
    
8.  **Bitstream:** The resulting codes are packed into the final bitstream.

---

## 📊 JPEG Modes, Artifacts, and JPEG 2000

### Progressive JPEG

The baseline JPEG mode described above loads the image block-by-block, scanline by scanline. For large images on the web, this is a poor user experience. **Progressive JPEG** modes send the data in multiple passes:

1.  **Spectral Selection:** Sends all DC coefficients first (a blurry, blocky image), then a pass for the first few AC coefficients, then the next, refining the image in passes.
2.  **Successive Bit Approximation:** Sends the Most Significant Bit (MSB) of *all* coefficients first, then a pass for the next bit, and so on.
3.  **Hierarchical:** Creates an image *pyramid* (e.g., 512x512 $\rightarrow$ 256x256 $\rightarrow$ 128x128...). It sends the smallest 128x128 image first, then sends the "residual" (difference) data to scale it up to 256x256, and so on.

### JPEG Artifacts

* **Blocking Artifacts:** Because each 8x8 block is compressed *independently*, visible seams or "blocks" can appear at the boundaries if the quality is set too low (i.e., quantization is too high).
* **The Flaw of DCT:** The DCT assumes the frequencies it finds are present *everywhere* in the 8x8 block. It has no time/space localization, which is what causes the blocking artifacts.

### Introduction to Wavelets (JPEG 2000)

Wavelets (the basis for JPEG 2000) solve the blocking artifact problem by *not* using blocks.

* **How it works:** Instead of blocks, it uses filters to recursively split the *entire* image.
* **Process:**
    1.  Pass the image through a **Low-Pass Filter (LPF)** (which gets the "average") and a **High-Pass Filter (HPF)** (which gets the "difference" or detail).
    2.  Keep the HPF output (the details).
    3.  Take the LPF output (which is now smaller) and **recursively** feed it back into the LPF/HPF pair.
* **Example (1D):** An image with pixels `[9, 7, 3, 5]`
    * **Pass 1 (LPF):** Average(9,7) = **8**; Average(3,5) = **4**. $\rightarrow$ `[8, 4]`
    * **Pass 1 (HPF):** Difference(9,7)/2 = **1**; Difference(3,5)/2 = **-1**. $\rightarrow$ `[1, -1]`
    * **Pass 2 (LPF):** Average(8,4) = **6**.
    * **Pass 2 (HPF):** Difference(8,4)/2 = **2**.
* **Final "Wavelet" Data:** `[6, 2, 1, -1]`. This is a fully invertible, lossless representation of the original `[9, 7, 3, 5]` signal. This will be explored further in the next lecture.

<img src="Lectures by Gemini.assets/image0-2417720.jpg" alt="image0" style="zoom:67%;" />



# Lecture 6 - 10/6/2025

## Admin & Assignment 1 Feedback

* **Assignment 1 Grading:** Grading is in progress. Emails sent out with partial grades were a mistake; please wait for the final, complete grades to be released (expected by early next week).
* **Submission Policy:** The **latest version** you submitted is the one that will be graded.
* **Grading Feedback:** For any test case where you don't receive full marks, the graders will provide a specific comment, explanation, or screengrab so you can see the issue.
* **Assignment 1 Typo:**
    * There was a typo in the YUV-to-RGB conversion matrix (`-0.417` was listed instead of the correct `-0.147`).
    * **Do not worry.** The graders have the correct outputs for *both* the correct value and the incorrect typo value. As long as your program's output matches the expected result for whichever value you used, you will receive full credit.
* **Image Size Issue:** If you accidentally hard-coded the wrong image dimensions (e.g., 512x512), you will not be penalized for the entire assignment. The graders will attempt to modify the code or test with the correct dimensions.
* **Error Metric (Analysis):** As long as you used a valid error metric (like **sum of absolute differences** or **sum of squared differences**) and *not* a simple difference (which would be incorrect), your analysis will be accepted. The graders are focused on the *patterns* you observed.
* **Exam Policy:**
    * **No** notes, books, or cheat sheets are allowed.
    * **Yes,** calculators are permitted.

---

## Recap: Why JPEG Has Artifacts

The previous lecture's JPEG (DCT-based) compression works well, but its core design creates a major problem: **blocking artifacts**.

* **The Cause:** JPEG divides an image into independent **8x8 blocks**. The DCT assumes the frequencies it finds are "stationary" (present everywhere *within* that block).
* **The Flaw:** This process ignores the relationships *between* blocks. At low bitrates (high quantization), the decoded blocks don't match up at their edges, creating a visible "grid" or "blocking" effect.

---

## 🌊 Wavelets (The Core of JPEG 2000)

Wavelets solve the blocking problem by **not using blocks**. Instead, they process the *entire* signal (or image) at once by recursively filtering it.

### The 1D Wavelet Transform (Haar Wavelet)

This process recursively separates a signal into **averages (low-pass)** and **differences (high-pass)**.

1.  **Start Signal:** Imagine a 1D signal with 4 pixels: `[9, 7, 3, 5]`
2.  **Level 1 Pass:**
    * **Low-Pass (Averages):** Take the average of pairs.
        * `(9 + 7) / 2 = 8`
        * `(3 + 5) / 2 = 4`
    * **High-Pass (Differences):** Take the *difference* from the average for each pair.
        * `(9 - 7) / 2 = 1`
        * `(3 - 5) / 2 = -1`
    * **Result 1:** The signal is now `[8, 4 | 1, -1]` (Averages | Differences)
3.  **Level 2 Pass (Recursive):**
    * We are done with the "Difference" (High-Pass) part `[1, -1]`, so we set it aside.
    * We *recursively* apply the same process to the "Average" (Low-Pass) part `[8, 4]`.
    * **Low-Pass (Average):** `(8 + 4) / 2 = 6`
    * **High-Pass (Difference):** `(8 - 4) / 2 = 2`
4.  **Final Representation:** `[6 | 2 | 1, -1]`
    * `6`: The overall average (Low-Pass Level 2)
    * `2`: The difference (High-Pass Level 2)
    * `[1, -1]`: The differences (High-Pass Level 1)

This final representation `[6, 2, 1, -1]` is a **100% lossless, reversible** representation of the original `[9, 7, 3, 5]`.

### The 2D Wavelet Transform

This same process is applied to 2D images, just in two directions:

1.  **Row Pass:** Perform the 1D wavelet transform on **all rows** of the image. This results in the image being split into two halves: a Low-Pass (Averages) half on the left and a High-Pass (Differences) half on the right.
2.  **Column Pass:** Perform the 1D wavelet transform on **all columns** of the *result* from Step 1.
3.  **Result (4 Quadrants):** This creates four quadrants in the image:
    * **LL (Low-Low):** The averages of the averages. This is the "thumbnail" or most important part of the image.
    * **LH (Low-High):** Averages of rows, differences of columns (shows horizontal details).
    * **HL (High-Low):** Differences of rows, averages of columns (shows vertical details).
    * **HH (High-High):** Differences of differences (shows diagonal details).
4.  **Recursion:** The *entire* process (Steps 1-3) is then **recursively applied** to the **LL quadrant** again... and again... and again, creating a hierarchical, multi-resolution structure.


### Advantages of JPEG 2000 (Wavelets)

* **Better Compression:** The wavelet representation is more compact (lower entropy) than DCT, leading to better quality at the same bitrate.
* **No Blocking Artifacts:** Since it processes the whole image, it doesn't create blocky seams.
* **Region of Interest (ROI):** The hierarchical bitstream allows a user to request *only* the coefficients needed for a specific area (e.g., zooming in on a map) without downloading the whole image.
* **Scalability:** The *same file* can be decoded in multiple ways. A server can store one J2K file and send:
    * Just the smallest LL quadrant for a **thumbnail**.
    * The first few levels for a **medium-resolution** image.
    * The full stream for a **high-resolution** image.
    This is known as **"encode once, decode many ways."**

---

## 🎨 Dithering: Improving Perceived Quality

**Problem:** What if you must display an image with a *severely* limited color palette (e.g., only 2 colors: black and white)?

**Bad Solution: Thresholding**
If you just say `pixel < 128 = black` and `pixel > 128 = white`, a human face becomes unrecognizable blobs.

**Better Solution: Dithering**
Dithering uses the *same* 2 colors to create a *perceived* sense of grayscale by arranging the black and white dots in a specific way.

* **Halftoning:** The old newspaper method. Uses clusters of dots (small dots for light gray, big dots for dark gray). Looks artificial.
* **Ordered Dithering:** Uses a small, tiled "dithering matrix" of thresholds. It compares each pixel to the threshold in the matrix to decide if it should be black or white. This creates a more patterned, but still artificial, look.
* **Error Diffusion (Floyd-Steinberg):** The best method. It creates a natural, randomized look.
    1.  Process one pixel at a time (in scanline order).
    2.  Quantize the *current* pixel (e.g., round it to black or white).
    3.  Calculate the **quantization error** (the difference between the original pixel value and the quantized value).
    4.  **Distribute** this error to its *future, unprocessed neighbors* (to the right, bottom-left, bottom, and bottom-right).
    5.  When you get to the next pixel, you first *add* the diffused error from its neighbors, *then* you quantize it.

This process ensures that while individual pixels are wrong, the *average* intensity over any small region is correct, resulting in a high-quality perceived image.


---

## Assignment 2: DCT and Progressive Modes

The second assignment will focus on implementing the DCT-based JPEG pipeline, specifically its different delivery modes.

* **Task:** You will build a program that takes an image, quantizes it in the DCT (frequency) domain, and then *dequantizes and displays* it progressively.
* **Inputs:** `(image, quantization_level, delivery_mode, latency)`
* **Pipeline:**
    `Input Image` $\rightarrow$ `8x8 Blocks` $\rightarrow$ `DCT` $\rightarrow$ `Quantize`
    ...THEN, based on mode, you will progressively feed coefficients to the...
    `Dequantize` $\rightarrow$ `Inverse DCT (IDCT)` $\rightarrow$ `Display Block`
* **Delivery Modes:**
    1.  **Baseline:** Dequantize and display one 8x8 block at a time (the "scanline" method).
    2.  **Spectral Selection:** Send all DC coefficients first, then all AC[1] coefficients, then all AC[2], etc. (64 passes).
    3.  **Successive Approximation:** Send the Most Significant Bit (MSB) of *all* coefficients first, then the next bit of *all* coefficients, etc. (requires bit manipulation).
* **Goal:** To create a "graceful quality improvement" and understand how the JPEG bitstream is structured.

---

## 🎬 Introduction to Video Compression

**The Naive Approach:** A video is just a sequence of images. We could compress each frame as a separate JPEG. This works, but it's very inefficient.

**The Problem:** This naive approach completely ignores **temporal redundancy**. In a 30fps video, Frame 22 is almost identical to Frame 21.

### Exploiting Temporal Redundancy

**Method 1: Frame Differencing (DPCM)**

* **Idea:** Send the first frame (Frame 1) as a full JPEG. For Frame 2, send only the *difference* (`Frame 2 - Frame 1`). For Frame 3, send (`Frame 3 - Frame 2`), and so on.
* **Benefit:** The "difference" frame has very low entropy and compresses extremely well.
* **Problems:**
    1.  **Error Accumulation:** Quantization errors from one frame build up and propagate to all future frames (can be fixed with a "closed loop" system).
    2.  **No Random Access:** A user "channel surfing" can't start watching in the middle. They are missing all the previous frames needed to reconstruct the current one.
* **Solution:** Insert a full, independently-coded **Keyframe** (or **I-frame**) every 1-2 seconds. A new viewer just has to wait for the next keyframe to start decoding.

**Method 2: Block-Based Motion Compensation (The *Real* Solution)**

* **The Flaw in DPCM:** A simple frame difference fails if the *camera pans* or an *object moves*. The pixels aren't the same, but they *have* just moved.
* **The Idea:** Instead of sending the *pixel difference*, let's just describe the *motion*.
* **The Problem:** Sending a **Motion Vector (MV)** (`dx, dy`) for *every single pixel* would be more data than the original image!
* **The Solution:** Motion is **structured**. Objects move, not random pixels. We can apply motion to **blocks**.
* **How it works (Backward Prediction):**
    1.  Take the current frame (Frame N+1) and break it into **macroblocks** (e.g., 16x16).
    2.  For *each* block in N+1, search in the previous frame (Frame N) to find the **best-matching block**.
    3.  **The Encoder Sends Two Things:**
        * The **Motion Vector (MV):** The `(dx, dy)` coordinates of where the best match was found.
        * The **Residual Frame:** The (hopefully very small) *difference* between the block from N+1 and its predicted block from N.
* **Motion Estimation:** The process of finding the "best-matching block" (usually with a **Mean Absolute Difference** metric) is the most computationally expensive part of video encoding, often taking **80% of the encoder's CPU time**.