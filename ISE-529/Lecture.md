# 1/12 Lecture 1

### **Course Logistics & Overview**

* **Course:** ISE 529: Predictive Analytics.


* **Instructor:** Prof. Tao Ma.


  * **Office:** GER 216.


  * **Office Hours:** Wednesday, 2:30 PM – 3:30 PM.


  * **Communication:** Appointments available by email if office hours don't fit; open to in-person meetings .


* **Teaching Assistant:** Rhea Huang.


  * **Office Hours:** Monday, 2:00 PM – 4:00 PM (same building) .


  * **Role:** Contact for homework questions and grading issues.


* **Format:** Two sections (regular in-person and online) managed via **Brightspace**.


* **Prerequisites:** Fundamental knowledge of Python programming, statistical probability models, and linear algebra.

---

### **Grading Structure**

* **Homework (25%):**

  * 5 required assignments + 1 optional bonus assignment (Homework 6) .


  * **Late Policy:**


    * 1 day late: 20% deduction.


    * 2 days late: 50% deduction.


    * more than 2 days late: Not accepted (0 grade).


  * **Submission:** Submit via Brightspace only; do not email homework.


* **Midterm Exam (30%):** In-person.


* **Final Exam (40%):** In-person, non-cumulative (no overlap with midterm).


* **Bonus Points (Up to 3 pts):** Based on attendance and participation. These are added to the final grade and can lift a letter grade (e.g., from A- to A) .

**Exam Rules:**

* Exams are **Open Book** (hard copies allowed, cheat sheets allowed) .


* **No Electronics:** No internet access, laptops, or phones allowed during the exam .


* **Attendance:** Mandatory for exams; no make-up exams allowed .

---

### **Course Content: Key Takeaways**

The course covers four major modules focused on theory (lectures) and application (homework).

**1. Quantitative/Numerical Predictions**

* Focuses on regression techniques.


* **Models:** Simple/Multiple linear regression, Polynomial regression, Ridge & Lasso, Principal Component Regression (PCR), Partial Least Squares (PLS).

**2. Classification**

* Predicting the probability that an input belongs to a specific class (e.g., Yes vs. No, image recognition) .


* **Models:** Logistic Regression, Linear Discriminant Analysis (LDA), Quadratic Discriminant Analysis (QDA), Naive Bayes, Support Vector Machines (SVM) .

**3. Tree-Based Methods**

* Used for both numerical prediction and classification .


* **Techniques:** Decision Trees, Bagging, Random Forest, Boosting .

**4. Deep Learning (Neural Networks)**

* Includes theory and practical implementation.


* **Multi-layer Perceptrons (MLP):** For numerical data .


* **Convolutional Neural Networks (CNN):** For image data/pattern recognition .


* **Recurrent Neural Networks (RNN):** For time-series data.

---

### **Software & Technical Setup**

**1. Python Requirements**

* **Version:** You **MUST** install **Python 3.10** (specifically 3.10.9 recommended).

  * *Reason:* Newer versions (3.11+) are not yet compatible with **TensorFlow** .


* **Required Libraries:** Numpy, Pandas, Scikit-learn (sklearn), Statsmodels, TensorFlow.

**2. IDE Options (Integrated Development Environments)**

* **JupyterLab (Recommended):** The standard environment for the course. Files saved as `.ipynb`.


* **PyCharm (Advanced):** Recommended for students with Computer Science backgrounds or advanced users. Files saved as `.py`.


* **Google Colab (Alternative):** A cloud-based "dummy environment" that requires no installation. Useful if you struggle with local setup.

**3. Hardware Requirements**

* **Standard Homework:** A personal laptop (CPU/GPU) is sufficient for Homework 1-5.


* **Bonus Homework (HW6):** Requires High-Performance Computing (HPC).


  * Involves a large dataset (20,000+ images) that may crash personal laptops.


  * Students will be given access to the USC HPC cluster (Linux-based) .


  * *Alternative:* Viterbi Virtual Desktop (available but limited to 8-hour run times) .

---

### **Installation Guide (Step-by-Step)**

**Installing Python (Windows/Mac)**

1. **Download:** Go to the official Python website and download **Python 3.10**.


2. **Windows Setup:** When installing, **check the box "Add Python to PATH"** (crucial for the OS to find the software) .


3. **Linux Setup:** Update the `.bashrc` file to include the path to the software .

**Installing Libraries (pip)**

1. Open your Terminal (Mac/Linux) or Command Prompt (Windows) .


2. Use the `pip` command (Python's packaging tool) to install libraries from the PyPI repository.


* *Command:* `pip install [library_name]` (e.g., `pip install tensorflow`).

**Optional: Miniconda**

* Can be used to manage environments and multiple Python versions.


* Allows creation of virtual environments so you don't mess up your base operating system.

**Running Code**

* **JupyterLab:** Start by typing `jupyter lab` in the terminal from your project folder . It runs code in cells (interactive mode).


* **PyCharm:** Runs `.py` scripts. You can right-click a file and select "Run" .


* *Note:* You can run `.py` files inside JupyterLab using the command `%run filename.py` .

### **Next Steps for Students**

* Install Python 3.10 and set up the environment (JupyterLab/PyCharm) immediately.


* Respect the schedule: Exams are on March 4th and April 29th (dates may shift slightly, but these are targets) .


* Attendance is not tracked daily but is noticed for bonus points .