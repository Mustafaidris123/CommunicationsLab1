# Converting from Fahrenheit to Celsius
The first task is to take a string as an input, convert each character into an integer using ASCII and store that in an array. Then convert each of those integers from fahrenheit to celsius using the formula 
$$celsius = (fahrenheit - 32) / (1.8)$$

First, the conversion into celsius is done by subtracting each fahrenheit value by 32. Then, we divide each of those values by 1.8. The divide operation must be done in floating point. The diagram below shows the full circuit which converts a string into a number of celsius values
![celsius_img](celsiusconverter.png)

Here is the result of running the simulation

![celsius data](celsiusata.png)

Now, we can compute the average temperature by diving the sum by the number of elements in the array

![average data](averagetemp.png)
![average](avgdatatest.png)

We can check if it's hot by seeing if the average temperature is greater than 50

![hot image](hot_img.png)

![colddata](hot_data.png)
![hotdata](hotdata2.png)


# Task 2: Central limit theorem

We can observe the central limit theorem using a mixture of count controlled loops and condition controlled loops. 

![calculatingsamplemean](sample_mean_circuit.png)

In the image above, a 2D array of randomly generated numbers (between 0-1) are generated using a nested for loop. The total number of elements is the product of each loop's "N" value. In this case, 10 * 10 = 100. Therefore, we divide the sum of the elements by 100 to obtain our sample mean. The program will then repeat this process to produe a different sample mean until the "stop" button is pressed".

The following image shows the result of running.

![samplemeanresults](sample_mean_data.png)

the sample mean (in this case 0.500562) is very close to the expected value (0.5). Most samples are expected to have a mean very close to the theoretical mean.


The results over time can be viewed using a histogram, we need to start by storing the sample mean from each iteration using an array. This can then be used as an input to the "signal" node on the histogram component. The "number of bins" node on the histogram refers to 
![histogram](histogram_generator.png)


An initial simulation with the number of bins set to 100 gives the following result

![histogramdata](histogram_data.png)

You can see clearly that most of the data is concentrated around ~0.5 and the overall shape of the curve resembles the gaussian distribution.

The next step would be to end the while loop when it has iterated a certain number of times. This can simply be done by comparing "i" with the total number of iterations.

![histogram](histogram_gt.png)

Now The simulation will be carried out again but this time, the number of bins = 10 and the number of iterations has been set to 1000

![histogram data 2](histogram_data_gt.png)

Now, we'd like to change the code so the final distribution observed is a histogram that is standard normal. The mean must be 0 and the standard deviation must be 1.

We can convert out distribution to a normal distribution using the following formula

$$Z = (X-\mu)/\sigma$$

This formula can either by applied after the sample mean has been taken, or during the sampling.

In both cases $$\mu = 0.5$$

However the standard deviation will be different.

During the sampling process

$$\sigma = (1-0)/\sqrt12 = 1/\sqrt12$$

After the samples have been taken

$$\sigma = (1-0)/(\sqrt(12n)) = 1/(10\sqrt12)$$

Therefore, the formula is

$$Z = (X - 0.5)(\sqrt(12n)) $$

where n = 1 if the formula is applied during sampling, and n = 100 if the formula is applied after sampling.

### Applying after sampling

![diagram](image-3.png)

![data](image-4.png)

### Applying during sampling


![diagram](image-5.png)


![data](image-6.png)

# Task 3: AM Modulator

The standard equation for modulating is

$$s(t) = [A_c + A_mcos(2\pi f_mt)]cos(2\pi f_ct)$$

the variables with the subscripts m and c are used to represent information for the modulated signal and the carrier signal, respectively.

### Generating a message and carrier signal

First, we will generate two waveforms using the **wave generator** module in the diagram window

the two waves will be generated using the information in the table below

![table](image-2.png)

We would like to see the power spectrum of the message signal. This can be done by inserting the **FFT Power Spectrum and PSD module** into the diagram.

Then, we must connect the message signal to the "signal" input terminal of the module.

The power spectrum is then obtained by creating graphs in the panel, and then connecting the graph nodes to the output of the FFT Power Spectrum and PSD module to the sine wave terminal.

![diagram](image-7.png)

![data](image-8.png)

Then, using the formula that was stated earlier, the AM waveform can be obtained.

$$s(t) = (A_c + A_mcos(2 \pi f_m t))cos(2 \pi f_c t)$$

$$s(t) = c(t) (1 + m(t)/A_c)$$

Therefore, we obtain the AM waveform by dividing the message signal by the carrier amplitude, adding a 1 and multiplying the output of that sum by the carrier signal.

![AM signal diagram](image-9.png)

![AM signal data](image-10.png)

Then, we can create an indicator to show the AM power spectrum and waveform.

![AM power spectrum](image-11.png)

We can now easily calculate the modulation index using

$$\mu = A_m/A_c$$


### Making the module a reusable block

The block diagram that was created can become modular by following a few simple steps

First, the **Edit icon** in the top right corner is pressed, then, the input and output terminals can be configured. They key inputs are frequency and amplitude for both the message and carrier, along with the carrier sampling info. The key outputs are message signal.