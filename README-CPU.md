# Short version 

## Google Colab Demo 
* CPU Version https://colab.research.google.com/drive/1B7qn8OXL29_VDfGyk1DJtWVd0QZGBxGn?usp=sharing
* GPU Version https://colab.research.google.com/drive/1IND9r8LkBx8JG1Z3sIdlIL9Ry-qY1aJ1?usp=sharing
* Run the web app trough a tunnel https://colab.research.google.com/drive/1nrc5Bk8bytdyxW1EBtpGWySdFcJChxK2?usp=sharing 

## Prepare Environments 
```
conda create --name nanoowl-cpu python=3.11 
conda activate nanoowl-cpu
```
## clone and pip install 
```
git clone https://github.com/abdshomad/nanoowl-cpu
pip install -r requirements-cpu.txt 
```
## Or, if failed, pip install one-by-one 
```
pip install torch torchvision torchaudio
pip install transformers
pip install opencv-python matplotlib
pip install git+https://github.com/openai/CLIP.git
pip install aiohttp
```
## Setup Nano OWL
```
cd nanoowl-cpu
python setup.py develop --user
```
## Make data folder before running examples 
```
cd nanoowl-cpu
mkdir data
```
## Run Examples
```
cd examples
python owl_predict.py --prompt="[an owl, a glove]" --threshold=0.1
python owl_predict.py --prompt="[an owl, a glove, a head]" --threshold=0.05
python tree_predict.py --prompt="[an owl [a wing, an eye]]" --threshold=0.15
python tree_predict.py --prompt="[an owl [a wing, an eye], a face [an eye, a nose]]" --threshold=0.05
python tree_predict.py --image "../assets/class.jpg" --prompt="[a face (smiling, neutral)]" --threshold=0.25
python tree_predict.py --image "../assets/class.jpg" --prompt="[a face (happy, sad)]" --threshold=0.25
python tree_predict.py --image "../assets/frog.jpg" --prompt="[a frog [an eye]]" --threshold=0.15

python tree_demo/tree_demo.py (this is still failed)
```
# Long Version 
# Running NanoOWL on CPU

This document provides instructions on how to run the NanoOWL project using only the CPU, without relying on a CUDA-enabled GPU. This is useful if you do not have a GPU or simply prefer to run on CPU (although performance will be significantly lower).

## Prepare the Environment

1.  **Create a new conda environment:** This step ensures that your dependencies do not conflict with other project dependencies.
    ```bash
    conda create --name nanoowl-cpu python=3.11
    ```
2.  **Activate the environment:** Switch to the newly created environment.
    ```bash
    conda activate nanoowl-cpu
    ```

## Clone Repository 
**Clone the Repository:** Download the NanoOWL code from GitHub.

```bash
git clone https://github.com/abdshomad/nanoowl-cpu
```

## Install Required Libraries

The following steps install all the necessary Python libraries for the project.
1.  **Install PyTorch (CPU Version):**  Install a basic PyTorch install that will use your computer's CPU, since CUDA will not be used for these instructions.
    ```bash
    pip install torch torchvision torchaudio
    ```
2.  **Install Transformers Library:** Install huggingface's transformers model library
    ```bash
    pip install transformers
    ```
3. **Install OpenCV and Matplotlib:** Install OpenCV for drawing bounding boxes and Matplotlib for setting up color maps.
    ```bash
    pip install opencv-python matplotlib
    ```
4.  **Install CLIP:**  Install the `clip` library directly from GitHub.
    ```bash
    pip install git+https://github.com/openai/CLIP.git
    ```
5. **Install aiohttp** Install aiohttp for use in the tree demo example for serving HTML and WebSockets.
    ```bash
    pip install aiohttp
    ```

## Install NanoOWL
1.  **Navigate to the Repository:** Enter the cloned directory
    ```bash
    cd nanoowl-cpu
    ```
2.  **Install the Package:** Install the NanoOWL package using the `setup.py` script. This registers the project for use in python scripts using the `import nanoowl` syntax.
    ```bash
     python setup.py develop --user
    ```

## Create a data Directory

1. **Create a `data` folder**: Create a folder called `data` at the root directory where you cloned the repository (nanoowl-cpu) This directory will be used as the default folder for outputs by various example scripts.
   
   This can be done manually by opening the folder location from a file explorer or from a terminal as shown below:
   ```bash
   mkdir data
   ```

## Run the Examples

The following commands demonstrate running the examples using only the CPU.

1. **Run `owl_predict.py`**

 This script runs the core OWL-ViT model and generates a new output in the `/data` directory with labels bounding boxes for a given image.

```bash
python examples/owl_predict.py --prompt="[an owl, a glove]" --threshold=0.1
```

2.  **Run `tree_predict.py`:** This example shows how to use the tree predictor for detecting objects at different levels and categories.
```bash
python examples/tree_predict.py --prompt="[an owl [a wing, an eye]]" --threshold=0.15
```

3. **Run `tree_demo/tree_demo.py`**:
   This example opens up a webserver for a camera-based real time demo for visualizating object detections.
```bash
python examples/tree_demo/tree_demo.py
```

4. **Run `tree_demo/tree_demo_using_video.py`**:
   This example opens up a webserver for a video based demo for visualizating object detections.

```bash
python examples/tree_demo/tree_demo_using_video.py --video_path "../../assets/owl360p.mp4
```

## Additional notes

   * These instructions specify that you use the **CPU** build of PyTorch
   * To run with CUDA/GPU, please refer to the official documentation provided in `README.md`.

By following the above instructions you should be able to fully execute the nanoOWL library locally on a CPU
