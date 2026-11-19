# Relax Inc. | Which new users become adopted users?

**Finding.** Of 12,000 signups, 1,602 (13.35%) logged in on three distinct dates within a rolling seven-day period. Signup source separates groups, but its ability to rank individual future adopters is weak.

| Signup source | Users | Adopted during observation |
|---|---:|---:|
| Google authentication | 1,385 | 16.75% |
| Guest invitation | 2,163 | 16.64% |
| Website signup | 2,087 | 14.04% |
| Organization invitation | 4,254 | 13.00% |
| Personal workspace invitation | 2,111 | 7.77% |

**How adoption was counted.** We retained one visited record per user and calendar date, then compared each date with the date two visits earlier. A gap of six days or less qualifies, including windows that cross a Sunday or a month boundary. We joined the earliest qualifying date back to all signups so users who never logged in remained in the denominator.

**Forward prediction.** We tested signup-source logistic regression on 2,177 users registered from February 1, 2014 onward with at least 30 observable calendar dates. Training used 8,510 earlier signups and only labels available before February 1. The observed-adoption target gives later users less follow-up, so we also tested adoption within the first 30 calendar dates for everyone.

| Target on later signups | Test prevalence | Source-only ROC AUC | Source-only average precision | Average precision with marketing flags |
|---|---:|---:|---:|---:|
| Ever adopted by end of observation | 9.00% | 0.547 | 0.098 | 0.099 |
| Adopted in first 30 calendar dates | 3.31% | 0.562 | 0.039 | 0.037 |

Prevalence is the constant-score baseline for average precision. Marketing opt-in and drip enrollment added little, even assuming those snapshot fields were available at signup. Last-session time would reveal later activity, so we excluded it. Personal workspace invitees also had the lowest 30-day rate on the holdout (1.47%). Google signups’ stronger full-period rate did not carry through to that early outcome (2.72%).

**Recommendation.** Test an onboarding prompt that gives personal-workspace invitees a specific shared task to return to. Randomize by workspace to limit spillover and compare 30-day adoption. Capture first collaboration and workspace activity at invitation time to investigate whether the gap reflects onboarding friction or how active the inviting team already was.

## Reproduce

Place takehome_users.csv and takehome_user_engagement.csv in a local data/ folder. From this directory run:

    python -m pip install -r requirements.txt
    python -m jupyter lab Relax_User_Adoption.ipynb

The notebook displays the source-level summaries and held-out scores. Raw names, email addresses and event records are excluded from the repository.

Source: Springboard take-home challenge. Analysis used the [public copy of the supplied inputs](https://github.com/pjandir/Springboard-DSTrack/tree/32c476cef31c84840a770e4396e2b76acfb9a71d/Exercises/take_home_challenges_20.1/relax_challenge).
