# Notes on starting any project
Notes, tips, and best practices on starting any research project. (More focused on image tasks since I work on image tasks)

# End task/goal
For any project there's an end task, goal, or performance one is aiming for, so make sure the following checklist is applied:
- [ ] Do a literature review on what the state-of-the-art performance is for that specific task or something close to it.
- [ ] Either train or clone the state-of-the-art model and replicate its performance on your goal/end task.

# Dataset
For any project, always do dataset exploration.
- [ ] Check class balances - what is the class balance/imbalance if any
- [ ] Check dataset images - is the data 8bit/16bit, grayscale/RGB, image shapes (128x128, 256x256, etc.)
- [ ] Check image files - how is the data stored? Png/jpeg/npy/nifti/DICOM
- [ ] Check image processing - specifically for DICOM images, do you need to do some CT HU windowing? MR adjustments (windowing)?

# Models
For any project, you have a model in mind
- [ ] 

# Model updates/improvements
- [ ] For every step of the training or model changes, double check the model performance to make sure the end task is still performing as good, if not better than the state-of-the-art.
