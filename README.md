# FSRS4RemNote

FSRS4RemNote is a custom scheduler plugin for RemNote implementing the Free Spaced Repetition Scheduler. FSRS is based on the [DSR](https://supermemo.guru/wiki/Two_components_of_memory) (Difficulty, Stability, Retrievability) model proposed by [Piotr Wozniak](https://supermemo.guru/wiki/Piotr_Wozniak), the author of SuperMemo. FSRS is improved with the DHP (Difficulty, Half-life, Probability of recall) model introduced in the paper: [A Stochastic Shortest Path Algorithm for Optimizing Spaced Repetition Scheduling](https://www.maimemo.com/paper/).

The scheduler is based on a variant of the DSR  model, which is used to predict memory states. The scheduler aims to achieve the requested retention for each card and each review.

# DSR Scheduler changes to standard FSRS4RemNote behavior

The formulas for new stability after recall and new stability after forgetting have been reshaped, in order to ensure w8 and w12 really modulates the retrievability weight on the next stability. 

Increasing w8 (coupled with decreasing w6) can ensure teh same behavior of stability increase for cards reviewed on due dates, but make the stability increase in case of recall less agressive for very overdued cards.

$S^\prime_r(D,S,R) = S\cdot(e^{w_6}\cdot (11-D)\cdot S^{w_7}\cdot(e^{(1-R^{w_8})}-1)+1)$

Also, new stability after rating "Hard" has been corrected to be the last stability * hard interval. This is to avoid the FSRS strange behavior of, after rating "Hard", on next review the proposed next interval in case of pressing "Hard" once more being too long, almost the same of that of pressing "Good".

## Usage

- Install the plugin from the RemNote plugin marketplace.
- Open the settings page and click on [Custom Schedulers].
- You can choose to use DSR Scheduler as your Global Default Scheduler or any other scheduler by clicking on the "Scheduler Type" dropdown menu and selecting "DSR Scheduler".