# active_adaptation
## Rough Plan
- Implement adverserial Lavg -> Lmax
- Robust optimization experiment
- Active learning experiment
- ICML Feb 24!!!!
- Figure out the theory part of domain adaptation stuff
- Domain adaptation as a discriminator
- Domain adaptation experiment
- Active domain adaptation experiment
- ICCV March 17
- RL experiment with robots
- Counter-Factual learning
- NIPS May 19

## Step Baseline 1
- <del>Cifar10 training and test (full data/nothing new using tf_base)</del>
- <del>Set the seed training_set and save it num_images = 5000</del>
- <del>Random active learning test 0.1/0.2/0.3/0.4/0.5/0.6/0.7/0.8/0.9/1.0</del>
- <del>Plot the accuracy vs training data (baseline 1)</del> see acc_vs_size.png

## Step Baseline 2
- <del>L_avg -> L_max experiment with the same setup </del>
- <del>No random selection, just a sampling w/ replacement </del>
- <del>Refactor the code</del>
- <del>Re-run the baseline 1</del>
- <del> Run the baseline 2 </del>
- <del> Plot the accuracy vs training data (baseline 2) </del>
- <del> Consider unbiasing the gradients </del> samples are pretty uniform
- <del> Consider dropping one fc layer </del> the reason is about distribution difference

## Step Active Learning
- Consider a few tricks
    - <del> Re-initialize everything </del> effective but not much
    - <dek> Keep a validation and learn adverserial only on the validation (no contamination since actual network never sees it) </del> effective but not much
- Sample new data with the learned model
- May be a diversity trick? <del>(still a valid thing)</del> does not seem necessary since tSNE is pretty diverse
    - Diversity is a submodular function if defined as sum of total probability covered around each ball
- To match theory and practice, put feature learning in both players
- Include gradient reversal layer
    - Seems like best option for now
    - <del>Step 1: vanilla reversal</del> Note: ADAM is using second derivative which is crap in adverserial setting so use momentum
    - Step 2: vanilla reversal+loss_rescale
    - Test 1: Reversal domain estimate + sampling
    - Test 2: Reversal + combinatorial sampling (this is desired simply because theory)
    - Step 3: active learning
- <del> Try with oracle loss </del> still worse than random may be it is bringing sort of a bias
- <del> Look at the tSNE plot and see is it because of diversity</del> it is pretty diverse
- Plot the accuracy vs training data (proposed model)

## Step Domain Adaptation
- Modify the loss/adversery to be applicable to domain adaptation

## Step Active Learning with DA
- Combine everything

## Device Assignment
- 109 0/5k/10k/15k
- 110 20k/25k/30k/35k
- 106 40k/45k

## Results
50,55,62,68,70,73,76,78,79,81

## Way to sample active datapoints
- get the top 5000 expected loss make it 1 rest 0
- combine with gamma = 0.01 or 0.02


