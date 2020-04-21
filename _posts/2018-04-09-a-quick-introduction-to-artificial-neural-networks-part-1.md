---
layout: post
title: "A Quick Introduction to Artificial Neural Networks (Part 1)"
tags: [ Practical Deep Learning Fundamentals ]
featured_image_thumbnail: assets/images/posts/2018/neuron-annotated.jpg
---

### Artificial Neural Networks
Artificial neurons mimic the basic function of biological neurons, and much like their biological counterparts they only become useful when connected in a larger network, called Artificial Neural Networks. 

Neural networks are extremely adept at recognising patterns, this is pattern recognition is the reason they have become so widely used and talked about in recent years. The ability of neural networks to discover and recognise patterns allows them to far surpass traditional methods in computer science, making them viable for use in research and business.

### An Artificial Neuron
The image below show an illustration of a single biological neuron annotated to describe a single artificial neurons function.

![](assets/images/posts/2018/neuron-annotated.jpg)

A biological neuron receives input signals from its dendrites from other neurons and sends output signals along its axon, which branches out and connects to other neurons. In the illustration above, the input signal is represented by `x0`, as this signal ‘travels’ it is multiplied (`w0 x0`) based on the a weight variable (`w0`). The weight variables are learnable and the weights strength and polarity (positive or negative) control the influence of the signal. The influence is determined by summing the signal input and weight (`∑i wi xi + b`) which is then calculated by the activation function f, if it is above a certain threshold the neuron fires.

### Activation Functions in Brief
The frequency of the firing of an artificial neuron is determined by an activation function. It determines at what threshold the neuron will fire. This section describes the Sigmoid activation function to bring clarity to the operation of an artificial neuron. Activation functions will be discussed in detail further on in this guide.

![](assets/images/posts/2018/sigmoidexample.jpg)

The graph above shows the Sigmoid activation function, which will convert all input signals into positive values between 0 and 1. The use of other activation functions with wider values, or negative values change the frequency of the firing of a neuron and will suit different types of data and purposes.

Activation functions are dicussed in further detail in the final quick introduction post, [part two](/a-quick-introduction-to-artificial-neural-networks-part-2).

----

This blog post was created using the content from Chapter 4 of my book, [Practical Deep Learning Fundamentals](practical-deep-learning-fundamentals/). The chapter describes artificial neural networks in an easy to understand manner, with minimum math and full explanation of the math that is required. Practical exercises lead the reader through the implementation of a single layer neural network in the Python machine learning library Scikit-learn.