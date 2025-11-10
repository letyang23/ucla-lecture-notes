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

## 🏛️ Part 0: Course Administration

* **Assignment 1 Grading:**
    * Grades were released prematurely by mistake; the grading process is still ongoing.
    * Final grades should be available by early next week.
    * **Feedback:** For any test case where full marks were not awarded, graders are required to provide an exact line, comment, or screengrab to explain the discrepancy.
    * Office hours will be held for further clarification after all grading is finished.
* **Flexible Format Submission Issue:**
    * Some students accidentally left the submission in a flexible format (e.g., 5x12).
    * This will **not** be penalized if it's a simple matter of changing parameters in the code to fix the image size. Graders will handle this; no need to request a regrade.

---

## 🖼️ Part 1: Image Compression (Wavelets & JPEG 2000)

### JPEG Recap & Limitations

* **Pipeline:** Image $\rightarrow$ Transform (DCT) $\rightarrow$ Quantization $\rightarrow$ Entropy Coding (Zigzag Scan, VLC) $\rightarrow$ Bitstream.
* **Core Idea:** Transform to frequency space, which has lower entropy (less information) because natural images are not random.
* **Perceptual Trick:** Aggressively quantize high frequencies, which our eyes are less sensitive to, while preserving low frequencies.
* **Limitation:** At low bitrates, **blocking artifacts** appear. This is because DCT is block-based (8x8) and assumes the signal is stationary (frequencies are present everywhere), which isn't always true.
* **Solution:** **Wavelets**, which are better for non-stationary signals.

### Wavelet Compression (1D Haar Wavelet)

<img src="Lectures by Gemini.assets/image-20251106155702717.png" alt="image-20251106155702717" style="zoom:50%;" />

The core idea is to recursively separate a signal into low-frequency (averages) and high-frequency (differences) components.

* **Filters:**
    * **Low-Pass Filter (LPF):** Captures averages. Contains most of the perceptual information.
    * **High-Pass Filter (HPF):** Captures differences. Contains less information and can be quantized more aggressively.
* **1D Example (Signal: [9, 7, 3, 5])**
    1.  **Level 1 Pass:**
        * **Averages (LPF):** $\frac{9+7}{2} = 8$; $\frac{3+5}{2} = 4 \rightarrow [8, 4]$
        * **Differences (HPF):** $\frac{9-7}{2} = 1$; $\frac{3-5}{2} = -1 \rightarrow [1, -1]$
        * *Signal Representation 1:* `[8, 4, 1, -1]`
    2.  **Level 2 Pass (Recursive):** Apply the same process to the **LPF output** `[8, 4]`.
        * **Average (LPF):** $\frac{8+4}{2} = 6 \rightarrow [6]$
        * **Difference (HPF):** $\frac{8-4}{2} = 2 \rightarrow [2]$
    3.  **Final Representation:** `[6, 2, 1, -1]`
* **Compression & Reconstruction:**
    * The final representation `[6, 2, 1, -1]` contains the same information as `[9, 7, 3, 5]` and is perfectly reconstructible.
    * Compression is achieved by **quantizing (or dropping) the high-frequency coefficients**.
    * Example: If we only send `[6, 2]` and the decoder assumes the rest are zero (`[6, 2, 0, 0]`), it would reconstruct `[8, 4, 0, 0]` $\rightarrow$ `[8, 8, 4, 4]`. This is not the original, but perceptually similar from a distance.

### Wavelet Basis Functions

This provides the mathematical foundation for the averaging and differencing process. Any signal (data) can be represented as a sum of **Coefficients** $\times$ **Basis Vectors**.

* **Scaling Functions (Averages): $\phi$ (phi)**
    * These are **box functions**.
    * The base function $\phi(x)$ is a box of value 1 between 0 and 1.
    * $\phi_{j,i}(x) = \phi(2^j x - i)$ represents a box function that is **scaled** by $j$ (gets narrower) and **shifted** by $i$.
    * <img src="Lectures by Gemini.assets/image-20251106155844487.png" alt="image-20251106155844487" style="zoom:50%;" />
    * Example:
      * <img src="Lectures by Gemini.assets/image-20251106155919364.png" alt="image-20251106155919364" style="zoom:80%;" />
      * <img src="Lectures by Gemini.assets/image-20251106155958150.png" alt="image-20251106155958150" style="zoom:50%;" />
* **Wavelet Functions (Differences): $\psi$ (psi)**
    * These are the **Haar functions**.
    * The base function $\psi(x)$ is `+1` from 0 to 0.5 and `-1` from 0.5 to 1.
    * $\psi_{j,i}(x) = \psi(2^j x - i)$ represents a scaled and shifted difference function.
* **Example (Signal: `[6, 2, 1, -1]`)**
    * This final wavelet representation can be written as:
    * $6 \times \phi_{0,0}(x)$ (the final average)
    * $+ 2 \times \psi_{0,0}(x)$ (the first difference)
    * $+ 1 \times \psi_{1,0}(x)$ (the second-level difference)
    * $+ (-1) \times \psi_{1,1}(x)$ (the second-level difference, shifted)

### 2D Wavelet Transform

This applies the 1D transform to 2D images.

* **Standard Recursive Method:**
    1.  Take the input image. Apply the 1D wavelet transform to **every row**. This results in an image half-filled with Averages (LPF) and half-filled with Differences (HPF).
    2.  Take the result from step 1. Apply the 1D wavelet transform to **every column**.
    3.  **Result:** The image is now divided into four quadrants:
        * **LL (Low-Low):** Averages of rows, Averages of columns (a smaller, scaled-down version of the image).
        * **LH (Low-High):** Averages of rows, Differences of columns.
        * **HL (High-Low):** Differences of rows, Averages of columns.
        * **HH (High-High):** Differences of rows, Differences of columns (least important information).
    4.  **Recursive Step:** Take the **LL quadrant** and repeat steps 1-3 on it.
    5.  This process is repeated until the LL quadrant is a single pixel (the average of the entire image).
* **Benefit:** This hierarchical structure is excellent for scalability. You can send just the tiny LL quadrant for a blurry preview and progressively add the LH, HL, and HH quadrants at increasing resolutions to sharpen the image.

### JPEG 2000

* **Basis:** Uses wavelet representation instead of DCT.
* **Key Features & Advantages:**
    * **Better Compression:** Outperforms standard JPEG at the same file size.
    * **Region of Interest (ROI):** The bitstream can be organized so you only stream the coefficients needed for a specific part of the image (e.g., zooming in on one area in Google Earth).
    * **Random Spatial Access:** Can "tile" the image, allowing a decoder to jump to any tile (region) without decoding the whole thing.
    * **Scalability:** The single bitstream can be decoded at different resolutions or quality levels without re-encoding.
