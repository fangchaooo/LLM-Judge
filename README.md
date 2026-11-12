# A Retrospective on Five Studies of LLM-Based Driving Evaluation
A Retrospective on Five Studies of LLM-Based Driving Evaluation Six Cases Where the Headline Number Was Decided by Something Other Than the Model
  
This is a retrospective on a year of experiments, not a new method.

Five studies asked variations of one question: can a language or vision-language model replace a hand-written Python rule evaluator in deciding whether
a logged driving trajectory violates a rule? The report looks back at those studies, but not at how well the models did. It looks at something more
awkward: six times, the headline number turned out to be decided by a variable unrelated to the capability being measured — and every time, it was found
after the number had been written down.

Each case has a mechanism that was measured rather than guessed:

| # | Finding | The numbers |
|---|---|---|
| 1 | A constant predictor beat most of the arms | Majority class 0.7031; 4 of 5 rescored arms fell below it |
| 1b | The prompt already contained the decision program, so transcribing it scores perfectly | 24/24 and 12/12 with 0 model calls |
| 2 | Holding the arm fixed and changing only the training seed moved it more than the arms differed | Largest within-arm movement 0.1574, against a largest power-calibration anchor of 0.0652 |
| 3 | A zero-shot evaluation that is byte-identical across reruns still changes its answer when a clause is reworded | Seven paraphrases span 0.0271, wider than the entire reported margin of 0.0250 |
| 4 | A gate criterion measured the data pipeline, not the model | All 3 arms, including a constant-velocity control, report 0.8947 |
| 5 | The same question, asked twice, reversed sign because the reference arm had got stronger | Miss rates went from 0.1761 vs 0.5341 to 0.0125 vs 0.0109 |

The sixth case runs the other way, and is the most useful one. An endpoint sitting at 0.5250 against constant strategies at 0.5000 looks like absent
capability. But reading out the probability the model placed on the token it had already emitted — leaving the generated answers byte-identical — gives
an AURC of 0.3392 against 0.4750 for random ordering. Turned into a threshold rule and reported on scenarios that do not overlap the fitting set, it
moves 0.5150 to 0.6650, attaining 90.4% of the refit ceiling. What was empty was the output stage, not the model. The two diagnoses imply opposite
actions: a larger model and a new objective, or a calibration layer that costs almost nothing.

The report closes with a seven-item checklist drawn from the mechanisms, and five directions it would take next: from executing known rules to
understanding unknown ones, from a binary verdict to a confidence-aware judge, from accuracy to safety-aware endpoints, from running reinforcement
learning to first measuring whether the reward has variance to optimise, and from studying the model to studying the whole evaluation system.
  
  One detail about the report itself. No number in it is typed by hand. All 125 values are recomputed from the stored experiment artifacts by one
  generator script, which writes the inline macros and the tables from the same values, so a sentence cannot disagree with the table beside it. The
  generator also asserts the identities and inequalities the six cases rest on, and refuses to run if any of them stops being true — because then the
  prose would be wrong.
  
  That checking caught the author twice during writing. It also caught two values that the original run log carries but that exist in no stored artifact,
  only in the log's prose. Those two are not used; the substitution is recorded in the disclosure section. The report's own subject recurring inside the
  report is, in a small way, the point.
  
  What it does not claim. All six cases are statements about measurement, not about whether models can understand driving scenes. That sentence is in the
  paper's scope paragraph, and it is load-bearing: the labels in every study come from a program, so a program scores perfectly by construction and the
  model's ceiling is a tie. The questions with room in them are the ones the program cannot answer, and reaching them needs annotation rather than
  compute.

