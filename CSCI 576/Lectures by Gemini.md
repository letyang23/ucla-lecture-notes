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