* **"Encode Once, Stream Multiple Ways":** A server can store one high-quality JPEG 2000 file and intelligently stream only the necessary parts (coefficients) based on the user's device (watch vs. laptop) and bandwidth.
* **Adoption:** Not common for everyday photos because JPEG is so entrenched. Used in specialized, high-bandwidth applications like **Digital Cinema** and **Google Earth**.

---

## 🎨 Part 2: Dithering

Dithering is a post-processing technique to improve the *perceived* quality of an image that has been heavily quantized (i.e., has fewer colors than the original).

* **Problem:** Simple quantization (e.g., thresholding grayscale to binary) produces terrible results (e.g., a face becomes two blobs for eyes).
* **Solution:** Use the limited color palette (e.g., just black and white) in a statistically distributed way to trick the eye into seeing intermediate shades.

### Halftoning

<img src="Lectures by Gemini.assets/Screenshot 2025-11-06 at 10.56.03 PM.png" alt="Screenshot 2025-11-06 at 10.56.03 PM" style="zoom:33%;" />

* An early newspaper technique.
* Divides the image into blocks and replaces each block with a pattern whose *perceived* grayness matches the block's average intensity.
* Often used concentric circles of increasing blackness.
* **Trade-off:** Larger blocks allow more "gray levels" but look blockier. Smaller blocks look smoother but have fewer intensity levels.

### Ordered Dithering

* Uses a $k \times k$ **dithering matrix** (or "order matrix") to determine the threshold for each pixel.
* A $k \times k$ matrix provides **$k^2 + 1$** perceived intensity levels.
* **Algorithm:**
    1.  For each pixel $I(x, y)$ in the input image:
    2.  Find the corresponding position in the dither matrix: $i = x \mod k$, $j = y \mod k$.
    3.  Get the matrix value $D(i, j)$.
    4.  **Normalize** the pixel's intensity $I(x, y)$ and the matrix value $D(i, j)$ to the same range (e.g., 0-8 for a 3x3 matrix and 0-255 for the pixel).
    5.  If $I_{\text{normalized}} > D_{\text{normalized}}$, output **white** (or 1).
    6.  Else, output **black** (or 0).

### Error Diffusion (e.g., Floyd-Steinberg)

* The highest quality method.
* **Key Idea:** Don't just discard the quantization error. **Diffuse** (spread) that error to neighboring pixels *that have not been processed yet*.
* **Algorithm (scanline order):**
    1.  Process the current pixel $P$.
    2.  Quantize it to the nearest available color (e.g., black or white). This is $P'$.
    3.  Calculate the error: $Error = P - P'$ (the "loss").
    4.  Distribute this $Error$ to neighbors that are to the **right** and **below** the current pixel, using specific fractions (e.g., the Floyd-Steinberg model).
    5.  When the next pixel is processed, its original value is first modified by the diffused error it received from its neighbors, *before* it gets quantized.
* **Result:** This process creates a much more natural, less-patterned distribution of pixels that is perceptually very close to the original grayscale image, even though it only uses black and white.

---

## 💻 Part 3: Assignment 2 Details

* **Task:** Implement a DCT-based progressive image viewer.
* **Process:** Go from RGB $\rightarrow$ DCT representation $\rightarrow$ Quantize. Then, de-quantize and apply Inverse DCT (IDCT) in one of three delivery modes.
* **Input Parameters:** Image, Quantization Level, Delivery Mode, Latency (to simulate a slow connection).
* **Delivery Modes:**
    1.  **Mode 1 (Baseline):** Process and display one 8x8 block at a time (block-by-block).
    2.  **Mode 2 (Spectral Selection):** Display all DC coefficients first. Then, add all AC coefficient 1. Then add all AC coefficient 2, etc., for all blocks.
    3.  **Mode 3 (Successive Approximation):** Send the Most Significant Bit (MSB) for *all* coefficients in *all* blocks. Then send the next bit, and the next, etc..
* **Goal:** Observe **"graceful quality improvements"** rather than random noise.
* **Development Tip:** Build and test in stages:
    1.  Get DCT and IDCT working (Input $\rightarrow$ DCT $\rightarrow$ IDCT $\rightarrow$ Output should look identical to Input).
    2.  Add Quantization and De-quantization.
    3.  Finally, implement the progressive delivery modes.

---

## 🎥 Part 4: Video Compression Fundamentals

### Temporal Redundancy

* **Core Concept:** A video is a sequence of images. The most naive compression (Motion JPEG, or MJPEG) is to just compress every single frame as a separate JPEG.
* **Inefficiency:** This ignores **temporal redundancy**—the fact that Frame 2 is extremely similar to Frame 1.
* **Better Approach (DPCM):**
    1.  Compress and send **Frame 1** (as a full image).
    2.  For Frame 2, calculate the **difference** ($Error = \text{Frame } 2 - \text{Frame } 1$).
    3.  Compress and send this $Error$ frame (which has much lower entropy and compresses better).
    4.  Decoder calculates $\text{Frame } 2 = \text{Frame } 1 + Error$.
* **Problem:** This is a long chain of predictions. To watch a stream, you *must* have Frame 1. If you join mid-stream (like tuning into a TV channel), you can't decode anything.
* **Solution: Keyframes (I-frames):** Periodically, the encoder inserts a **keyframe**, which is a full, independently-compressed frame (like a JPEG). This breaks the prediction chain and allows a new viewer to "sync up".

### Block-Based Motion Compensation (MC)

This is a more advanced way to exploit temporal redundancy, forming the basis of standards like MPEG.

* **Problem with Simple Differencing:** Pixels *move*. An object at $(x, y)$ in Frame $n$ may move to $(x+dx, y+dy)$ in Frame $n+1$. Simple differencing would see this as a large error.
* **Reasons for Pixel Change:** Camera motion, subject motion, lighting changes, and sensor noise.
* **Key Insight:** Motion is **structured**. Pixels don't move randomly; they move in **regions or blocks**.
* **MC Algorithm (Encoder Side):**
    1.  Take the current frame to be encoded ($F_{n+1}$) and divide it into **macroblocks** (e.g., 16x16).
    2.  For *each* macroblock in $F_{n+1}$, search the *previous* frame ($F_n$) to find the block that is the "best match".
        * This "backward prediction" (from $F_{n+1}$ to $F_n$) is preferred because it ensures every block in the *current* frame is accounted for.
    3.  The search is done in a "search area" around the block's original position.
    4.  "Best match" is determined by a metric, typically **Mean Absolute Difference (MAD)** (sum of absolute pixel-by-pixel differences).
    5.  The displacement $(dx, dy)$ between the current block and its best match is stored as a **Motion Vector (MV)**.
    6.  A **Predicted Frame** is created, assembled from all the "best match" blocks found in $F_n$.
