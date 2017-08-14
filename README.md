# gridagent
GridAgent is a Particle Electron shield that both provides ground truth power state information to the GridWatch central service over GSM and explores audio fingerprinting as a signal for grid state. 

GridAgent will get its power from AC. It will have a LIPO backup. Electrons come with built in circuitry to detect whether the AC or the LIPO source is being used. This allows for an outage to be detected when the Electron switches from AC to LIPO, and a restoration to be detected with the Electron switches from LIPO to AC. On either event, GridAgent will sample from all sensors. It will look at the microphone FFT for 50hz/100hz peaks and will look for fingerprint changes in the magnetic field. The Electron has a M3 base processor, which seems capable of doing much of the DSP work for this. 

Particle Electron provides some pretty magical things, including OTA updates and management of fleets of GSM enabled systems. Originally, GridAgent was going to be built as a self contained system. Instead, in an effort to get a number of GridAgent devices deployed in Kenya and Ghana as soon as possible, we are going to bootstrap on top of Electron. 

The major downside of Electron is a fairly expensive GSM plan ($2.99/mb, $0.99 a mb after that) and a fairly expensive base platform ($49 for 2G). This will require some thinking about what data makes sense to collect in real time. It makes raw audio impossibly expensive. Electron also doesn't have built in GPS, which many 2G low cost radios have in chip. Still, we can throw money at this for a small number of units and start learning about deployment hurdles and evaluating sensors in the field. The hardest part of my Kenya deployments so far has been GSM management and reliable OTA upgrades, so, Electron seems worth paying for at least for now.

The first hardware that is going to be part of GridAgent is going to be an Electron shield built to evaluate multiple microphones and hall effect sensors. Design files are found in /hardware/evaluation_board. 

The microphones under evaluation are all MEMS PDM style with a frequency range that starts below 50HZ. This may require the use of a CODEC, but I'm hopeful that it won't to keep cost and complexity down. I plan on getting around this on the final versions of GridAgent by using the i2c sampling method for clocking the microphones. This won't work for the evaluation board because there are too many microphones. I am still trying to figure out how I should deal with this. I don't want to have to figure out a CODEC just for evaluation purposes, but don't have a great way of muxing mics otherwise. Just picking a single pair of mics per event makes it difficult to directly compare mics. Thinking remains to be done on this.

Right now, the code for GridAgent is being developed in the Particle Electron online IDE and is written in the Arduino style. The software and compiled binarys will be found in /software/evaluation_board. 

GridAgent is part of the GridWatch project.
