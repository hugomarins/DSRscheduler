# A FSRS4RemNote fork

DSR Scheduler is a fork of FSRS4RemNote (https://github.com/open-spaced-repetition/fsrs4remnote).

FSRS4RemNote is a custom scheduler plugin for RemNote implementing the Free Spaced Repetition Scheduler, based on the [DSR](https://supermemo.guru/wiki/Two_components_of_memory) (Difficulty, Stability, Retrievability) model proposed by [Piotr Wozniak](https://supermemo.guru/wiki/Piotr_Wozniak), the author of SuperMemo, and improved with the DHP (Difficulty, Half-life, Probability of recall) model introduced in the paper: [A Stochastic Shortest Path Algorithm for Optimizing Spaced Repetition Scheduling](https://www.maimemo.com/paper/).

The scheduler is based on a variant of the DSR  model, which is used to predict memory states. The scheduler aims to achieve the requested retention for each card and each review.

# DSR Scheduler changes to standard FSRS4RemNote behavior

The formulas for new stability after recall and new stability after forgetting have been reshaped, in order to ensure w8 and w12 really modulates the retrievability weight on the next stability. 

Increasing w8 (coupled with decreasing w6) can ensure teh same behavior of stability increase for cards reviewed on due dates, but make the stability increase in case of recall less agressive for very overdued cards.

$S^\prime_r(D,S,R) = S\cdot(e^{w_6}\cdot (11-D)\cdot S^{w_7}\cdot(e^{(1-R^{w_8})}-1)+1)$

In the same manner, the formula for the next forget stability has been adjusted:

$S^\prime_f(D,S,R) = w_9\cdot D^{w_{10}}\cdot S^{w_{11}}\cdot e^{(1-R^{w_{12}})}$

Also, new stability after rating "Hard" has been corrected to be the last stability * hard interval. This is to avoid the FSRS strange behavior of, after rating "Hard", on next review the proposed next interval in case of pressing "Hard" once more being too long, almost the same of that of pressing "Good".

Other minor changes:
- For new cards, learning steps were ajusted:
    - 1 min after rating "Again";
    - 10 min after rating "Hard";
    - 1 day after rating "Good";
    - 10 days after rating "Easy".

## Usage

- Install the plugin from the RemNote plugin marketplace by using the link https://www.remnote.com/plugins/dsrscheduler.
- Open the settings page and click on [Custom Schedulers].
- Choose to use "DSR Scheduler" on the "Scheduler Type" dropdown menu (as your Global Default Scheduler or any other scheduler).