Hvis vi åbner den givene wav fil og kigger på det som spektrometer så ser vi at der er ny frekves hvert sekundt.

![image](https://github.com/L30HP/DDC-24-Nationals/assets/93826052/b04e58ca-2af2-4440-b28a-ce7e7b395b6c)




Først fik jeg lavet et script der kunne læse wav filens frekvens hvert sekund:

start prompt: 

#### I need a python script that reads a wav file, and analyzes the frequency components for each 1s section, and prints the dominant frequency for each second.

```python
import numpy as np
import scipy.io.wavfile as wav

def dominant_frequency(filename):
    # Read the WAV file
    sample_rate, data = wav.read(filename)

    # Handle stereo audio by averaging both channels
    if len(data.shape) == 2:
        data = np.mean(data, axis=1)
    
    # Define the duration for each segment
    segment_length = sample_rate  # 1 second segments
    
    num_segments = len(data) // segment_length

    # Process each 1-second segment
    for i in range(num_segments):
        segment = data[i * segment_length : (i + 1) * segment_length]
        
        # Apply FFT to the segment
        fft_result = np.fft.fft(segment)
        freqs = np.fft.fftfreq(len(segment), 1 / sample_rate)
        
        # Consider only positive frequencies
        positive_freqs = freqs[freqs >= 0]
        positive_magnitudes = np.abs(fft_result[freqs >= 0])
        
        # Identify the dominant frequency
        dominant_freq = positive_freqs[np.argmax(positive_magnitudes)]
        
        print(f"{dominant_freq:.0f}")


# Example usage
filename = 'output.wav'
dominant_frequency(filename)
```


Så fik jeg en masse tal som jeg sat ind i cyberchef og decoded talne fra decimal.
      
Derefter fik jeg en binær fil med starten PNG.
      
Så åbnede jeg den som png og fik et billede som var lidt pixels med forskellige farver

![image](https://github.com/L30HP/DDC-24-Nationals/assets/93826052/97e6130e-37e7-4aee-acf6-d120389fa86c)

Så fik jeg et script som kunne læse hver pixels far i r, g, b.

Start prompt:

#### I need a python script that reads a png file, and prints the color of each pixel

```python
from PIL import Image

# Load the image
img = Image.open("download.png")

# Convert image to RGB format
img = img.convert('RGB')

# Get image dimensions
width, height = img.size

# Prepare a bytearray to store RGB values
output_data = bytearray()

# Loop through each pixel and store its color in the bytearray
for y in range(height):
    for x in range(width):
        r, g, b = img.getpixel((x, y))
        output_data.extend([r, g, b])

# Write the RGB values to a binary file
with open('output.bin', 'wb') as f:
    f.write(output_data)

```
Så fik jeg en binær pdf fil ud og så åbnede jeg den som pdf og så var flaget det :)

![image](https://github.com/L30HP/DDC-24-Nationals/assets/93826052/2fbac51f-c476-46eb-9f50-547121145d89)
