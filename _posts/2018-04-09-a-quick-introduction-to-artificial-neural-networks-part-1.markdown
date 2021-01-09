---
layout: post
title:  A Quick Introduction to Artificial Neural Networks (Part 1)
description: Artificial neurons mimic the basic function of biological neurons, and much like their biological counterparts they only become useful when connected in a larger network, called Artificial Neural Networks...
date:   2018-04-09 15:01:35 +0000
image:  '/images/posts/2018/neuron-annotated.jpg'
tags:   [machine learning, neural networks]
---

<style>p { text-align: justify; }</style>

*Update*: Since 2018 I have created better resources for those interested in machine learning. Head over to <a href="https://security.kiwi">this course on mahcine learning</a> which covers neural networks.

### Artificial Neural Networks
Artificial neurons mimic the basic function of biological neurons, and much like their biological counterparts they only become useful when connected in a larger network, called Artificial Neural Networks. 

Neural networks are extremely adept at recognising patterns, this is pattern recognition is the reason they have become so widely used and talked about in recent years. The ability of neural networks to discover and recognise patterns allows them to far surpass traditional methods in computer science, making them viable for use in research and business.

### An Artificial Neuron
The image below show an illustration of a single biological neuron annotated to describe a single artificial neurons function.

![](/images/posts/2018/neuron-annotated.jpg)

A biological neuron receives input signals from its dendrites from other neurons and sends output signals along its axon, which branches out and connects to other neurons. In the illustration above, the input signal is represented by `x0`, as this signal ‘travels’ it is multiplied (`w0 x0`) based on the a weight variable (`w0`). The weight variables are learnable and the weights strength and polarity (positive or negative) control the influence of the signal. The influence is determined by summing the signal input and weight (`∑i wi xi + b`) which is then calculated by the activation function f, if it is above a certain threshold the neuron fires.

### Activation Functions in Brief
The frequency of the firing of an artificial neuron is determined by an activation function. It determines at what threshold the neuron will fire. This section describes the Sigmoid activation function to bring clarity to the operation of an artificial neuron. Activation functions will be discussed in detail further on in this guide.

![](/images/posts/2018/sigmoidexample.jpg)

The graph above shows the Sigmoid activation function, which will convert all input signals into positive values between 0 and 1. The use of other activation functions with wider values, or negative values change the frequency of the firing of a neuron and will suit different types of data and purposes.

Activation functions are dicussed in further detail in the final quick introduction post, [part two](/a-quick-introduction-to-artificial-neural-networks-part-2).
