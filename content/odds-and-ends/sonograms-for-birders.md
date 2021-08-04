---
title: "Sonograms for Birders"
date: 2020-07-27T12:41:22+02:00
updated: 2020-07-27T12:41:22+02:00
tags:
 - birds
 - earbirding
draft: true
toc: true
---

Birding is just as much about listening to birds, as it is about looking at
birds. And just as being able to describe how birds look is valuable for
learning how to identify birds visually, being able to describe how birds sound
is valuable for learning how to identify birds by song or call.

Describing sounds with natural language is difficult, but by creating visual
representations of bird songs and calls with sonograms, we get something we can
see and talk about, and which can help us analyze songs and calls.

This article intends to give birders who are interested in understanding
sonograms, an overview of the underlying mathematics, science and technology
of sonograms. As part of the journey we will encounter two amazing mathematical
truths with deep implications for how we can analyze and understand, not only
bird songs and calls, but all signals of all kinds in the entire universe!

A sonogram [^1] is a visual representation of the spectrum of frequencies of a
signal as it varies over time.

[^1]: Sonograms are also sometimes called spectrograms, which is the more general
term, but I'll use the term sonogram, since I will be talking about spectrograms
for sound.

Ok, here we want to put a sidenote {{< sidenote-gvdb "1">}} This is so interesting it goes into a sidenote. {{< /sidenote-gvdb >}} that is really really interesting.

Ok, here we want to put a marginnote {{< marginnote-gvdb "1">}} This is so interesting it goes into a marginnote. {{< /marginnote-gvdb >}} that is really really interesting.

Ok, here we want to put a sidenote {{< sidenote-gvdb "2">}} This is even more interesting so it also goes into a sidenote. {{< /sidenote-gvdb >}} that is really really interesting.

# The challenge of listening to and recording birds

Bird songs and calls are seldome pure in the sense of clean, stable and well
defined sounds and notes. They are complex and consist of many different
frequencies, rapidly changing frequencies as well as rapid changes in loudness.
Birds have the physiological equivalent of two larynxes, which they can control
independently of each other and thus produce very complex sounds with.

To make it even more difficult for us as listeners, we usually have many other
sounds competing with the particular individual bird we're interested in
listening to, or in recording. Also, we don't always see the bird singing or
making calls, and in some cases in can be quite difficult to exactly pinpoint
the direction from where the song or call is coming from.

{{< youtube id="f4BwbAIRag0" autoplay="false" >}}

Occasionally we are lucky in not only seeing a bird, but also in hearing it
sing, or make calls, at the same time. Like the Nightingale thrush, _Luscinia
luscinia_, above, which I encountered in the Royal Djurgården park in Stockholm
(_May 19 2020_).

Nevertheless, every species has a repertoire of songs and calls that are
recognizable within the boundaries of variation. Furthermore, when we can look
at the frequencies by using sonograms of recordings of birds, we can _see_ the
distinctive features of their songs and calls in a way that our ears can't
always easily _hear_. And when we see those features we can discuss them and
we can use them mentally to assist us the next time we get a chance to listen
to that particular bird! And of course, if we do get a recording of a bird
flying past us that just uttered a few calls on its migratory journey and we
are unsure about which bird it was, we have a chance of analyzing that call
afterwards, by looking at the sonogram of the recording!

# A summary of the process from bird song to sonogram

I want to begin with the big picture and present the overall process from bird
song or call, to a sonogram.

1. **The source**: A bird sings, calls or chirps and the sound, consisting of
   aucustic waves travelling through the air, reaches a microphone.
2. **The recording**: The microphone transforms the aucustic wave to an
   electrical signal that has approximately the same wave shape as the
   aucustic wave. The better the microphone is, the better the approximation is.
   The electrical signal is also feed through a pre-amplifier that amplifies
   the electrical signal so it is stronger and better suited for manipulation in
   the following steps. A good preamplifier should amplify the original sound
   signal with miminal distortion and and also keep circuit noise to a minimum.
3. **The ADC (analog to digital conversion)**: The analog electrical signal is
   transformed into a discrete digital signal by a process called sampling.
   There are two aspects of the signal that are digitised. First of all the
   signal is sampled at distinct and evenly spaced points in time, decided by the
   chosen sampling frequency. Secondly, the sampled signal strength is quantized
   to discrete values of equal spacing, where the spacing is decided by the
   chosen resolution in bits and the peak signal strength. The digital signal
   is given a representation that can be stored as a digital recording in the
   form of a data file, e.g. a \*.wav file.
4. **The DFT (discrete Fourier transform)**: The digital signal is transformed
   from a function in the time domain to a function in the frequency domain.
5. **The sonogram plot**: The transformed DFT signal is plotted as a visual
   representation called a sonogram that shows the frequencies and their power
   in the digital recording, as they vary over time.
6. **The analysis**: We can look at the sonogram and correlate it to what we hear
   and compare it to other bird sonograms created from other recordings.

For step 1 we are at the mercy of birds and serendipity! For steps 2 and 3 we
need digital recording equpiment. A common smart phone will do, or we can buy
more expensive equipment. For steps 4 and 5, we need software, and there is both
costfree, free and open source software, as well as commercial and proprietary
software, for this today. For step 6 you are needed!

Even though this process and the underlying mathematics and technology is quite
advanced and may seem a bit daunting at first, all the needed equipment is
quite cheap and easy to use today, and once you have understood a few important
aspects of the overall process, you should have no problems att all in becoming
a capable sonogram ninja, in no time at all!

If you just want to get going at once, jump to the section [Ok, lets get
started](#ok-lets-get-started).
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
more pure sound by us and we talk about the pitch of the sound. Anyone who
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

# Ok, lets get started!

# Possiblities in Machine Learning and AI

* Automated recognition of bird songs and calls by using the information in the
  Fourier transforms of different species.
* Mobile apps that can take a recording and generate a nice sonogram.

# Further reading

TBD!
