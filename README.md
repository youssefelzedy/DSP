
### Library You want
```python
import numpy as np
import matplotlib.pyplot as plt
import scipy.signal as signal
```
### Base Equation
```python
# Change Only this part
B = [1, 1.655, 1.655, 1]  # البسط
A = [1, -1.57, 1.264, -0.4]  # المقام
```

### Poles and Zeros Using `tf2zpk` Function
```python
# Using the tf2zpk function to convert the transfer function to zeros, poles, and gain.
plt.figure(figsize=(4, 4))
z, p, k = signal.tf2zpk(B, A)
plt.plot(np.real(z), np.imag(z), 'bo', fillstyle='none', markersize=10)
plt.plot(np.real(p), np.imag(p), 'rx', markersize=10)
unit_circle = plt.Circle((0, 0), 1, color='black', fill=False)
plt.gca().add_artist(unit_circle)
plt.xlim([-1.5, 1.5])
plt.ylim([-1.5, 1.5])
plt.xlabel('Real')
plt.ylabel('Imaginary')
plt.title('Poles and Zeros')
plt.grid(True)
```

### Poles and Zeros Without Using `tf2zpk` Function
```python
# Without using the tf2zpk function.
zeros = np.roots(B)
poles = np.roots(A)
plt.figure(figsize=(4, 4))
plt.plot(np.real(zeros), np.imag(zeros), 'bo', fillstyle='none', markersize=10)
plt.plot(np.real(poles), np.imag(poles), 'rx', markersize=10)
unit_circle = plt.Circle((0, 0), 1, color='black', fill=False)
plt.gca().add_artist(unit_circle)
plt.xlim([-1.5, 1.5])
plt.ylim([-1.5, 1.5])
plt.xlabel('Real')
plt.ylabel('Imaginary')
plt.title('Poles and Zeros')
plt.grid(True)
```

### Frequency Response - Amplitude
```python
# Frequency response, both amplitude and phase.
plt.figure(figsize=(6, 3))
w, h = signal.freqz(B, A)
plt.plot(w, abs(h))
plt.xlabel('Frequency [rad/sample]')
plt.ylabel('Amplitude')
plt.title('Frequency Response - Amplitude')
plt.grid(True)
```

### Frequency Response - Phase
```python
plt.figure(figsize=(6, 3))
plt.plot(w, np.angle(h))
plt.xlabel('Frequency [rad/sample]')
plt.ylabel('Phase')
plt.title('Frequency Response - Phase')
plt.grid(True)
```

### Impulse Response
```python
# Impulse response
t, h = signal.dimpulse((B, A, 1), n=1000)
h = np.squeeze(h)
plt.figure(figsize=(6, 3))
plt.plot(t, h)
plt.xlabel('Time [samples]')
plt.ylabel('Impulse response system')
plt.title('Impulse response')

plt.show()
```
