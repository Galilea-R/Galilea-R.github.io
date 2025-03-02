---
title: "Brain Theory"
categories:
  - Blog
tags:
  - brain
  - data science 
---

One of my main achievements in my academic journey has been using Neurodynex to comprehend how changes in the following variables impact the behavior of the simulated neuron:
membrane_time_scale, membrane_resistance, firing_threshold, abs_refractory_period, and v_rest

This project was part of my coursework in Brain Theory and has been my favorite. For a long time, I aspired to study neuroscience, so I enjoy combining data science with topics related to the brain.

```python
{% raw %}
i_min=3.0*namp

# create a step current with amplitude= i_min
step_current = input_factory.get_step_current(t_start=5, t_end=100, unit_time=ms,amplitude= i_min)  # set i_min to your value

LIF.FIRING_THRESHOLD = -40*mV

# run the LIF model.
# Note: As we do not specify any model parameters, the simulation runs with the default values
(state_monitor,spike_monitor) = LIF.simulate_LIF_neuron(input_current=step_current, simulation_time = 100 * ms,
                                                       membrane_time_scale=8.*ms,
                                                       membrane_resistance=25.*Mohm,
                                                       firing_threshold=-40.*mV,
                                                       abs_refractory_period=2.*ms,
                                                       v_rest=-70*mV,
                                                       v_reset=-65*mV)
# plot I and vm
plot_tools.plot_voltage_and_current_traces(state_monitor, step_current, title="min input", firing_threshold=LIF.FIRING_THRESHOLD)
print("nr of spikes: {}".format(spike_monitor.count[0]))  # should be 0
{% endraw %}
```
One of the conclusions we were able to observe when playing with the parameters is that, by adjusting the membrane resistance, the number of spikes increases significantly. This suggests that, experimentally, membrane resistance is what affects the number of spikes in this model, confirming what we had already seen in class.