* **What is Sent in the Bitstream:**
    1.  **Motion Vectors:** A list of ($dx, dy$) for every macroblock.
    2.  **Error Frame (Residual):** The encoder calculates $Error = F_{n+1} \text{ (Actual)} - \text{Predicted Frame}$. This error frame is then compressed (using DCT, quantization, etc.) and sent.
* **Decoder Side:** The decoder receives the MVs and the compressed Error Frame. It uses the MVs to build the same Predicted Frame, then adds the Error Frame back to get the final $F_{n+1}$.
* **Complexity:** Motion prediction is the most computationally expensive part of video encoding, often accounting for **80% of the computation**.



# Lecture 7 - 10/13/2025 - Video Compression

## 🏛️ Part 0: Course Administration

### Assignment 1 Grades

* Grades should be released this week.
* Feedback will be detailed, explaining any lost marks.
* **Zeros:** Some students may have received a zero if the graders could not compile the program or if no output was shown. Graders may have sent emails to get a program running.
* **Questions:** Email the graders or TAs, or attend their office hours.

### Assignment 2 (JPEG Pipeline)

* **Deadline:** Due in two weeks from the lecture date (Oct 13, 2025).
* **Goal:** Understand the JPEG pipeline and progressive streaming modes.
* **Pitfall 1: Clamping Values**
    * The DCT (Discrete Cosine Transform) and IDCT (Inverse DCT) processes involve floating-point math.
    * After the IDCT, your channel values (e.g., 0-255) might go *above* 255 or *below* 0.
    * You **must clamp** these values. If you simply cast them to an `unsigned char`, they will wrap around (e.g., `255.01` becomes `0`), ruining the image.
* **Pitfall 2: Progressive Modes**
    * **Baseline (Mode 1):** Displays block-by-block. The `latency` variable simulates a slow connection.
    * **Spectral Selection (Mode 2):** Displays coefficient-by-coefficient (all DCs, then all AC1s, etc.). This should show the image get progressively better over 64 iterations.
    * **Successive Approximation (Mode 3):** This is the hardest. It displays bit-plane by bit-plane (Most Significant Bit first).
        * Be very careful with **signed vs. unsigned** representations.
        * The first few iterations might be **all black** until the first non-zero bit is reached.
        * The goal is a **"graceful transition"** from a blurry image to a clear one.

---

## 🎥 Part 1: Video Compression Recap

* **Naive Method (MJPEG):** Compressing each frame as a separate image (like a JPEG). This works but is inefficient.
* **Problem:** It ignores **temporal redundancy**—the fact that Frame 2 is extremely similar to Frame 1.
* **Simple Prediction (DPCM):**
    * Predict that the next frame is the same as the previous frame.
    * Compute the **error** (the difference) between the actual frame and the predicted frame.
    * Compress and send this error. This works well unless there is a scene cut or large motion.
* **Key Insight:** Pixels don't move randomly; they move in a **structured** way. The goal of video compression is to exploit this structured motion.

---

##  COMPENSATION (The Core Concept)

This is the standard, block-based method used in most video codecs (mPEG, H.264, etc.) to predict motion.

### The Encoding Process

1.  **Divide Frame:** The *current* frame to be encoded ($F_{n+1}$) is divided into **macroblocks** (e.g., 16x16 pixels).
2.  **Search:** For *each* macroblock in $F_{n+1}$, the encoder searches the *previous* frame ($F_n$) to find the block of pixels that is the "best match."
3.  **Predict:** The encoder builds a **Predicted Frame** using all the "best match" blocks it found in $F_n$.
4.  **Calculate Error:** The encoder computes the **Error Frame** (also called the *residual*) by subtracting the Predicted Frame from the Actual Frame ($Error = F_{n+1} - \text{Predicted Frame}$).
5.  **Transmit:** The encoder sends two pieces of information:
    * **Motion Vectors (MVs):** A set of $(dx, dy)$ coordinates telling the decoder where to *get* each block from the previous frame. This is encoded **losslessly**.
    * **The Error Frame:** This error image is compressed **lossily** (using DCT, quantization, etc.). Since the prediction was good, the error frame has low entropy and compresses very well.

### The Search Algorithm (Brute Force)

* **Co-located Position:** For a macroblock at $(x, y)$ in $F_{n+1}$, the search starts at the same $(x, y)$ position in $F_n$.
* **Search Area ($k$):** The encoder searches in a window around this position, defined by a parameter $k$ (e.g., $k=31$ pixels). A larger $k$ can find faster motion but is computationally slower.
* **Process:** The encoder checks *every single possible position* within this $k \times k$ search area to find the one with the minimum error.

### Error Metrics (Finding the "Best Match")

These metrics are used to measure the difference between the current macroblock and a potential match.

* **MAD (Mean Absolute Difference):** The average of the absolute differences of all pixels.
* **SAD (Sum of Absolute Differences):** The sum of the absolute differences. This is the most common metric as it avoids a division, making it fast.
* **MSD (Mean Squared Difference):** The average of the *squares* of the differences. This metric heavily penalizes large differences but is computationally slower (a `square` operation is slower than an `absolute value`).

---

## 📈 Part 3: Macroblock Size & Complexity

### Macroblock Size

* **The Problem with Large Blocks:** If a single 16x16 block contains both a moving foreground object and a static background, the encoder is "conflicted." It will find a "best match" that is a poor compromise, resulting in a high error.
* **The Solution with Small Blocks:** If that same 16x16 area is broken into four 8x8 blocks, the encoder can find *different* motion vectors for each. The background blocks will have a $(0,0)$ vector, and the foreground blocks will have a vector that *accurately* tracks the motion.
* **Conclusion:** The sum of the errors from the 4 small blocks is almost always *less* than the error from the 1 large block.
* **Modern Standards (HEVC):** Use **adaptive block sizes** (called a Coding Tree Unit) that can be large for static areas (like a blue sky) and progressively smaller for complex boundaries.

### Computational Complexity

<img src="Lectures by Gemini.assets/image-20251107143325238.png" alt="image-20251107143325238" style="zoom:50%;" />

