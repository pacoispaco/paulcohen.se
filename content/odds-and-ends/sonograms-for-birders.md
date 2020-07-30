---
title: "Sonograms for Birders"
date: 2020-07-27T12:41:22+02:00
updated: 2020-07-27T12:41:22+02:00
draft: true
---

Birding is just as much about listening to birds, as it is about looking at
birds. And just as visually describing birds is important for being able to
visually recognize and identify birds, audial descriptions are important for
being able to audially recognize and identify birds. Describing sounds with
natural language is difficult, but by creating visual representations of bird
songs and calls with sonograms, we have a nice tool for both talking about
and visually analyzing songs and calls.

This article explains what sonograms are and how they can be used bya birders.
A sonogram is a visual representation of the spectrum of frequencies of a
signal as it varies over time. Sonograms are also sometimes called
spectrograms, which is the more general term, but I'll use the term sonogram,
since I will be talking about spectrograms for sound. This article intends to
give birders who are interested in understanding sonograms, an introduction to
the underlying mathematics, science and technology of sonograms!

As part of the journey we will encounter two amazing mathematical truths with
deep implications for how we can analyze and understand, not only bird songs and
calls, but all signals of all kinds in the entire universe!

# The challenge of listening to and recording birds

We know that bird songs and calls seldom are pure in the sense of clean stable
and well defined sounds and notes. They are complex and usually consist of many
different frequencies, rapidly changing frequencies and as well as rapid changes
in loudness. Birds have the physiological equivalent of two larynxes, which they
can control independently of each other and produce very complex sounds with.

To make it even more difficult for us as listeners, we usually have many other
sounds competing with the particular individual bird we're interested in
listening to, or in recording.

Nevertheless, every species has a repertoire of songs and calls that are
recognizable within the boundaries of variation. Furthermore, when we can look
at the frequencies by using sonograms of recordings of birds, we can see the
distinctive features of their songs and calls in a way that our ears can't
easily do.

# Sound and Analog Electrical Signals

Sound is a vibration that propagates as an acoustic wave, in the form of rapid
compression and decompression of some transmission medium, such as air or
water. Sound is characterized by two fundamental properties, amplitude and
frequency.

The distance between the higest value of compression and the lowest
value of decompression, is called the **amplitude** of a wave. A sound that
has a large amplitude for a period of time is percieved by us as a
loud sound. If a wave has a regular pattern of compression and decompression
over time where the distance between successive peaks of compression is
constant, we say that the wave has a constant **frequency**. A sound consisting
of only one reasonably stable frequency over time is percieved as a cleaner and
more pure sound by us and we talk about the **pitch** of the sound. Anyone who
has tried singing or playing the violin will know the the difficulty of
producing a clear sound of a given pitch.

Sound vibrations can be picked up by our ears or by a sensor, such as a
microphone, and turned into an analog electrical signal. An analog electrical
signal has an amplitude which varies over time, and thus contains information
about the sound.

An analog electrical signal contains all the information about the recorded
sound, except for what is limited by the physical properties of the sensor,
such as its sensitivity, its directional capabilities and the speed and fidelity
with which it can convert sound waves to electrical signals.

Analog electrical signals can then be manipulated in many interesting and fun
ways, but for practical purposes, we usually convert the analog signals to
digital signals and then store and manipulate the recorded sounds as digital
signals.

# Signals as mathematical curves and functions

Aucoustic and electrical signals that have an amplitude that changes over time
can be described as graphs of functions, where the amplitude **y** is the value
of a function **f** over time; **y = f(t)**.

> Astonishing fact 1: Every complex wave can be completely represented by a sum of pure sine waves!

# Analog and Digital Signals

The process of converting an analog electrical signal to a digital signal is
called sampling. There are two important parameters to consider when sampling;
the **resolution when converting the amplitude to a digital value**, and the
**rate of sampling over time**. Intuitively, we realize that a higher
resolution will capture more **details of the different amplitudes in the
original signal**, and a higher sampling rate will capture more of the
**details of amplitude changes in the original signal**. Thus, the sampling
resolution and rate have a direct influence on how much information from the
original analog signal is retained in the digital signal.

# Digital Encoding and Information Theory

TBD!

> Astonishing fact 2: The Nyquist-Shannon sampling theorem establishes a sufficient condition for a sample rate that permits a discrete sequence of samples to capture all the information from a continuous-time signal of finite bandwidth!

The Nyquist–Shannon sampling theorem is a theorem in the field of digital signal processing which serves as a fundamental bridge between continuous-time signals and discrete-time signals. It establishes a sufficient condition for a sample rate that permits a discrete sequence of samples to capture all the information from a continuous-time signal of finite bandwidth.

# Tools for manipulating recordings and creating sonograms

TBD!

# Possiblities in Machine Learning and AI

* Automated recognition of bird songs and calls by using the information in the
  Fourier transforms of different species.
* Mobile apps that can take a recording and generate a nice sonogram.

# Further reading

TBD!
