## Lung Infection Detection using CNN and Transfer Learning


## **Motivation**

I chose this project driven by my passion for applying AI for real-world applciations particularly in the healthcare space

Early and accurate detection of lung infections is crucial for preventing disease progression and improving patient outcomes. However, radiographic images are often complex and require expert interpretation, which may not always be accessible in low-resource settings.  

This project aims to develop an automated deep learning model capable of identifying lung infection patterns from medical images. By leveraging **Convolutional Neural Networks (CNNs)** and **transfer learning techniques**, the model supports medical professionals in diagnostic decision-making, reduces workload, and enhances screening efficiency.


## **Approach**


### **Data Exploration and Visualization**

- Examined image distribution across three classes — *Healthy*, *Type 1 disease*, and *Type 2 disease* — to understand class balance.

### **Preprocessing and Augmentation**
- Applied data augmentation (**random flips**, **rotations**, **rescaling**, and **resizing**) to increase dataset variability and improve model robustness.


## **Dataset Overview**
- **Training images:** 251  
- **Test images:** 66  
- **Classes:**  
  - Healthy  
  - Type 1 disease  
  - Type 2 disease  


## **Model Architecture**
- Built a **custom CNN** with three convolutional blocks followed by fully connected layers.
- Used **Glorot Normal (Xavier)** initialization for stable gradient flow.  
- Incorporated **Batch Normalization** and **ReLU activations** for faster convergence and improved performance.


## **Regularization and Optimization**
- Mitigated overfitting using **L2 regularization**, **Dropout**, and **Early Stopping** with validation monitoring to restore the best weights.  
- Compiled the model with **Categorical Crossentropy** loss and the **RMSprop** optimizer for stable optimization.

### Key challenge faced
-  Limited dataset caused the model to overfit.


## **Models Experimented**

### **1. Custom CNN (Baseline)**
- Simple CNN built with Conv2D, Batch Normalization, Dropout, and Dense layers (input size: 48×48).  
- **Optimizer:** RMSProp  
- **Loss:** Categorical Crossentropy  
- Achieved moderate accuracy but showed severe overfitting due to limited data.

- Initially used the pretrained weights directly. Later unfroze selected layers to fine-tune the model, adapting it to lung infection classes that differed from ImageNet categories.

### **2. MobileNet (Transfer Learning+ Fine-tuning)**
- MobileNet pretrained on ImageNet with frozen base layers and custom Dense + Dropout layers (input size: 224×224).  
- **Optimizer:** RMSProp  
- **Metrics:** Accuracy, F1 Score (~0.81)  
- Achieved ~85–90% accuracy and generalized well on small data.

### **3. DenseNet121 (Transfer Learning + Fine-Tuning)**
- DenseNet121 pretrained on ImageNet with custom top layers: Dense(1024) → Dropout → Dense(256) → Dropout → Dense(3, softmax).  
- **Optimizer:** Adam  
- **Metrics:** Accuracy, Precision, Recall, F1  
- **Performance:** ~98% accuracy, F1 ≈ 0.98 (best-performing model)

- Demonstrated excellent generalization across all classes, outperforming baseline and other pretrained models.


## **Future Work**
- Experiment with larger and more diverse datasets to improve robustness.  
- Explore attention-based architectures (e.g., Vision Transformers).  
- Incorporate explainable AI (Grad-CAM, LIME) for visual interpretability of predictions.  
- Deploy as a lightweight web or mobile diagnostic tool.

  

## **Tools Used**
- **TensorFlow** with **Keras API**  
- **NumPy**, **Matplotlib**, **Pandas** for data preprocessing and visualization  
- **Google Colab** for model training and experimentation


## License

This project is licensed under the Apache License 2.0.  
See the [LICENSE](LICENSE) file for details.
