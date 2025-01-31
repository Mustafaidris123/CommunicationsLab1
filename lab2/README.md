# Exercise 1: AM Demodulators

There are two ways to demodulate an AM modulated signal:

**Coherent Demodulation**: Multiply the AM signal with the carrier signal and then use a low pass filter.

**Envelope Detection**: Rectify the AM signal, low pass-filter it and remove the DC component to obtain the envelope.

Both techniques will be used in two seperate VI modules **'AMCoherent.gvi'** and **'AMEnvelopeDetection.gvi'**.

## Exercise 1a: Coherent detection

Two demodulate the signal, first we open the **AMCoherent.gvi** file that was provided. Then by adding a multiply function to the diagram we can multiply an AM signal and carrier signal. The next step is to connect the output of the multiplier to a filter. The high frequencies must be filtered out so for that reason a butterworth low pass filter is used. The only thing left to do is to subtract the DC offset, which is obtained using the **Amplitude Mmeasurements Module**.

The mathematical proof behind this technique is shown below.

$$s(t) = (A_c+A_mcos(2 \pi f_m t)) cos(2 \pi f_c t) $$
$$s(t)cos(2 \pi f_c t) = (A_c + A_mcos(2 \pi f_m t)) (2cos(4 \pi f_c t) + 1)$$
Low pass filter is applied
$$f_l(s(t)cos(2 \pi f_c t)) = A_c + A_mcos(2 \pi f_m t) = DC+ m(t)$$
DC offset is removed
$$f_l(s(t)cos(2 \pi f_c t)) - DC = m(t)  $$


The result can then be viewed in both the time and frequency domain.

This module can now be transfered into a sub-VI, just like Exercise 3 of lab 1.

## Exercise 1b: Envelope detection
Envelope == 

## Exercise 2: AM Simulation

## Exercise 3: AM Communications via USRP

## Exercise 4: Listening to AM Music