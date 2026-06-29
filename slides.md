---
title-slide: false
bibliography: references.bib
csl: vancouver.csl
citeproc: true
theme: serif
background-color: "#ffffff"
transition: slide
navigationMode: linear
hash: true
---

:::: {.columns}
::: {.column width="50%"}

## Sample slides
#### PlaceHolderName
#### Universiti Malaysia Perlis
#### [placeholder@email.com](mailto:placeholder@email.com)

<!-- __AUDIO_INTRO_DO_NOT_TOUCH__ -->

:::

::: {.column width="50%"}
![](media/pics/logo1.png)
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Slide one
**Key Concepts:**
- Energy conservation per @carnot1824.
- $\Delta U = Q - W$
:::

::: {.column width="50%"}
![](media/pics/sample.png)
:::
::::

---

<span class="slide-title" data-title="My Hidden Slide Name"></span>

![](media/pics/wide.jpeg)

---

:::: {.columns}
::: {.column width="50%"}
### The Master Equation
The fundamental relation of thermodynamics:

$$\Delta U = Q - W$$

The work done $W$ is positive when the system expands against an external pressure.
:::

::: {.column width="50%"}
<video data-src="media/videos/sample.mp4" data-autoplay loop muted width="100%"></video>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Visualizing the Gas Law
**Interactive Model:**

- P, V, and T relationships.
- Use the slider to adjust pressure.
- Observe the phase boundary.
:::

::: {.column width="50%"}
<iframe 
  data-src="media/plots/sample.html" 
  width="100%" 
  height="500px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Control Chart for PartLength

This X-bar control chart displays the `PartLength` for data filtered by `Machine = 1`, `Pressure = 200kPa`, and `Temperature = 338K`.

**Key Observations:**
- **Target Value:** 50
- **Upper Specification Limit (USL):** 55
- **Lower Specification Limit (LSL):** 45

Analyze the plot to identify any out-of-control points or trends that might indicate process instability.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/machine1_control_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Control Chart for PartLength

This X-bar control chart displays the `PartLength` for data filtered by `Machine = 1`, `Pressure = 100kPa`, and `Temperature = 303K`.

**Key Observations:**
- **Target Value:** 50
- **Upper Specification Limit (USL):** 55
- **Lower Specification Limit (LSL):** 45

Analyze the plot to identify any out-of-control points or trends that might indicate process instability.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/machine1_P100_T303_control_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Process Capability Chart for PartLength

This chart visualizes the process capability for `PartLength` under the conditions of `Machine = 1`, `Pressure = 100kPa`, and `Temperature = 303K`. It shows the distribution of the observed data, a fitted normal distribution, and the specified Lower Specification Limit (LSL), Upper Specification Limit (USL), and Target value.

The calculated Cpk value indicates whether the process is capable of producing output within the specified limits. A Cpk >= 1.0 suggests the process is capable.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/machine1_P100_T303_capability_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::

::::
