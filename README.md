# CSE 461 final project - Thorne Garvin

# Problem Description

The problem I worked on for the final project was the Kaggle Bird Classification competition. For the competition, we had to train a neural network based classifier on images of birds and then submit our predictions for the test dataset to the competition webpage.

# Previous Work

While I tried out a half-dozen potential models for transfer learning, what I ended up using was ResNet50, which was originally created in 2015. ([paper](https://arxiv.org/abs/1512.03385). ResNet50 is both small enough to be trained quickly and powerful enough to create a good fit for the relatively challenging bird dataset, which was too complex for weaker versions of ResNet like ResNet18 and ResNet34. ResNet50 and its cousins were the first mainstream neural networks to use residual learning, which marked a paradigm shift in neural network creation. For my project, I used a version pretrained on the ImageNet dataset by PyTorch.

# My Approach

I didn't know a lot about how neural networks worked, or even how to use them, when I started this project, so my approach was simple: I wanted to use a pretrained neural network as my base, and build a code framework that let me easily re-train that network over the bird images to produce a fine-tuned classifier. My basic strategy was to iterate over a number of possible candidate network architectures until I found one that minimized loss when trained over a small number of epochs, then develop a robust learning rate schedule and train over a larger number of epochs. I also experimented with feature extraction (only allowing the weights in the last, fully connected layer of the network to change) but I ultimately found that it was universally worse than fine-tuning (re-training the entire network with the new data) for this application.

# Datasets

 - ImageNet
 - Birds dataset (available at competition page)

# Results

As of right now (10:00 PM 3/17/21), my highest-rating prediction on the public subset of the test images sits at 81% accuracy.

# Discussion

This was a super enjoyable and productive project for me as someone who had literally never touched neural networks/ML code before this, and it was super challenging to wrap my head around what was happening even at the most basic level. Ultimately, I think I was able to get a good grasp on the basics, which is why I was able to crack 80% accuracy. However, I had to play catch-up during the initial phases of this project and spent a lot of time flailing around in the ~50% accuracy range doing trial and error before I finally took the time to read up on the relevant material.

There were a number of approaches I think could've produced a significant improvement in my results 
 - I considered but scrapped the idea of pre-processing all of the images to make data loading faster and/or storing the images in an hdf5 file to allow accessing them from memory. Training the network for 30-50 epochs, which was what I determined was doable and relevant, was already very possible without any dataloader optimizations.
 - I also did not pursue, but probably should have, altering the input images beyond simply horizontally flipping them.
 - I gave up on training google's inceptionNetv3, even though it should've been more powerful than ResNet50 and fit on the GPU, because I couldn't get it to train well over 5-10 epochs. 

Here are screenshots of my attempts at training Inception, which went terribly. Loss is on the Y axis, epochs on the X.
![Failed Attempt #1](https://i.imgur.com/5E6coBy.png)
![Failed Attempt #2](https://i.imgur.com/Zv6hz31.png)

For comparison, here's resnet18:
![Resnet](https://i.imgur.com/qw6GIs1.png).

Ultimately, I think I gave up on InceptionNet slightly prematurely. At the point in the project where I gave up on InceptionNet and went back to ResNet, I didn't really understand how to create a useful learning rate schedule for training, nor did I have a good ballpark for how many epochs I would need to train for to produce a good result. If I had stuck with InceptionNet for longer and/or come back to it later, I have no doubt I could've gotten higher accuracy with it.

With all that said, I could've gotten a significantly better result with the knowledge I had gained by the end of the project if I had more time to continue to work, but I unfortunately ran out of time by monday and had to switch to working on different projects/exams.

With regards to the uniqueness of my approach, I don't believe my approach was particularly unique, but I do think it was a solid example of the basics and definitely better than attempts at using more complicated/larger networks that weren't as fundamentally solid.

Finally, this is entirely unrelated to my project, but I just wanted to say that this was one of my favorite classes I've ever taken at UW! Thank you to the instructor and staff for a great time!
