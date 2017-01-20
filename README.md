# active_adaptation
## Rough Plan
- Implement adverserial Lavg -> Lmax
- Robust optimization experiment
- Active learning experiment
- ICML? Feb 24!!!!
- Figure out the theory part of domain adaptation stuff
- Domain adaptation experiment
- Active domain adaptation experiment
- ICCV? March 17
- RL experiment with robots
- Counter-Factual learning
- NIPS? May 20?

# Jan 20,21,22

## Jan 20
- Cifar10 training and test (full data/nothing new using tf_base)
- Set the seed training_set and save it num_images = 5000
- Random active learning test 0.1/0.2/0.3/0.4/0.5/0.6/0.7/0.8/0.9/1.0
- Plot the accuracy vs training data (baseline 1)

## Jan 21
- L_avg -> L_max experiment with the same setup 
- No random selection, just a sampling w/ replacement
- Plot the accuracy vs training data (baseline 2)

## Jan 22
- Sample new data with the learned model
- Plot the accuracy vs training data (proposed model)
