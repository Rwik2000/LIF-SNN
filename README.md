# Leaky Integrate and Fire - SNN


This is a simple implementation of Leaky integrate and fire model (LIF) neuron. Given an input current value the neuron gives the corresponding spikes. 

All parameters of the neuron can be changed in the [configs.py](www.google.com). Note that the units of time is **milliseconds**.

## Usage:
From [neuron.py](www.google.com), call the function `runLIF()`. 
```python
def runLIF(model, t_span, dt, I):
    v = np.zeros_like(t_span)

    for i, t in enumerate(t_span):
        if i==0:
            v_prev = 0
        else:
            v_prev= v[i-1]
        v[i] = model.generateSpiking(I[i], t, dt, v_prev)

    
    if model.isPlot:
        plt.plot(t_span,v)
        plt.plot(t_span,I)
        plt.show()
    
    return v
```
Here, `t_span` is the the overall time duration, `dt` being the small time steps and `I` being the current function w.r.t time.

To get an idea just run the [neuron.py](www.google.com), and see the default example given at the end:
```python
t_tot = 500
dt = 0.01
t_span = np.arange(0, t_tot+dt, dt)
I = [0 if 200/dt <= i <= 300/dt  else 10 for i in range(len(t_span))] # defining the current(time)
neuron = LIF() #defining the neuron model
# passing the current through the neuron.
v = runLIF(neuron, t_span, dt, I)
```

**NOTE**: To plot the voltage and current data, turn ON the `isPLot` argument in the [configs.py](www.google.com)

## Test Case:
![alt text](http://url/to/img.png)

## To-Do:
Add random salt-pepper noise to the output voltage.


