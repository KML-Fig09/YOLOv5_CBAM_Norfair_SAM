
# 🎯 **Advanced YOLOv5 Model with CBAM & Norfair Tracking SAM Segemntation Pipeline: A Computer Peripherals Detection System for Digital Streamers**
![HeadphoneHighlight](https://github.com/user-attachments/assets/e7a36c0a-b41a-4e64-afd4-3a250329fba9)

## 🚀 **Project Overview**

This project addresses challenges faced by **digital streamers** in the gaming and tech world. Live-streaming communities often focus on streamers' computer setups, with their audience curious about the equipment used (e.g., headsets, mice, keyboards, PCs). To streamline communication, this project automatically detects these peripherals and presents information in an aesthetically appealing manner using advanced **deep learning techniques**.

The system integrates a **custom YOLOv5** model, augmented with a **Convolutional Block Attention Module (CBAM)** to improve detection, alongside **Norfair tracking** to maintain object identity across frames, and the **Segment Anything Model (SAM)** for creating segmented masks with visually enhanced edge detection. This system is built to highlight detected objects, providing a **science-fiction-like experience** for the audience.

**Note:** The datasets required this model were trained on are too large for this repository, but they have been linked below. The steps I took to combine and augment them will be included in this repo, and the in-depth project report is available on request. 

## 🖥️ **Application Context**

Streamers often face disruptions when viewers request information about specific peripherals during broadcasts. This system is designed to alleviate those interruptions by automatically detecting and identifying peripherals in real-time, making the process more **seamless** and **aesthetically pleasing**. Within the confines of a student project, it was not possible to train on any one specific brand name or model, but the dataset used is a stand-in for the potential use of more expansive data. 

The final output features a **color-masked overlay** for each detected object. The project overall maintains temporal consistency with Norfair tracking, and can enhance visual engagement with SAM edge detection. Crucially, the SAM mask overlay includes accurate labels for each object, a function with is not yet possible with SAM alone. 

**Note before running**: You will need to upload your own mp4 video. Ensure it is of decent quality to allow the model to perform optimally. You may also wish to try running it with your own datasets, if you have access to more. 

## 📂 **Repository File Structure**

### Single Files:
- **README.txt**: This file, a detailed description of the context, aims, and contents of this repository. 
- **YOLOv5_CBAM_Norfair_SAM.ipynb**: The main Google Colab notebook containing code for training, inference, edge detection, and object tracking.
- **Dataset_Preprocessing_Augmentation.ipynb**: - Supporting notebook handling and preprocessing the datasets used in this project.
- **Splitting_the_Combined_Dataset.ipynb**: - Supporting notebook splitting the combined dataset into train, test, val, sets for use with custom YOLOv5 model.

### Zip Files:
- **yolov5_dir.zip**: YOLOv5 code and dependencies to be uploaded to the Colab environment.
- **train.zip**, **test.zip**, **val.zip**: Data containing images of computer peripherals, organized for training, testing, and validation.

### Folders:
1. **Output Examples**: Images showing examples of inference, tracking, and SAM edge detection. Videos available upon request. 
   - **HeadphoneHighlight.png**, **PCHighlight.png**.


## 📋 **Getting Started**

### Prerequisites
- **Google Colab**: For running the notebook with GPU support.
- **YOLOv5 Libraries**: Automatically installed via the Colab notebook.

### Setup Instructions [WIP]:
1. Clone the repository:
   ```bash
   git clone https://github.com/YOLOv5_CBAM_Norfair_SAM/YOLOv5_CBAM_Norfair_SAM.git
   ```
2. Upload `train.zip`, `test.zip`, `val.zip`, and `yolov5_dir.zip` to Google Colab.
3. Run the notebook sequentially, starting with **unzipping datasets** and **installing YOLOv5**, to **training, inference, tracking**, and **segmentation**.

## ⚙️ **How It Works**

### 1. **Custom YOLOv5 with CBAM**
The YOLOv5 architecture is enhanced with a **CBAM module** to boost detection accuracy, focusing on relevant spatial and channel-wise features. This helps with detecting complex objects like peripherals under various lighting conditions often found in streaming setups.

### 2. **Norfair Tracking**
Norfair provides **temporal consistency**, ensuring objects are tracked across multiple frames, even when they move or become occluded.

### 3. **SAM Edge Detection**
The **Segment Anything Model (SAM)** generates segmentation masks, enhancing the visual appeal by creating edge-detection overlays with distinctive colors (like **Twitch purple**) for each object.

## 🔬 **Methodology and Data Handling**

This project involved augmenting and combining multiple datasets from **Roboflow** to improve detection accuracy. The following augmentations were applied to simulate real-world variability:
- **Horizontal and Vertical Flips** (50% probability).
- **Brightness and Contrast Adjustments** (20% probability).
- **Shift, Scale, and Rotations** (50% probability).
- **Gaussian Blur** (20% probability).

Label files were processed carefully to maintain consistency and prevent errors in bbox coordinates.

## 🧠 **Model Architecture**

- **Backbone**: YOLOv5 uses **CSPNet** for feature extraction, maintaining efficiency and accuracy in real-time detection.
- **Neck**: **PANet** aggregates features from different layers for multi-scale detection. **CBAM** is sandwiched in this section. 
- **Head**: Predicts bounding boxes and object classes, using anchor boxes for different object sizes.

The custom YOLOv5 model was trained with the following parameters:
- **Image Size**: 640 pixels
- **Batch Size**: 16
- **Optimizer**: SGD with a learning rate of 0.002

The inclusion of **CBAM** allows the model to balance both channel and spatial attention, enhancing detection, particularly for smaller or occluded objects.

## 💡 **Tracking and Edge Detection Integration**

After object detection, **Norfair** tracks the detected objects with a custom Euclidean distance function, ensuring smooth transitions across frames. Then, **SAM** applies segmentation masks over detected objects, creating a visually appealing overlay that highlights peripherals during streaming.

## 📊 **Evaluation Metrics**

Key evaluation metrics include:
- **Precision**: How often the model correctly detects peripherals.
- **Recall**: The percentage of actual peripherals detected by the model.
- **Mean Average Precision (mAP)**: Overall detection performance.
- **Loss Metrics**: Box loss, object loss, and class loss, providing insight into model accuracy.

Despite some challenges, such as object misalignment in the final output, the system achieved substantial improvements over the pilot version, found at this github also, with a 121.43% increase in Precision-Recall mAP@0.5. Further improvements could be made with a larger dataset and more time to combine and augment such data.

## **Datasets Used**

- Energy Chaser (2023) Desktop PC. Roboflow Universe. Available at: https://universe.roboflow.com/energy-chaser/desktop-pc 
- Energy Chaser (2023) Monitors TVs & PC Monitors, etc.. Roboflow Universe. Available at: https://universe.roboflow.com/energy-chaser/monitors-tvs-pc-monitors-etc 
- Mouse 2Lugf (2023) Raava. Roboflow Universe. Available at: https://universe.roboflow.com/mouse-2lugf/raava
- Project IEC8E (2024) Mouses. Roboflow Universe. Available at: https://universe.roboflow.com/project-iec8e/mouses-zcwi8 
- Practicas (2024) Computer Keyboard. Roboflow Universe. Available at: https://universe.roboflow.com/practicas-eoqqx/computer-keyboard 
- YOLOv8 Workspace (2024) Headphones Detection. Roboflow Universe. Available at: https://universe.roboflow.com/yolov8workspace/headphones-detection-rx2oj 

## 💡 **How to Contribute**
Contributions are welcome to improve this project! If you'd like to contribute:
1. Fork this repository.
2. Make your changes in a new branch.
3. Submit a pull request explaining your changes / motivation.

## 💬 **Contact**
For any questions or suggestions, feel free to message me privately. 