* **Brute Force Search** is extremely slow.
    1.  **SAD per position:** Requires $O(n^2)$ operations (where $n$ is macroblock size, e.g., 16).
    2.  **Positions to search:** $(2k+1)^2$ (where $k$ is the search parameter). If $k$ is on the same order as $n$, this is $O(n^2)$.
    3.  **Complexity per macroblock:** $O(n^2) \times O(n^2) = O(n^4)$.
    4.  **Macroblocks per frame:** The number of blocks is also proportional to the image size, giving another $O(n^2)$ factor.
    5.  **Total Complexity per Frame:** $O(n^4) \times O(n^2) = O(n^6)$, which is too slow for real-time encoding of HD video.

---

## 💨 Part 4: Fast Motion Estimation

To avoid $O(n^6)$ complexity, encoders use "smarter" search algorithms that *assume* the error decreases as you get closer to the best match.

* **Logarithmic Search:**
  
    1.  Check 9 points in a grid (center, corners, mid-sides).
    2.  Find the point with the *least* error.
    3.  Make this the *new center* and repeat the 9-point search in a smaller, refined area.
    4.  This "homes in" on the best match in logarithmic time.
    
* **Hierarchical Search:**
  
    <img src="Lectures by Gemini.assets/image-20251107144417004.png" alt="image-20251107144417004" style="zoom:50%;" />
    
    1.  Create an image pyramid by subsampling the frame (e.g., Level 4, Level 3, Level 2, Level 1=Full-res).
    2.  Perform a brute-force search on the *tiniest* level (Level 4). This is very fast.
    3.  Take the best MV from Level 4 and use it as a *starting guess* for Level 3.
    4.  At Level 3, perform a *small local search* (e.g., 8 new positions) around that guess to refine it.
    5.  Repeat this process down the pyramid to the full-resolution image.
    6.  This reduces the number of searches from thousands (e.g., 4225) to a tiny fraction (e.g., 105).

---

## 🎞️ Part 5: Frame Types (I, P, B)

* **I-frame (Intra-frame):**
    * A standalone frame compressed just like a JPEG, using only spatial redundancy.
    * Has **no dependencies**.
    * Used as a "keyframe" to start a video sequence or after a scene cut.
* **P-frame (Predicted-frame):**
    * Predicted from a *past* I-frame or P-frame.
    * More efficient than an I-frame.
* **B-frame (Bi-directional-frame):**
    * Predicted from *both* a **past** frame and a **future** frame.
    * These are the **most efficient** frames and offer the highest compression.
    * **Example:** An object entering the scene (the "rock" example) cannot be predicted from the past, but it *can* be predicted from the future, resulting in a near-zero error.
* **Problems with B-frames:**
    * **Delay:** The encoder must see and process $F_{n+2}$ *before* it can finish encoding $F_{n+1}$.
    * **Out-of-Order Transmission:** To decode a B-frame, the decoder needs both its past and future anchors. The transmission order must be re-ordered.
        * **Display Order:** `I_1, B_2, B_3, P_4, B_5, B_6, P_7...`
        * **Transmission Order:** `I_1, P_4, B_2, B_3, P_7, B_5, B_6...`

---

## 📺 Part 6: Video Standards & Structure

* **GOP (Group of Pictures):** A sequence of frames starting with an I-frame (e.g., `I B B P B B P`). The encoder is often configured with two parameters: `P between I` and `B between P`.
* **Syntactical Hierarchy:** Video Stream $\rightarrow$ GOPs $\rightarrow$ Frames (Pictures) $\rightarrow$ Slices (Group of Blocks) $\rightarrow$ Macroblocks $\rightarrow$ Blocks $\rightarrow$ (DC/AC) Coefficients.
* **Key Standards:**
    * **H.261:** For early video conferencing (ISDN). Low bitrate, I and P-frames only.
    * **mPEG-1:** For VCDs (~1.4 Mbps). Added B-frames.
    * **mPEG-2:** For DVDs and Digital TV. Introduced **transport streams** (188-byte packets) and **Scalable Streams**.
        * **Scalable Streams:** A single stream is split into a "base" (e.g., 600kbps) and an "enhancement" (e.g., 400kbps). If bandwidth drops, the decoder can drop the enhancement stream but continue playing the base stream, resulting in lower quality but no interruption.
    * **H.264 (AVC) / mPEG-4 Part 10:** The dominant standard for HD content.
    * **H.265 (HEVC):** High-Efficiency Video Codec. Needed for 4K streaming. Uses highly adaptive block sizes (Coding Tree Units) for maximum efficiency.

---

## 📡 Part 7: Rate Control

* **The Problem:** The "natural" bitrate of video is **Variable (VBR)**—high motion needs many bits, low motion needs few. But streaming networks are often designed for a **Constant Bitrate (CBR)**.
* **Naive CBR:** If a high-motion scene occurs, a naive encoder will just quantize *heavily* to stay under the bit limit. This causes massive, visible artifacts (as seen in the *Matrix* example clip).
* **Smart Rate Control:**
    1.  The encoder **buffers** incoming frames (e.g., 1-2 seconds) to "look ahead."
    2.  It analyzes this buffer to identify upcoming high-motion and low-motion scenes.
    3.  It then intelligently distributes the bit budget: it "borrows" bits from the low-motion scenes (by quantizing them slightly *more* than needed) and "spends" those saved bits on the high-motion scenes (quantizing them *less*).
    4.  This maintains a **constant average bitrate** over the buffer window while maximizing the *overall perceptual quality*.

# Lecture 8 - 10/20/2025 - Audio Compression
## 1. 🎵 Four Core Methods of Audio Compression

The lecture organizes audio compression into four main categories based on how "sound" is treated:

1.  **Sound as a Waveform:** Treating audio as a generic statistical signal.
2.  **Sound as Perceived:** Using the limitations of the human ear (psychoacoustics) to remove data we can't hear.
3.  **Sound as Produced:** Parameterizing the *source* of the sound (e.g., the human larynx) and synthesizing it.
4.  **Sound as Performed:** Storing the "score" or instructions for the music (e.g., MIDI) rather than the recorded sound itself.

---

## 2. 📈 Type 1: Sound as a Waveform (Statistical Compression)

This method compresses the digital signal itself with no understanding of human hearing.

### Key Concepts

* **DPCM (Differential Pulse-Code Modulation):** A form of prediction. Instead of storing each sample's value, store the *difference* between a sample and the previous one.
    * **Why?** The *dynamic range* of the differences is much smaller than the samples themselves, requiring fewer bits to store.
    * **Prediction Model:** The simplest form of DPCM predicts the next sample will be the *same* as the previous sample; the "difference" is the *error* in this prediction.
