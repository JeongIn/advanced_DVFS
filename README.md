# advanced_DVFS

Linux shell script for advanced DVFS technique.

Set a maximum temperature, # of cores, maximum frequency of your devices. </br>
It predicts the higest temperature of cores at different frequencies. </br>
The highest one is adopted for CPU frequency.

We use linear-regression model. </br>
The model was established using the following:

<pre><code>EXEC, IPC, FREQ, AFREQ, L3MPI, READ, WRITE,
INST, PhysIPC, INSTnom, Proc_Energy_(Joules), Total_Util, frequency

"Total_Util" is total utilization of cores.
"frequency" is current CPU frequency.
Other details are in PCM (Processor Counter Monitor) - https://github.com/opcm/pcm. </code></pre>
This model is based on Intel i7-7700. </br>
Thus, different types of servers may show slightly different prediction results.

<hr/>
This script must be run with sudo privileges.

## Installation
1. Install PCM (Processor Counter Monitor)
<pre><code>git clone https://github.com/opcm/pcm.git </code></pre>

2. Download this project
<pre><code>git clone https://github.com/JeongIn/advanced_DVFS.git </code></pre>

3. Move "pcm-pred_model.cpp" and "advanced_DVFS" to "pcm" folder

4. Modify "Makefile"
<pre><code> EXE = pcm-pred_model.x </code></pre>

5. Make
<pre><code> make </code></pre>


## How to Use
1. super user mode
<pre><code> su </code></pre>

2. Start "pcm-pred_model"
<pre><code>cd pcm/
./pcm-pred_model.x </code></pre>

3. Start "advanced_DVFS" with new terminal. </br>
[This example will limit system temperature to 50 Celsius (8 cores, Maximum frequency: 4.2GHz]
<pre><code>cd pcm/
./advanced_DVFS.sh 50 8 4200000 </code></pre> 

