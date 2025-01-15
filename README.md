# Automated Information Extraction using Deep Learning Models

## Overview

This project focuses on extracting meaningful information from product images to identify physical attributes (height, depth, width, voltage, wattage, etc.) using a combination of image processing techniques and deep learning models like YOLOv8, EasyOCR, and BERT. The goal is to create an end-to-end pipeline for identifying and processing images from two specific categories to retrieve text-based attributes.

## Models Used

### YOLOv8 (You Only Look Once v8)
- **Task**: Object detection for extracting text from images.
- **Data**: Fine-tuned using 250 hand-labeled images, including data augmentation techniques.
- **Output**: Extracts text regions for further processing.

### EasyOCR
- **Task**: Optical Character Recognition (OCR) for extracting text from images.
- **Data**: Fine-tuned for our dataset, post image-processing to enhance readability in low-quality images.
- **Output**: Extracts text for both classes of images.

### BERT (Bidirectional Encoder Representations from Transformers)
- **Task**: Used for question-answering tasks, where the text extracted by EasyOCR is used as the context and specific attributes are retrieved by forming questions (e.g., "What is the wattage?").
- **Data**: Fine-tuned on training data with domain-specific QA pairs.
- **Output**: Retrieves answers related to voltage, wattage, volume, weight, etc.

## Pipeline

### Image Segmentation
Images are categorized into two sections:
1. **Height, depth, width**.
2. **Voltage, wattage, volume, weight, and maximum recommended weight**.

### YOLOv8 (For Class 1)
- Class 1 images (height, depth, width) are processed using YOLOv8, where a fine-tuned CNN model identifies regions of interest to extract text.

### Image Preprocessing
- Applied to all images to enhance clarity, recover data loss, and handle noisy/blurry images.
- The goal is to make the images OCR-ready and improve text detection by EasyOCR.

### EasyOCR
- Applied to both Class 1 and Class 2 images after preprocessing to extract relevant text from the images.

### BERT (For Class 2)
- For Class 2 images (voltage, wattage, volume, etc.), the extracted text is passed to a fine-tuned BERT QA model.
- BERT processes the text in a question-answer format, with the extracted text as context and questions tailored to the specific attributes (e.g., "What is the voltage?").

### Python Script for Class 1
- The extracted text from Class 1 images is fed into a Python script designed to handle unit conversions, abbreviations, and correct errors in data.

## Challenges

1. **Small Resolution Images**:
   - Significant accuracy loss in text extraction and object detection due to differences in resolution between training (high-resolution) and test (low-resolution) datasets.

2. **Model Performance**:
   - YOLOv8 and EasyOCR struggled to handle the low-quality images in the test dataset, impacting overall performance.

## Conclusion

The pipeline successfully extracts meaningful information from images, though performance drops significantly on low-resolution test images. In future iterations, further model adjustments and advanced image enhancement techniques are required to handle varying image resolutions effectively.