* **Delta Modulation:** A specific type of DPCM where the difference is stored as only **one bit** (+delta or -delta).
* **ADPCM (Adaptive DPCM):** The number of bits used to store the difference *changes* (adapts) based on how quickly the signal is changing.
* **Companding (Compressing + Expanding):** A non-uniform quantization technique used for human voice.
    * **Problem:** The dynamic range of human voice is large, but most speech happens in a narrow "conversational" band.
    * **Solution:** Use a *logarithmic* scale. This creates smaller, more precise quantization intervals in the common conversational range (reducing error) and larger, less precise intervals at the loud/quiet extremes.
    * **Standards:** A-Law (16-bit to 13-bit) and $\mu$-Law (16-bit to 12-bit).

---

## 3. 👂 Type 2: Sound as Perceived (Psychoacoustics)

This method, used by MP3, exploits the limitations of the human ear to discard data that a listener would not be able to hear.

### Human Hearing Limitations

1.  **Frequency Limitation:** The ear can only hear frequencies between **20Hz and 20kHz**.
    * **Compression:** Use filters to throw away all data outside this range *before* compression.
2.  **Time Domain Limitation:** The ear processes sound in small windows of about **30 milliseconds**.
    * If two sounds arrive **> 30ms** apart, you hear both.
    * If two sounds arrive **< 30ms** apart, one can **mask** (or garble) the other.

### The Masking Model

* **Threshold in Quiet:** The baseline minimum intensity (loudness) needed to hear a frequency in a perfectly quiet room.
    * **The Curve:** This threshold is not flat. It's a U-shape where the ear is *most sensitive* (requires the *least* intensity) in the **2kHz - 4kHz** range, which is the range of human speech.
    
    * **Compression:** Any sound *below* this curve is inaudible and can be discarded (given 0 bits).
    
      <img src="Lectures by Gemini.assets/image-20251108001844731.png" alt="image-20251108001844731" style="zoom:50%;" />
    
* **Frequency Masking:** A loud sound (a "masker") will *raise* the "threshold in quiet" for frequencies near it.
  
    * Any other sound that falls under this *new, raised curve* is "masked" and becomes inaudible, even if it was above the original "threshold in quiet".
    
    * **The Global Masking Curve:** In a real signal (like music), there are many frequencies at once. The final threshold is the **envelope** (the combined "sum total") of all the individual masking curves from all the different frequencies.
    
      <img src="Lectures by Gemini.assets/image-20251108003003354.png" alt="image-20251108003003354" style="zoom:50%;" />
    
      <img src="Lectures by Gemini.assets/Screenshot 2025-11-08 at 12.31.52 AM.png" alt="Screenshot 2025-11-08 at 12.31.52 AM" style="zoom:50%;" />

### Perceptual Encoder vs. Decoder

* **Asymmetric:** The encoder is much more complex than the decoder.
* **Encoder:** Takes a 30ms window, analyzes all its frequencies, and builds the dynamic **Global Masking Curve** for that specific window. It then allocates bits based on this curve (maskers get bits, masked sounds get 0 bits).
* **Decoder:** Does **not** have or need the perceptual analysis module. The encoder already made all the "perceptual" decisions. The decoder just reconstructs the frequencies it was sent.

### Audio vs. Visual Compression (Key Difference)

* **Visual (JPEG):** Uses a **static** (fixed) quantization table. It's always biased towards low frequencies and is *known* by both the encoder and decoder. It is *not* sent in the bitstream.
* **Audio (MP3):** Uses a **dynamic** bit allocation table. The number of bits for each frequency *changes for every 30ms window* based on the masking curve. This table *must be sent in the bitstream* for the decoder to understand the data.
* **Difficulty:** Audio is **harder** to compress than video because the ear is *more sensitive* to errors and noise than the eye.

---

## 4. 🗣️ Type 3: Sound as Produced (Source Coding)

This method models the *physical source* of a sound. It's used almost exclusively for **human speech**.

* **Model of Speech:** Human voice = Larynx (a "buzzer" producing a base frequency up to **4kHz**) + Vocal Tract (a "filter" created by the tongue, lips, and mouth).
* **Linear Predictive Coding (LPC):** The main algorithm for speech.
    * **Windowing:** Speech is sampled at **8kHz** (Nyquist for the 4kHz larynx) and broken into **30ms windows**, which contain **240 samples**.
    * **Analysis:** Each window is classified as *Voiced* or *Unvoiced*.
        * **Unvoiced:** A sound with no larynx frequency (e.g., "sh", "f"). The encoder just sends **1 bit** to flag it as "unvoiced". The decoder **fills these 240 samples with random noise**, which our brain perceives correctly. This provides huge compression (~40% of speech).
        * **Voiced:** A sound with a base larynx frequency (e.g., "e", "o"). The encoder performs LPC analysis.
    * **LPC Parameters:** Instead of sending 240 samples, the encoder finds a *pitch frequency* and a small set of *prediction coefficients* (e.g., 16 $\alpha$ parameters) that can be used to mathematically *synthesize* the 240 samples.
    * **Data Sent (Voiced):** 1 bit (flag) + Pitch Frequency + ~16 $\alpha$ parameters + a small **Residue** (the error between the original and synthesized signal).

---

## 5. 🎹 Type 4: Sound as Performed (Structured Audio)

* **Example: MIDI (Musical Instrument Digital Interface)**.
* **Concept:** Does not store any recorded audio. It stores a *description* or "score" of the music.
* **Analogy:** This is like compressing an image of text using **OCR** (Optical Character Recognition) to store the letters, rather than using **JPEG** to store the pixels.
* **Playback:** The decoder (e.g., your computer) reads the score and uses its own *local library* of instrument sounds to synthesize the music.
* **Pros/Cons:** Provides the *best* compression but cannot be used for human voice and is dependent on the quality of the decoder's sound library.

---

## 6. 💿 Audio Standards

### MPEG-1 Audio (Layers 1, 2, 3)

* **MP3 = MPEG-1 Layer 3**. (It is *not* MPEG-3).
* **Backwards Compatible:** A Layer 3 decoder can play Layer 2 and 1 streams.
* **Transparency Bitrates** (sounds the same as the original):
    * **Layer 1:** 384 kbps
    * **Layer 2:** 296 kbps
    * **Layer 3 (MP3):** **96 kbps** (This massive improvement is due to its advanced psychoacoustic model).

### Key Innovations in MP3 (Layer 3)

MP3 adds three main components to the standard perceptual encoder:

