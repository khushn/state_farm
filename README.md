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

#### Training on GPU

Tensorboard ran, but could not view it on port 6006 (perhaps security group changes did not take affect). But below are the end logs of training.

Also NOTE: The bulk of the time around over 1 hour was spent in just creating bottleneck files for the all the images 

<blockquote>
	0% (N=100)
INFO:tensorflow:2018-01-18 19:24:54.070764: Step 3990: Train accuracy = 85.0%
INFO:tensorflow:2018-01-18 19:24:54.071000: Step 3990: Cross entropy = 0.503428
INFO:tensorflow:2018-01-18 19:24:54.152726: Step 3990: Validation accuracy = 89.0% (N=100)
INFO:tensorflow:2018-01-18 19:24:54.900999: Step 3999: Train accuracy = 89.0%
INFO:tensorflow:2018-01-18 19:24:54.901243: Step 3999: Cross entropy = 0.409679
INFO:tensorflow:2018-01-18 19:24:54.983265: Step 3999: Validation accuracy = 88.0% (N=100)
INFO:tensorflow:Final test accuracy = 92.5% (N=2220)
INFO:tensorflow:Froze 2 variables.
Converted 2 variables to const ops.

</blockquote>


#### AMI Building
<blockquote>
	aws ec2 create-image --instance-id i-01595fe39f6a7d0b1 --name "kaggle_fast_ai_v2" --description "Used for Kaggle & DL" --no-reboot
</blockquote>


#### Classifying the test images
There is a problem with tensorflow transfer learning samples, in that the default code can only work on the images sequentially. When I tried to give the images in batches it gave an error implying it expects only 1 X 299 x 299 x 3 i.e. can't take ? x 299 x 299 x 3. Sample the below message in the notebook when I tried to give 2 images:

<blockquote>
	ValueError: Cannot feed value of shape (2, 299, 299, 3) for Tensor 'import/Mul:0', which has shape '(1, 299, 299, 3)'
</blockquote>

This issue has also been well documented here: 
https://github.com/tensorflow/tensorflow/issues/1021

There are some workarounds mentioned in the above link. But they don't look straightforward. So as a result, I am suspending this project here (noted on 25 Jan 2018)

