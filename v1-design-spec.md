# AI Code Debugging Game: V1 Design Spec

Working title: TBD
Status: V1 scope, pending playtest with a small group of engineers
Platform: iOS and Android via React Native (Expo recommended)

---

## 1. Overview

A daily, Wordle-style challenge where software engineers find the bugs in short code snippets that look correct at first glance. Every player who picks the same language gets the same ten snippets on the same day. Players tap the lines they think are wrong, are scored on accuracy with a time bonus, and compete on per-language leaderboards.

The product is built for engineers who are increasingly shipping AI-generated code they don't fully read, and want to get better at reviewing it. It is also designed for short sessions on a commute.

## 2. Goals and non-goals

**Goals for V1**

- Test whether engineers return to a daily debugging challenge on their own.
- Test whether the bugs feel realistic, especially ones an AI coding tool would plausibly produce.
- Validate the core loop, scoring, and mistake limit with a small group of engineers.

**Non-goals for V1**

- Practice / puzzle section (deferred until the daily challenge is validated)
- Hints and any ad-based monetization (deferred)
- Naming or explaining bugs in-game (deferred to practice)
- Languages beyond Go and Python
- Social features beyond leaderboards (no friends, no chat, no sharing beyond a simple result card)
- Interview-prep mode

## 3. Target users

Software engineers who use AI coding tools and play on a phone during a commute (train, bus, subway). Typical session: 5 to 15 minutes.

## 4. Core loop

1. Player opens the app and picks a language (Go or Python). This choice is remembered but can be changed.
2. The app loads today's ten-snippet set for that language.
3. Player reads the code (top) and the expected vs. actual program output (bottom).
4. Player taps line numbers they believe contain a planted error.
5. Each snippet is completed before the next one unlocks. Snippets cannot be skipped.
6. Run ends when all ten snippets are completed, or when the mistake limit is exceeded.
7. Results screen shows score breakdown, streak status, and leaderboard position.

## 5. Daily challenge rules

**Set composition**

- Ten snippets per language per day.
- Each snippet has up to two planted errors (a snippet may have zero or one).
- The same set is served to every player who picks the same language on the same date.

**Mistakes**

- A mistake is tapping a line that does not contain a planted error.
- Re-tapping the same wrong line does not count again.
- Mistake limit for a run = 50% of the total planted errors in that day's set, rounded up to an even number before halving. For the standard set (ten snippets, two errors each, 20 errors), the limit is 10.
- Exceeding the limit (the eleventh mistake, in the standard set) fails the run.

**Failure flow**

- When a run fails, the player sees the results screen.
- The player may continue working through the remaining snippets for learning. Continued snippets show planted errors and do not count toward score, leaderboard, or streak.

**Pause**

- One pause per run. Pausing blurs the screen until the player resumes.
- The run clock stops during pause.

**Timing**

- There is no time limit. Time only contributes a bonus to the score.

## 6. Scoring

Score is computed on the server.

- **Correct find:** fixed points per planted error located.
- **Mistake penalty:** fixed deduction per mistake.
- **Time bonus:** small bonus per snippet for finishing quickly, shrinking gradually over time, capped so it cannot outweigh accuracy. Exact values to be set during playtesting.
- **Failed run:** no score. Does not appear on the leaderboard.
- **Ranking:** total score, then fewer mistakes, then total time.

The results screen shows a breakdown: correct finds, mistakes, time bonus, and total.

During the run, a running score is displayed and updates as correct finds are made.

## 7. Streaks

- A streak advances by one day when a player completes a full daily challenge (all ten snippets, without exceeding the mistake limit) in a given language.
- Streaks are tracked per language. Switching language starts a fresh streak for that language.
- A failed or abandoned run breaks the streak.
- A global "days played" count (across languages, never resets) may be shown on the profile for V1. Optional.

## 8. Leaderboards

- One leaderboard per language per day, plus an all-time view if useful.
- Only completed runs appear. Failed runs do not rank.
- Ties are broken by fewer mistakes, then total time.
- V1 leaderboards are shown as a list of players with their score, streak, and rank.

## 9. Languages and content

- V1 languages: Go and Python.
- Content is written and reviewed by hand before publication. Each snippet has:
  - Code as shipped to the player
  - Expected program output
  - Actual program output (what the code really produces)
  - Planted error line numbers (server-side only, never sent to the client)
  - Short explanation (stored for future practice use, not shown in V1)
- Each language has its own set, so the same bug does not need to appear in both languages.
- Snippets should be realistic: bugs an AI coding tool could plausibly produce, such as plausible-looking code that calls a non-existent or deprecated API, swallowed errors, off-by-one loops, wrong comparison operators, shared mutable state, and tests that pass for the wrong reason.
- Output must be deterministic. Avoid floats in output, unordered map printing, sort ties, and locale-dependent formatting.

## 10. Screens

