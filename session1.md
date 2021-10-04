# Session 1: Sound Part One

# Oscillation

- Fundamental basis of all periodic phenomena
- Not just useful for sounds, but also images
- `sin(x)` function creates a sine wave
- This is a wave, or waveform
- `maxiOsc` object

## Air moving

- Wave goes above 0. --> Speaker moves forward
- Wave goes below 0. --> Speaker moves backward
- when the value of the wave is over 1 or below -1, you're in distortion
- i.e. the speaker can't move any further, so the waveform is clipped.

_The position of the speaker is the PHASE of the wave._

## All about time

- Both sound and video are time based
- Interesting fusion occurs around 20Hz
- Getting things to happen at the right time is an important computational problem

## Frequency

Waves don’t just have a phase. They also have _frequency_

- This is how often they move up and down each second - measured in hertz (hz) (also called 'Cycles Per Second (cps)').
- Waves that oscillate more than around 20 times per second take on a quality of continuos sounds, and not separate pulses
- Interestingly, the same is roughly true for images (fps)
- Oscillations below 20hz are called “Low Frequency” (LFOs)

## Frequency 2

- It's generally considered that humans can't hear oscillations with freqencies over 20000hz (20KHz)
- This very often changes with age, reducing as hearing definition decreases (as hair cells in the Cochlea cease to function).
- It order to digitally represent any periodic oscillation, we need to take **at least** two measurements, or 'samples' (one for each peak phase position).
- This is why your digital audio system is considered most effective if it has a samplerate of at least twice the maximum frequency you can hear (e.g. 44100hz, 48000hz etc.)
- The samplerate is the number of times per second that your system can measure (record) or reproduce (play back) the amplitude value of a signal
- The maximum frequency your system can reproduce is half the samplerate, called the _Nyquist Frequency_. The samplerate is also equal to the _Nyquist Rate_, which everybody finds confusing.
- Remember - **the rate is twice the frequency**, even when it's the Nyquist rate. But the rate is **never** the Nyquist Frequency
- You should probably check the samplerate of your audio hardware when programming audio systems, and make sure you at least know what it is. It will cause you problems if you forget that it exists.

## Amplitude

Waves also have an amplitude.

- This is how much they move up and down.
- In the real world, this is how much air they are moving.
- The speaker reproduces this process based on the computer's representation
- Remember, when the amplitude value of the wave is over 1 or below -1, you're in distortion
- In the computer, we have a different situation in that it can be more, and we can clip on purpose, for example to change the nature of the wave.

## Amplitude 2

- When we take a measurement of an oscillation (a sample), we store the value of the sample using a number of bits.
- 8 bit gives you a potential 256 values to represent the amplitude. This isn't great (although I like it).
- Most people agree that 16 bits per sample is fine. This gives you 65,536 numbers with which to encode a floating point value between 1 and -1.
- Many modern audio systems have much higher bitrates and sample rates.
- Reducing the bitrate is lots of fun and you should try it. You can use quantisation for this which is pretty simple to do by accident.

## Adding sounds together

- In the computer, the audio output should vary between -1 and 1
- This is a linear measurement, not in dB - i.e. not logarithmic
- `dB = Math.log10(linear_volume)*10`, which means linear val 1 == 0dB, 0.5 = -3.010. It's times 10 because a deciBel is a tenth of a Bel.
- Let me know if you want me to bore your pants off about this.
- When you add sounds, they combine linearly and can create distortion
- At maximum, `1+1=2` ...which will cause clipping

## Combining sounds in different ways

- When we add sounds together, strange things happen
- The sounds interfere with each other
  - Beating
  - Amplitude modulation - (multiplication)
  - Frequency modulation - (controlling frequency with another oscillator)
  
## Beating
- When two sinewave oscillators of different frequencies are added together, they interact to alter the amplitude
- This is because they cycle across each other. Sometimes, one will be at -1, while the other is at 1
- So the result becomes 0 at these points
- What you hear is the sound fading in and out.
- We call this 'beating'
- The beat frequency (how often it fades in and out) is equal to the difference between the two input frequencies.
  
## Amplitude Modulation

- A common example of amplitude modulation (AM) is when we multiply two sinusoidal oscillators together
- The output is two signals whose frequencies are the sum and the difference of the two input frequencies
- So if you multiply two sine waves together with frequencies of 400hz & 500hz, you will instead hear 900hz and 100hz

## Frequency Modulation 1
- We can use the output of a sinewave oscillator to control the frequency of another
- We do this by setting the frequency of the carrier oscillator, and adding the output of the second oscillator (the modulator) to it.
- If we don't change the amplitude of the modulator, not much will happen, because it will simply be adding a value between 1 and -1
- When we increase the amplitude of the modulator (i.e. change the 'modulation index'), this doesn't change the amplitude of the carrier - the sound output doesn't get louder
- Instead, the frequency of the sound changes in predictable, but nonetheless, very exciting ways
## Frequency Modulation 2
- If the frequency of the modulator is greater than the threshold of pitch perception (20 hz), increasing the modulation index makes the sound brighter
- **i.e. the frequency content of the signal increases in complexity as you increase the modulation index**
- The higher the modulation index, the more sidebands are created, increasing the brightness of the sound
- If the carrier and modulator are factors or multiples of each other, there is less beating (the sounds are harmonics of one another).
- If not, there is increased beating (the sounds are inharmonic) and eventually, noise (they become highly complex).
- You can use this technique to do lots of things, including generating pseudo-random numbers.
- John Chowning demonstrated that you could theoretically use this technique to simulate almost any sound with enough parameterised modulators.
- https://ccrma.stanford.edu/people/john-chowning
- https://ccrma.stanford.edu/sites/default/files/user/jc/fm_synthesis_paper.pdf

# Session #1 Homework

Make sure you're familiar with how the MIMIC platform works.

Make sure you have created an account on the MIMIC platform.

Make a fork of this document if you want the simplest possible starting example :

https://mimicproject.com/code/8e5728dd-2eb9-02a9-9cb8-63d3731bba68

Or if you want to use the visualisation, use this one.

https://mimicproject.com/code/69704316-d8d8-7623-f0c6-316cb983f0b9

Or one of the examples frmo this page, which are a bit more fully featured :-)

https://mimicproject.com/guides/maximJS

Use either as a basis for carrying out the following tasks:

- Using at least 4 oscillators, create a continuous, drone-based sound texture or sound bed.

- Use two of the oscillators to control parameters of the other two oscillators.

- Make the sound texture vary continuously over a period of 1 minute through the use of low-frequency oscillators, so that the sound texture develops over the entire period.

Further reading:
- Follow Chris Kiefer and Louis McCallum's tutorial on the Mimic platform: https://mimicproject.com/guides/maximJS
- Read this useful article from izotope on bit resolution and sampling rate
-- https://www.izotope.com/en/learn/digital-audio-basics-sample-rate-and-bit-depth.html
