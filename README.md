### Notes

#### Training

<blockquote>
	python tensorflow/examples/image_retraining/retrain.py --image_dir ../data/samples/train/
</blockquote>


#### Tensorboard
<blockquote>
	tensorboard --logdir retrain_logs/
</blockquote>

Tensorboard view:
<image src="tensorboard_1.png"/>


#### Testing

<blockquote>
	python tensorflow/examples/label_image/label_image.py --input_layer=Mul --output=final_result --graph=../output_graph.pb --labels=../output_labels.txt --image=../data/sample/valid/c5/img_97543.jpg
</blockquote>

