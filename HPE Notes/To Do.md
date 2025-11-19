
**To Do:**
- Make story for updating the kubectl dsp plugin.
- Review comments and test scenarios on ippodd osd add and remove ip address requests change
- make story to refactor lir-svc configmap code to use k8scommon configmap functions

Switch Firmware Versions
GL.10.12.1000 = ArubaOS-CX_8325_10_12_1000.swi
GL.10.15.1010 = ArubaOS-CX_8325_10_15_1010.swi
GL.10.16.1006 = ArubaOS-CX_8325_10_16_1006.swi
CL.10.16.1006 = AOS-CX_9300-32D_10_16_1006.swi

Add model to the CRD?

JL636A part = 8325 model = ArubaOS-CX or AOS-CX file prefix, GL version prefix
R8Z96A part = 9300 model = AOS-CX file prefix, CL version prefix 

Check part number mapping in configmap to get 

GL version prefix = JL636A part = 8325 model
CL version prefix = R8Z96A part = 9300 model

inputs:
firmware version spec -> prefix can be extracted out of and used to check model
switch part number -> part number maps to model



i have a switch firmware version which is being used to determine which firmware image to use to upgrade to