1.  **MDCT (Modified Discrete Cosine Transform):** A standard DCT on non-overlapping windows creates "clicks" (blocking artifacts) between audio blocks. The MDCT uses **overlapping windows** to ensure the signal is continuous, eliminating the "clicks".
2.  **Huffman Encoder:** After the perceptual model and quantization, the data is *further* compressed using Huffman (entropy) coding, just like in JPEG.
3.  **Buffer & Rate Control:**
    * Huffman coding creates a **Variable Bitrate (VBR)** stream.
    * Streaming applications require a **Constant Bitrate (CBR)**.
    * MP3 uses a *buffer* to absorb the VBR data and output it at a CBR.
    * **Feedback Loop:** If the buffer gets full, it sends a signal *back* to the **quantizer**, telling it to "quantize more heavily" (i.e., create less data) to prevent an overflow.

### MPEG-2 Audio

* Extends MPEG-1 to be **multi-channel** (e.g., 5.1 surround sound).
* **AAC (Advanced Audio Codec):** A non-backwards-compatible part of the MPEG-2 standard. It improves on MP3 by applying psychoacoustics *across* channels (e.g., a loud sound in the left ear can mask a quiet sound in the right ear).



# Lecture 9 - 10/27/2025 - Graphic Compression

## 1. 🖼️ Introduction to Graphics

### Core Goal
* The lecture's goal is not to be a full computer graphics course, but to understand graphics from a multimedia perspective.
* This involves:
    * How graphics are **represented** (2D and 3D).
    * Where the **redundancy** is in that representation.
    * How to **compress** that information for storage and streaming.

### Typical Graphics Pipeline
The process of creating a 3D image involves several stages:
1.  **Models:** Creating 3D assets (objects, characters) with textures.
2.  **Reflectance:** Defining the physical properties of a model's surface (e.g., plastic, metal, shiny).
3.  **Lighting & Rendering:** Simulating light, shadows, and other effects to create a realistic (or stylized) 2D image from the 3D scene.
4.  **Motion (Animation):** Moving objects, characters, or simulating effects (smoke, liquid) over time, frame by frame.

### Applications
* **Scientific Visualization**
* **Medical Imaging** (MRI, CT)
* **CAD/CAM** (Computer-Aided Design & Manufacturing)
* **Entertainment** (CG animated films, visual effects)
* **Multimedia Contexts:** Virtual Reality (VR) and Augmented Reality (AR).

---

## 2. ⚡ Core Concepts: Raster vs. Vector

<img src="Lectures by Gemini.assets/Screenshot 2025-11-08 at 4.05.40 PM.png" alt="Screenshot 2025-11-08 at 4.05.40 PM" style="zoom:50%;" />

Ideal vs. Vector vs. Raster

### Vector Graphics

* **Representation:** An ideal line drawing. Data is stored as mathematical definitions of vertices (2D locations) and the lines or curves that connect them.
* **Resolution:** Resolution-independent. You can zoom in "infinitely" and the line remains sharp because it is just redrawing the line between two points.

### Raster Graphics
* **Representation:** An image made of pixels (e.g., on your monitor). The data is stored in a **frame buffer**, which is a block of memory holding the color value for each pixel.
* **Resolution:** Fixed resolution. Zooming in eventually reveals the individual pixels (pixelation).

### Frame Buffer Types
* **True Color Frame Buffer:** Each pixel in memory stores a full, accurate RGB value.
* **Index Color Frame Buffer:** Used for low-end displays. An 8-bit value in the frame buffer doesn't store a color, but rather an *index* (0-255) into a **Color Map** (or Lookup Table) that holds 256 pre-selected RGB colors.

---

## 3. 📐 Part 1: 2D Graphics Representation & Transformations

### 2D Primitives (The Model)

<img src="Lectures by Gemini.assets/image-20251108162917528.png" alt="image-20251108162917528" style="zoom:50%;" />

A 2D object or model is logically represented by a set of primitives:
* **Vertices:** A list of 2D coordinates, $v_i = (x_i, y_i)$.
* **Edges:** A list of pairs of vertices that are connected, $e_{ij} = (v_i, v_j)$.
* **Faces (Triangles):** A list of vertex *indices* that form a triangle, $f_k = (v_1, v_2, v_6)$. The entire object is drawn by drawing all its faces.

### 2D Transformations

To animate an object, we apply mathematical transformations to its vertices.

1. **Translation (Move)**

   <img src="Lectures by Gemini.assets/image-20251108162952084.png" alt="image-20251108162952084" style="zoom:50%;" />

   * **Operation:** An *additive* operation.
   * **Formula:** The new position is $x' = x + d_x$ and $y' = y + d_y$, where $(d_x, d_y)$ is the translation vector.

2. **Rotation (Turn)**

   <img src="Lectures by Gemini.assets/image-20251108163928267.png" alt="image-20251108163928267" style="zoom:50%;" />

   * **Operation:** A *multiplicative* operation.
   * **Formula (about origin):**
       * $x' = x \cos(\theta) - y \sin(\theta)$
       * $y' = x \sin(\theta) + y \cos(\theta)$
   * **Problem:** This matrix only rotates around the *origin* (0,0). To rotate an object "in place" around its own center, you must:
       1.  Translate the object to the origin.
       2.  Perform the rotation.
       3.  Translate the object back to its original position.
   * **Key Point:** Translation and Rotation are **not commutative** (T * R is not the same as R * T).

3. **Scaling (Resize)**

   * **Operation:** A *multiplicative* operation.
   * **Formula (about origin):** $x' = x \cdot s_x$ and $y' = y \cdot s_y$.
   * If $s_x = s_y$, it is **uniform scaling**. If $s_x \neq s_y$, it is **non-uniform scaling**.

### Homogeneous Coordinates
* **The Problem:** The standard transformations are *non-homogeneous*. Translation is **addition**, while Rotation and Scaling are **multiplication**. This is cumbersome for a graphics engine, which would have to check which operation to perform.
* **The Solution:** Convert *all* operations into a **single, uniform multiplication**.
* **The Method:** Add a third coordinate, $w$, to every vertex. A 2D point $(x, y)$ becomes **$(x, y, 1)$**.
* **The New Matrices:** All transformations become 3x3 matrices.
    1.  **Homogeneous Translation:**
        * We can now represent the *additive* translation $(x + d_x)$ as a *multiplication*.
    2.  **Homogeneous Rotation:**
        * The original 2x2 rotation matrix is embedded within a 3x3 matrix.
    3.  **Homogeneous Scaling:**
        * The original 2x2 scaling matrix is embedded within a 3x3 matrix.
* **The Benefit:** To create a complex animation, you can now **multiply all the matrices together** (e.g., $M_{final} = T_2 \cdot R \cdot T_1 \cdot S$) into a single composite matrix. This one matrix can then be applied to all vertices of the object.

---

## 4. 🧩 Part 2: 3D Graphics Compression

