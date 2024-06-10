# Peer Review Grading

We use [Bayesian inference](https://arxiv.org/abs/2209.01242) to estimate each student's "dependability" as a reviewer on a weekly basis.
The key idea is that calibrations and assignments graded by TAs give us information about which graders are more reliable; we then bootstrap this knowledge to decide how much to trust each grader on assignments that were not graded by a TA.
Your dependability score is our estimate of _effort_ \* (1/_variance_), where _effort_ is (1 - the probability that you choose a grade close to the class average without considering the essay) and _variance_ is our estimate of your tendency to differ from the essay's true grade when you do make an effort. The system starts out with the assumption that all students have low dependability scores (specifically, low _effort_ and high _variance_).
As you grade assignments and perform calibrations, we'll update these beliefs.
In particular, observe that doing more calibrations both helps you to get better at grading and gives us evidence of your grading prowess to overwhelm the system's pessimistic initial belief.
Note that if you always assign each submission the class average, or if you grade very erratically, our model will assign you a low _effort_ probability; you need to properly identify both strong and weak assignments in order to achieve a high dependability score.

Every time a TA grades an assignment that you also graded, they'll make a binary assessment of whether you offered thoughtful comments (independently of whether they agreed with your scores).
We'll use these assessments to update your _effort_ probability and hence your dependability score.

For each student we will maintain both a "realistic" estimate of dependability and a "pessimistic" (lower confidence bound) estimate.
Each essay, we'll identify those students with pessimistic dependability estimates below a certain threshold and assign them to grade each other; we'll also have a TA grade each such assignment.
(Note that this means that if you have a low pessimistic dependability estimate, you'll likely get noisier peer grades, but this won't matter because your grade will be entirely determined by a TA.)
The remainder of students (those for whom even our pessimistic dependability estimates exceed a threshold) will perform independent peer review grading as discussed above.
This system ensures that your assignment will either be graded by a TA or will be graded entirely by peers that the system confidently predicts will grade reliably.

If your pessimistic dependability estimate falls below our threshold, you will also be required to perform 3 "calibration" reviews of carefully pre-graded essays from previous years, which will automatically be graded by the system.
These calibration reviews are a designed to help you learn how to grade well and also how to write good essays.
You're also allowed to do extra calibrations (whether your weekly assignment was 3 or 0); this is a particularly good idea when your dependability estimate is low, because doing extra calibrations will teach you to grade better and can also improve your peer review grading scores.

Each essay, we'll assign you a peer review grading score; overall, these scores will make up the peer review grading portion of your final grade.
These grades will be derived from our "realistic" estimates of your dependability score.
The exact formula is complex and subject to change, but a student with a dependability score exactly equal to our calibration threshold will receive a grade of 80%.
Beyond this, the formula is strictly monotone in dependability; you can see your current standing in MTA.

Observe that your dependability score will start low, but you can increase it quickly by performing additional calibrations and by grading well.
You'll only be eligible to perform peer review when you have completed the week's quiz.
If you complete only `_x_` peer reviews in a week when you were assigned `_y_`, we'll scale your peer review grade for that week by `_x/y_`; if you complete only `_x'_` calibrations in a week when you were assigned `_y'_` calibrations, we'll (further) scale your peer review grade for that week by `_(y + x')/(y + y')._`

We'll scale your peer review grades in a manner similar to your essay grades:

- your first 3 peer review grades will be scaled by 0.6;
- your next 3 peer review grades will be scaled by 0.8;
- your final 4 peer review grades will be scaled by 1.0.

Your final peer review grade will be a weighted average of your individual peer review grades using the weights given above.

```{tip}
We will drop the 2 peer review weeks that produce the largest weighted average overall (not necessarily your two lowest grades, since later weeks are worth more).
```
<!-- 
## Frequently Asked Questions (about Peer Reviews)
 -->


