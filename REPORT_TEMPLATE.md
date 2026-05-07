# CSC4005 - Lab 2 Report

# CNN Image Classification: From Scratch vs Transfer Learning

---

## Student Information

* Name: Nguyễn Thành Duy
* Student ID: manhduy04
* Course: CSC4005
* Lab: Lab 2 - CNN Image Classification

---

# 1. Introduction

Trong bài lab này, mục tiêu là xây dựng và đánh giá mô hình phân loại ảnh sử dụng Convolutional Neural Networks (CNN) trên bộ dữ liệu NEU Surface Defect Database.

Bài lab gồm hai hướng tiếp cận:

1. CNN from scratch
2. Transfer Learning với ResNet18

Mục tiêu chính:

* Hiểu cách hoạt động của CNN.
* So sánh hiệu năng giữa mô hình tự xây dựng và pretrained model.
* Phân tích learning curves và hiện tượng overfitting.
* Làm quen với Weights & Biases (W&B).

---

# 2. Dataset

Dataset sử dụng:

* NEU Surface Defect Database (NEU-CLS)

Dataset gồm nhiều loại lỗi bề mặt thép khác nhau.

Ví dụ các lớp:

* Crazing
* Inclusion
* Patches
* Pitted Surface
* Rolled-in Scale
* Scratches

Mỗi ảnh được resize về kích thước:

```text
64 x 64
```

Dữ liệu được chia thành:

* Train set
* Validation set
* Test set

---

# 3. Environment Setup

## Libraries

Các thư viện chính:

```python
PyTorch
Torchvision
NumPy
Matplotlib
Weights & Biases
```

## Install

```bash
pip install -r requirements.txt
```

---

# 4. CNN From Scratch

## Model Architecture

Mô hình CNN from scratch gồm:

* Convolution layers
* ReLU activation
* MaxPooling
* Dropout
* Fully Connected layers

Cấu hình:

| Parameter     | Value |
| ------------- | ----- |
| Optimizer     | AdamW |
| Learning Rate | 0.001 |
| Batch Size    | 32    |
| Epochs        | 20    |
| Dropout       | 0.3   |
| Image Size    | 64    |

## Training Command

```bash
python -m src.train --data_dir D:/datasets/NEU-CLS.zip --project csc4005-lab2-neu-cnn --run_name cnn_small_baseline --model_name cnn_small --train_mode scratch --optimizer adamw --lr 0.001 --weight_decay 0.0001 --dropout 0.3 --epochs 20 --batch_size 32 --img_size 64 --patience 5 --augment --use_wandb
```

---

# 5. Transfer Learning

## Pretrained Model

Trong phần này sử dụng:

```text
ResNet18
```

ResNet18 đã được pretrained trên ImageNet.

Chỉ fine-tune phần classifier cuối.

## Configuration

| Parameter     | Value  |
| ------------- | ------ |
| Optimizer     | AdamW  |
| Learning Rate | 0.0001 |
| Batch Size    | 32     |
| Epochs        | 10     |
| Dropout       | 0.3    |
| Image Size    | 64     |

## Training Command

```bash
python -m src.train --data_dir D:/datasets/NEU-CLS.zip --project csc4005-lab2-neu-cnn --run_name resnet18_transfer --model_name resnet18 --train_mode transfer --optimizer adamw --lr 0.0001 --weight_decay 0.0001 --dropout 0.3 --epochs 10 --batch_size 32 --img_size 64 --patience 5 --augment --use_wandb
```

---

# 6. Results

## CNN From Scratch

| Metric               | Result |
| -------------------- | ------ |
| Training Accuracy    | ...    |
| Validation Accuracy  | ...    |
| Test Accuracy        | ...    |
| Best Validation Loss | ...    |

### Observations

* Training loss giảm ổn định theo epoch.
* Validation accuracy tăng dần.
* Có dấu hiệu overfitting nhẹ ở các epoch cuối.

---

## Transfer Learning

| Metric               | Result |
| -------------------- | ------ |
| Training Accuracy    | ...    |
| Validation Accuracy  | ...    |
| Test Accuracy        | ...    |
| Best Validation Loss | ...    |

### Observations

* Model hội tụ nhanh hơn.
* Accuracy cao hơn CNN scratch.
* Validation loss ổn định hơn.
* Ít overfitting hơn.

---

# 7. Learning Curves

## CNN Scratch

Chèn ảnh learning curves từ W&B.

Bao gồm:

* Train Loss
* Validation Loss
* Train Accuracy
* Validation Accuracy

---

## ResNet18 Transfer

Chèn ảnh learning curves từ W&B.

Bao gồm:

* Train Loss
* Validation Loss
* Train Accuracy
* Validation Accuracy

---

# 8. Comparison

| Model             | Accuracy | Training Speed | Overfitting |
| ----------------- | -------- | -------------- | ----------- |
| CNN Scratch       | ...      | Medium         | Medium      |
| ResNet18 Transfer | ...      | Fast           | Low         |

## Analysis

Transfer Learning cho kết quả tốt hơn vì:

* ResNet18 đã học đặc trưng từ ImageNet.
* Khả năng trích xuất feature mạnh hơn.
* Hội tụ nhanh hơn.
* Generalization tốt hơn.

CNN from scratch vẫn hoạt động tốt nhưng cần:

* nhiều epoch hơn
* nhiều dữ liệu hơn
* tuning kỹ hơn

---

# 9. Weights & Biases Tracking

Project W&B:

```text
https://wandb.ai/duy19912745-dainam-vietnam/csc4005-lab2-neu-cnn
```

W&B được sử dụng để:

* Theo dõi metrics
* Visualize learning curves
* So sánh experiments
* Lưu hyperparameters

---

# 10. Challenges

Một số khó khăn gặp phải:

* Cài đặt môi trường PyTorch.
* Login W&B.
* Quản lý đường dẫn dataset.
* Điều chỉnh learning rate phù hợp.
* Giảm overfitting.

---

# 11. Conclusion

Trong bài lab này:

* Đã xây dựng thành công CNN from scratch.
* Đã áp dụng Transfer Learning với ResNet18.
* So sánh được hiệu năng giữa hai phương pháp.
* Làm quen với experiment tracking bằng W&B.

Kết quả cho thấy:

* Transfer Learning đạt accuracy cao hơn.
* Hội tụ nhanh hơn.
* Generalization tốt hơn CNN scratch.

---

# 12. References

1. PyTorch Documentation
2. Torchvision Models
3. Weights & Biases Documentation
4. NEU Surface Defect Database