### Motivation
* Modern 3D models (e.g., from 3D scanners) are incredibly dense, with millions of vertices and polygons.
* This massive amount of data must be compressed for storage, streaming, and real-time gaming.

### 3D Representation (The Mesh)
A 3D mesh is defined by two main components:
1.  **Geometric Information:** The list of 3D vertex coordinates, $v_i = (x_i, y_i, z_i)$.
2.  **Connectivity Information:** The list of faces (triangles) that define the surface, $f_k = (v_i, v_j, v_k)$. These are *indices* into the vertex list.

### Information Cost (Uncompressed)
* **Assumption:** A closed, bounded mesh has approximately **twice as many faces as vertices** ($F \approx 2V$).
* **Geometry Cost:** For $n$ vertices:
    * $n \text{ vertices} \times 3 \text{ coordinates/vertex (x,y,z)} \times 32 \text{ bits/coordinate (float)} = \mathbf{96n} \textbf{ bits}$.
* **Connectivity Cost:** For $\approx 2n$ faces:
    * $2n \text{ faces} \times 3 \text{ indices/face} \times \log_2(n) \text{ bits/index} = \mathbf{6n \log_2(n)} \textbf{ bits}$.
* **Total Bits = $96n + 6n \log_2(n)$**.

### Compression Algorithm 1: Quantization (Lossy)
* **Method:** A simple lossy compression method.
* **Idea:** Reduce the precision of the vertex positions.
* **Example:** Instead of storing each $x$, $y$, and $z$ coordinate as a 32-bit float, quantize it and store it as a 16-bit short. This introduces small errors but cuts the geometry cost significantly.

### Compression Algorithm 2: Topological Surgery
* **Goal:** Compresses **connectivity information** by removing redundancy.
* **Redundancy:** Every *shared edge* in a mesh is defined by two vertices. This pair of vertices is stored *twice* (once for each triangle that shares the edge).
* **Method:**
    1.  Treat the 3D mesh as a graph ($V=\text{Nodes}, E=\text{Edges}$).
    2.  Create a **Vertex Spanning Tree**—a path that visits all vertices *without* creating cycles.
    3.  Metaphorically "cut" the mesh along the edges of this spanning tree.
    4.  This "unfolds" the 3D mesh into a 2D layout of "triangle strips" or "runs".
* **Benefit 1 (Connectivity):** Instead of storing 3 indices for *every* triangle, you can store a "triangle strip" as a single run of indices (e.g., $v_1, v_2, v_3, v_4, v_5...$). This implicitly defines triangles $(v_1, v_2, v_3)$, $(v_2, v_3, v_4)$, $(v_3, v_4, v_5)$, etc., which is much more compact.
* **Benefit 2 (Geometry):** The spanning tree creates a *traversal order* (a sequence) for the vertices. We can now use **DPCM** (like in audio).
    * Store the full $xyz$ for the first vertex.
    * For all other vertices, just store the *difference* $(dx, dy, dz)$ from the previous vertex in the tree.
    * These $(dx, dy, dz)$ values are small and can be stored with fewer bits than the full 32-bit float coordinates.
* **Optimization:** The *choice* of spanning tree matters. A Depth-First Search (DFS) often creates long, simple strips (low entropy).
* **Metric:** The best spanning tree expands into **flatter areas** first, as they have less entropy.
    * **How to find "flatness":** Calculate the **dot product of the normal vectors** of two neighboring vertices. A high dot product (close to 1.0) means the normals point in the same direction, indicating a very flat surface. The algorithm should always expand to the neighbor with the highest dot product.

### Compression Algorithm 3: Polyhedral Simplification (Progressive Meshes)

<img src="Lectures by Gemini.assets/Screenshot 2025-11-08 at 9.25.33 PM.png" alt="Screenshot 2025-11-08 at 9.25.33 PM" style="zoom:50%;" />

* **Goal:** Reduce the number of vertices and edges in a model to create a simpler version.
* **Core Operation:** **Edge Collapse**.
    * Select two vertices, $v_s$ and $v_t$, that are connected by an edge.
    * Collapse the edge and merge the two vertices into a *single* new vertex (e.g., at their midpoint).
* **Process:** Start with the original high-poly mesh and sequentially perform edge collapses one by one, reducing the total vertex count with each step.
* **Application (Level of Detail - LOD):** Used heavily in games.
    * When the object is *close* to the camera, the full-detail 13,000-face model is rendered.
    * When the object is *far away*, a simplified 1,000-face version is rendered, which is faster and looks "good enough" from a distance.
* **Metric:** To minimize the *perceived* loss, the algorithm must choose which edge to collapse.
    * The best choice is to collapse edges in the **flattest areas** of the model, where the change will be least noticeable.
    * The metric is the same as before: collapse the edge between two vertices with the **highest dot product (most similar normals)**.



# Lecture 10 - 11/3/2025 - Graphic Compression

## 1. 🔒 Introduction to Digital Rights Management (DRM)

### Core Problem
* Digital media (movies, music, etc.) is easy to copy and distribute.
* The challenge is to protect this content, especially when using **open networks** and **open standards** (like MPEG or JPEG), which are designed to be easily read and decoded.
* If content is compromised, you need a way to **prove ownership** and, ideally, **find out where the leak occurred**.

### Two Pillars of DRM
The lecture focuses on two main techniques that work in complementary, or *orthogonal*, ways:

1.  **Watermarking:** Embedding a hidden digital signature *into* the media to prove ownership or track distribution.
2.  **Encryption:** Scrambling the media *during transit* to make it unintelligible without a key.

### Key Constraints for Media DRM
A successful DRM system for media *must* follow two critical engineering rules:

1.  **Bitrate Unchanged:** The encryption or watermarking process cannot change the stream's bitrate. An encoder works hard to create a **Constant Bitrate (CBR)** stream for smooth playback, and the DRM must not break this.
2.  **Bitstream Compliance:** The stream must remain *partially* readable as a valid MPEG (or other standard) file. You cannot just encrypt the entire file, because intermediary network devices need to access parts of the stream for tasks like inserting local ads.

---

## 2. 💧 Watermarking

### Concept
* **Steganography** (hidden writing) is the general term for hiding a message. In stganography, the *message* is important, and the rest is just noise.
  * example: read last word in every line.

* **Watermarking** is a subset where the *host signal* (the media) is the important part. The goal is to embed a secondary signal (the watermark) without destroying the host signal.

### Classifications & Desirable Qualities
* **Visible vs. Invisible:** Invisible watermarks are preferred so they don't interfere with the content. Visible watermarks are sometimes used for branding (e.g., a Nike logo).
* **Fragile:** This is a desirable quality. A fragile watermark is so deeply integrated with the media that any attempt to remove it will also **damage or destroy the content** itself.
* **Payload:** The size of the watermark data. It should be small.
* **Robustness:** The watermark must be difficult to remove and must survive **attacks**.