1. **Onboarding:** short intro, language picker, and a note that the daily set is the same for everyone.
2. **Home:** today's challenge for the selected language, current streak, best score, and a Start button. Language can be changed here.
3. **Challenge:** code panel at top, output panel at bottom, a run header with running score, mistakes remaining, snippet progress (for example, 3 of 10), and pause button. Tapping a line number marks it. Line tap feedback is immediate.
4. **Pause overlay:** blurred screen with a Resume button. Available once per run.
5. **Results:** score breakdown, mistakes used, streak status, leaderboard rank. If failed, shows a "continue for learning" option.
6. **Leaderboard:** per-language list for today, with a toggle for all-time.
7. **Profile:** current streak per language, best scores, days played.

Mobile layout notes:

- Code panel scrolls horizontally for long lines and keeps a readable monospace size.
- Output panel sits below code and is also scrollable.
- Line numbers are large enough for reliable thumb taps.
- Designed for portrait first. Landscape is optional.

## 11. Platform and technology

- **Client:** React Native with Expo, for iOS and Android from one codebase.
- **Backend:** a lightweight API for accounts, daily set delivery, run submission, scoring, streaks, and leaderboards. Scoring and answer-key checks run only on the server.
- **Database:** PostgreSQL (see section 12).
- **Auth:** email or social sign-in. Anonymous play can be a fallback for early testers, but streaks are tied to accounts.
- **Time:** the server defines the daily boundary as 10:00 UTC.

## 12. Data model (sketch)

- `users` (id, display_name, created_at)
- `languages` (id, code, name)
- `challenge_days` (id, language_id, date, published_at)
- `snippets` (id, challenge_day_id, position, code, expected_output, actual_output, created_at)
- `planted_errors` (id, snippet_id, line_number), server-side only
- `runs` (id, user_id, challenge_day_id, language_id, started_at, submitted_at, status, mistakes, score, time_bonus, total_time_ms)
- `run_taps` (id, run_id, snippet_id, line_number, is_correct, tapped_at)
- `streaks` (user_id, language_id, current_streak, best_streak, last_completed_date)

Constraints:

- One run per user per challenge day per language.
- Taps are unique per run, snippet, and line, which enforces the rule that re-tapping a wrong line doesn't count again.

## 13. Offline and connectivity

- The daily set is downloaded when the run starts, so the player can play on a train with no signal.
- The answer key (planted error lines) is never sent to the device.
- Run results are queued locally and submitted when the device reconnects. The server validates taps, recomputes the score, and updates streaks and leaderboards.
- Time bonus is measured on the device during offline play. Allow a small tolerance for clock differences, and keep the bonus modest.

## 14. Analytics to capture from day one

- Daily active players per language
- Start rate and completion rate per language
- Failure rate and where in the run failures happen (which snippet)
- Mistakes per snippet and per error
- Median time per snippet
- Return rate: percentage of players who play again the next day
- Pause usage
- Snippets with unusually high mistake rates (candidates for rewrite)

## 15. Testing plan

- Two to five engineers playing on real commutes for one to two weeks
- Short debrief after each week: did they finish, did they return, did the bugs feel realistic, did they learn anything, was the scoring understood
- Content review: each day's set checked against expected output by running the code in each language before publication

## 16. Open questions

- Final point values for correct finds, mistakes, and time bonus
- Exact time bonus curve
- Display name rules and whether players can choose usernames
- Whether to show other players' results on a snippet after the day ends
- Whether to add a share card for results in V1

## 17. Future phases (out of scope for V1)

- Practice / puzzle section with difficulty progression, modeled on chess puzzle ratings
- Naming the problem and explanations, inside practice
- Hints, priced and capped, with ad-unlocks before the run
- Ads in practice, with a daily free allowance
- Additional languages
- Interview-prep mode with longer multi-file problems on desktop

---

## Appendix A: Database choice

Recommendation: PostgreSQL.

Reasons:

- The data is relational. Runs connect users, challenge days, languages, snippets, and taps, and the rules depend on those relationships.
- Constraints matter. One run per user per day per language, and unique taps per run, are enforced by the database rather than by application code.
- Scoring and streak updates need transactions. When a run is submitted, the run row, its taps, the streak, and the leaderboard entry should update together.
- Leaderboards are simple ordered queries on `challenge_day_id`, `language_id`, and `score`, which Postgres handles well at V1 scale with an index.
- Content is a good fit for JSON columns in Postgres if you want flexibility for snippets, so you don't need a separate document database.

Why not NoSQL for V1: a document store such as MongoDB or DynamoDB can store snippets easily, but streaks, uniqueness rules, and leaderboard ordering are awkward to enforce across documents. You would end up writing those guarantees in application code.

Practical hosting: a managed Postgres service (for example, Supabase, Neon, or AWS RDS) keeps operations light. Add Redis or a similar cache only if leaderboards become a bottleneck, which is unlikely in early testing.

---

## Appendix B: Glossary

- **Planted error:** an intentional bug in a snippet that the player should find.
- **Mistake:** a tap on a line that contains no planted error.
- **Mistake limit:** half the planted errors in the day's set, rounded up to even, beyond which the run fails.
- **Run:** one player's attempt at one daily set in one language.
- **Daily set:** the ten snippets published for a language on a given date.
