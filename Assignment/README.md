# Sử dụng mô hình DETR để xác định người đeo khẩu trang trong ảnh 

Bài toán này sử dụng mô hình Detection Transformer (DETR) được giới thiệu trong [paper](https://arxiv.org/pdf/2005.12872.pdf) của nhóm những nhà nghiên cứu trong đội ngũ [FacebookAI](https://ai.facebook.com/research/publications/end-to-end-object-detection-with-transformers)

## Bộ dữ liệu

Nhóm mình tạo 2 bộ dataset với những đặc trưng riêng biệt: 
 - [Một bộ](https://drive.google.com/drive/folders/1XUR4ci88ABahff3TOxoT9GuxbjP7NwCq?usp=sharing) gồm những hình người đeo khẩu trang ở nhiều góc độ khác nhau. Được trích từ [đây](https://www.kaggle.com/andrewmvd/face-mask-detection)
 - [Một bộ](https://drive.google.com/drive/folders/1i0aN3Si202GC6c08WJGYs3GKIJNUB-dY?usp=sharing) gồm nhiều hình chân dung được thêm khẩu trang tự động. Được trích từ [đây](https://www.pyimagesearch.com/2020/05/04/covid-19-face-mask-detector-with-opencv-keras-tensorflow-and-deep-learning/)

Bộ dữ liệu đầu vào được xây dựng theo cấu trúc bộ dữ liệu của [http://cocodataset.org](http://cocodataset.org/#download) năm 2017:
```
path/to/dataset/
  annotations/  # annotation json files
  train2017/    # train images
  val2017/      # val images
```


## Training



Đầu tiên, clone repository mô hình DETR về máy:
```
git clone https://github.com/facebookresearch/detr.git
```
Cài đặt PyTorch 1.5+ and torchvision 0.6+:
```
conda install -c pytorch pytorch torchvision
```
Cài đặt pycocotools and scipy:
```
conda install cython scipy
pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
```
Tải [pretrained model](https://drive.google.com/file/d/1LOjGPqkPvBUWLjF_gQsU9Kt0n_QB9uvq/view?usp=sharing) đã được lược bỏ phần classification head

Training bộ dữ liệu mới từ checkpoint sẵn có
```
python main.py --coco_path /PATH/TO/DATASET --epochs /NUM/OF/EPOCHS --batch_size= /YOUR/BATCH/SIZE --output_dir= /YOUR/OUTPUT/FOLDER --resume="detr-r50_no-class-head.pth"
```

## Models


- Nhóm mình sử dụng bộ dữ liệu 1 để train model với 110 epochs và kết quả tốt nhất là:

  <img src="https://i.ibb.co/CK7h4Rm/dataset11.png" width="600">

Model nằm [tại đây]()


- Đối với bộ dữ liệu thứ 2, tụi mình train qua 500 epochs và thu được kết quả như sau:

 <img src="https://i.ibb.co/rpG0bTX/dataset1.png" width="600">

Model nằm [tại đây](https://drive.google.com/file/d/1-cIrb326EOhvPYltzN8Kjab_JNCCq6pn/view?usp=sharing)

