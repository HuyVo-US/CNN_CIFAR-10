**CNN TRAINING PIPELINE FOR CIFAR-10 (NPU-ORIENTED DESIGN)**
===============================================================================

**Mục tiêu:**

    - Huấn luyện mô hình CNN cho bài toán Image Classification (CIFAR-10)
    - Thiết kế kiến trúc phù hợp để triển khai trên NPU tự thiết kế (Verilog)
    - Target FPGA: Terasic DE10-Standard (Cyclone V)

**Đặc điểm thiết kế (Hardware-aware):**

    - Chỉ sử dụng các phép toán cơ bản:
        + Convolution (3x3)
        + ReLU
        + MaxPooling
        + Fully Connected
    - Tránh các layer phức tạp (Dropout, Residual, Attention)
    - Kiến trúc gọn nhẹ, dễ mapping sang phần cứng

**Pipeline:**

    1. Load & preprocess CIFAR-10
    2. Data augmentation (train)
    3. Xây dựng CNN model
    4. Training (AdamW + Cosine LR)
    5. Lưu best model
    6. Evaluate & phân tích kết quả

**Triển khai phần cứng:**

    - Fuse BatchNorm vào Conv
    - Quantize về INT8
    - Export weights → HEX
    - Mapping sang NPU (Verilog)
