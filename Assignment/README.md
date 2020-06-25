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

- Nên git pull branch master. Sau đó merge master vào branch của mình. Rồi mới commit và push code
- Các bạn có thể tham khảo code của nhau bằng cách switch sang branch của bạn khác. Nhưng **tuyệt đối** không được sửa code của người khác và commit lên

## Timeline
| Tuần | Ngày | Nội dung |
| -------      |  ------  |:---------|
| 1   | 25/05/2020   | Introduce to Machine Learning |
| 2 | 29/05/2020 | Your first model: Fashion MNIST|
| 3  |      01/06/2020    | Introduce to CNNs |
| 4  |     05/06/2020     | Overfitting problem |
| 5  |     08/06/2020     | Tranfer Learning |
| 6  |     12/06/2020     | Authentication |
| 7  |     15/06/2020     | The Workflow ò Machine Learning |
| 8  |     19/06/2020     | Summary |
| 9  |     22/06/2020     | Final Report |

