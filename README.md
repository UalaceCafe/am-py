# am-py
A naïve AM/Tremolo effect for _.wav_ audio files written in Python 

## What is it?
_am-py_ is a simple study of Amplitude Modulation (more specifically, as it was initially intended, Tremolo effect) using Python, scipy, numpy and matplotlib.

Although I'm a long time programmer, this is my first _real_ python code, so the implementation is quite naïve. However, it has been tested on
a few recordings of mine, including a cover of the song _Do I Wanna Know?_, by the _Arctic Monkeys_.

## How to use it?
```python
IN_FILE = "input.wav"
OUTL_FILE = "outl.wav"
OUTR_FILE = "outr.wav"
```
Change _IN_FILE_, _OUTL_FILE_ and _OUTR_FILE_ to how you called your input file, and to how you want to call your left channel output file and your right channel output file, respectively. Note that _all_ of them must be in _.wav_ format.

The modulating wave (carrier) is created with the following lines of code:

```python
CARRIER_FREQ = 8.0
DEPTH = 0.6
carrier = np.cos(2 * np.pi * CARRIER_FREQ * time)
carrier = map(carrier, -1.0,  1.0, 1 - DEPTH, 1.0)
```

* _CARRIER_FREQ_, as the name suggests, is the frequency of the carrier wave in _Hertz_. A value between 1.0 and 25.0 is usually recommended for a Tremolo effect. Too high of a frequency will make it sound robotic; unless that is your intetion, of course.
* _DEPTH_ determines the range (i.e., the intensity) of the effect, from subtle variations to completely deadening the signal. It is supposed to range from 0.0 to 1.0, where 0.0 means no depth (i.e., no effect) and 1.0 is maximum intensity.

At the end, these two lines of code will generate the left channel and right channel _.wav_ files:
```python
wavfile.write(OUTL_FILE, samplerate, left_mod.astype(np.int16))
wavfile.write(OUTR_FILE, samplerate, right_mod.astype(np.int16))
```
