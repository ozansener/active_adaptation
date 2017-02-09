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
    - <del>Diversity is a submodular function if defined as sum of total probability covered around each ball</del>
    - <del>Theory suggests a covering ball so let's use that</del>
- <del>Combinatorial Algorithm: start with greedy 2-OPT solution, then refine it using integer programming and binary search if feasible.</del> this is pretty feasible actually somehow Gurobi is more efficient than greedy one to improve the solution
- <del>To match theory and practice, put feature learning in both players</del>
- Include gradient reversal layer
    - Seems like best option for now
    - <del>Step 1: vanilla reversal</del> Note: ADAM is using second derivative which is crap in adverserial setting so use momentum 
    - <del>Step 1.5: Implement reversal with single output (so it can learn data distribution) </del>
    - <del>Step 2: vanilla(so) reversal+loss_rescale </del>
    - <del>Step 3: Reversal(so) domain estimate + sampling </del>
    - <del>Step 4: Reversal(so and not/so) + combinatorial sampling (this is desired simply because theory) </del>
- <del> Try with oracle loss </del> still worse than random may be it is bringing sort of a bias
- <del> Look at the tSNE plot and see is it because of diversity</del> it is pretty diverse
- <del> Exploration works so test different degree of exploration </del> 0.2 seems like a nice one, may be 0.25
- Consider normalizing stuff since they become crazy (may be remove batch norm)
- Use BiGAN or ALI as semi-supervised algorithm

## Baselines
- k-k^\prime
- maximum uncertanity
- uncertanity based sampling
- oracle uncertanity based sampling

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
- <del>get the top 5000 expected loss make it 1 rest 0</del>
- <del>combine with gamma = 0.01 or 0.02</del>

## Report
- Descrive the active learning with pool problem, state it is a weakly supervised problem and need to be treated like one
- Discuss p(x) p_n(x) p_\hat{n}(x) and give the basic idea behind loss re-scale and discuss how it can be discussed through alternating minimization (Adverserial Weak Supervision)
- Discuss the theoretical aspect of active learning
    - Review robustness and generalization
    - Lemma (VGG is robust)
    - Theorem: Any robust algorithm is robust with less samples if ()
- Discuss the empirical setup and explain the two concepts (fixed budget, single step)
    - Representations should be as close as possible so it is easier to cover the same space with less points
        - Gradient reversal layer
    - The bound depends solely on (\gamma) hence solve combinatorial optimization to have minimum ball
        - Binary search over a submodular problem
- Experiments
    - MNIST
    - Cifar 10 / Cifar 100 on VGG


# Current TODO

- <del>Get the features and look at the tSNE </del>
- Sample far points and try this
- Implement the combinatorial algorithm for N-D, try with 2D t-SNE points
- Experiment the active learning