### Watermark Attacks
1.  **Intentional Attacks:** A malicious user trying to find and remove the watermark.
2.  **Unintentional Attacks:** Common, everyday media processes that can accidentally damage or destroy the watermark. These include:
    * Compression and decompression
    * Transcoding (changing formats)
    * Filtering
    * Resampling (changing size or sample rate)

---

## 3. 🏞️ Watermarking Techniques by Media Type

### Text
* **Line Shift Coding:** Embedding a '1' by shifting a line of text up by one pixel, or a '0' by shifting it down. To provide a reference, this is only done on *even* lines, while *odd* lines are left untouched.
* **Word Shift Coding:** Shifting a word slightly left or right to encode a bit.
* **Feature Coding:** Modifying tiny features of a letter, such as making the stem of a 'T' slightly longer or the dot on an 'i' bigger or smaller.

### Images (Spatial Domain)
* **Least Significant Bit (LSB):** The watermark bit (a '1' or '0') is written into the *lowest bit-plane* of a pixel (e.g., the 8th bit of an 8-bit color value).
    * **Problem:** This is **not secure**. An attacker can easily destroy the watermark by "randomizing" the entire LSB plane, which has no visible effect on the image.
* **Correlation:** A secret key generates a pseudorandom pattern of small positive and negative values (e.g., +k and -k). This pattern is *added* directly to the image's pixels. The detector uses the same key to re-generate the pattern and runs a correlation to see if it's present.

### Images (Frequency Domain - for JPEG/MPEG)
This is a robust method designed to survive compression.
1.  **Process:** It works *after* the DCT and **quantization** steps.
2.  **Block Selection:** A secret key generates a pseudorandom sequence of 8x8 blocks to embed bits into.
3.  **Coefficient Selection:** Within a block, the algorithm selects **three specific DCT coefficients** from the **mid-frequency range**.
4.  **Pattern Embedding:** It embeds a '1' or '0' by forcing a specific *pattern* on these three values (let's call them A, B, and C):
    * **To Embed '1':** Force value **C** to be the **lowest** of the three (e.g., $A > C$ and $B > C$).
    * **To Embed '0':** Force value **C** to be the **highest** of the three (e.g., $A < C$ and $B < C$).
    * **Invalid:** If C is in the middle, the block is marked as invalid, and the bit is embedded in the *next* block in the sequence.
5.  **Modification:** If the block's existing pattern doesn't match the bit (e.g., the pattern is '0' but you need to embed '1'), the algorithm adds/subtracts small values (within a threshold) to the coefficients to *force* the correct pattern.
6.  **Why Mid-Frequencies?**
    * **Not Low-Frequencies:** These are perceptually vital. Changing them would visibly damage the image.
    * **Not High-Frequencies:** These are mostly quantized to zero during compression, so there is no data to modify. Mid-frequencies are the best compromise for robustness and invisibility.

### Video
* Video watermarking is difficult due to **temporal confusion**.
* A **static watermark** (same in every frame) becomes visible when the video content moves.
* A **dynamic watermark** (changes every frame) becomes visible as flickering when the video content is static.

### Audio
* **Observation:** Audio signals have a **local zero-mean**. In any small window of samples, the positive and negative values tend to average out to zero.
* **Two-Set Method:**
    1.  A key selects two sets of samples, **Set C** and **Set D**.
    2.  To embed '1': Add a small, imperceptible value $d$ to all samples in Set C. **Subtract** $d$ from all samples in Set D.
    3.  To embed '0': **Subtract** $d$ from Set C. Add $d$ to Set D.
* **Detection (without original):** The detector finds the same sets C and D using the key.
    * It calculates: $E[C_{watermarked}] - E[D_{watermarked}]$
    * If the result is $\mathbf{+2d}$, it's a **'1'** (because $(0+d) - (0-d) = 2d$).
    * If the result is $\mathbf{-2d}$, it's a **'0'** (because $(0-d) - (0+d) = -2d$).

---

## 4. 🔑 Encryption for Media

### Hard Encryption vs. Soft (Selective) Encryption
* **Hard Encryption (e.g., RSA, PKI):** Encrypts the *entire* file. This is what's used for credit cards and banking. This is **not suitable for media** due to:
    1.  **Large File Size:** Encrypting gigabytes of data is too slow.
    2.  **Real-Time Constraints:** Cannot be done on the fly for streaming.
* **Soft/Selective Encryption:** The solution for media. Instead of encrypting the whole file, you encrypt *only the most important parts*.
    * **Example (MPEG Video):** A video stream consists of I, P, and B frames. The P and B frames are *dependent* on the I-frame. You only need to **encrypt the I-frames**. An attacker with the unencrypted P and B frames still can't reconstruct the video, as they are useless without the decrypted I-frame.

---

## 5.  industry DRM Solutions

### Music Industry (Apple iTunes & FairPlay)
* **Problem:** After Napster, Apple needed a DRM system that was secure and could work on both powerful Macs and computationally weak iPods.
* **The Solution (Hybrid Encryption):**
    1.  The entire song is encrypted **once** with a single **Master Key**.
    2.  This Master Key is stored in a "user data" section of the **AAC** audio file.
    3.  When a user buys the song, their account's unique **User Key** is used to encrypt *only the Master Key*.
* **Result:** Every user downloads the *same* large, encrypted song file. However, the tiny Master Key needed to unlock it is *differently encrypted for every single user*.
* **Benefits:**
    * **Scalable:** The server only has to do a tiny encryption (for the key) at download time, not encrypt the entire multi-megabyte song for every user.
    * **Secure:** If one user's key is cracked, it only compromises *their* song; it can't be used to unlock anyone else's.

### Motion Picture Industry
* **Problem:** A much more complex distribution chain (studio $\rightarrow$ distributor $\rightarrow$ theater network $\rightarrow$ local theater), with many potential points for leaks.
* **The Solution (Session-Based Watermarking):**
    1.  A unique watermark (WM 1) is embedded when the movie leaves the studio.
    2.  When it arrives at the main distributor, a *second* watermark (WM 2) is added on top.
    3.  When the distributor sends it to the AMC theater chain, a third (WM 3) is added, and so on.
* **Result:** When a pirated movie is found, forensics can analyze it.
    * If it contains only WM 1 and WM 2, they know the leak happened *at the main distributor*.
    * If it contains all ten watermarks, they know the leak happened *at the specific movie theater*. This allows them to pinpoint the exact location of the compromise.