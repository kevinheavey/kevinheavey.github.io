---
layout: post
title: "How to top every leaderboard on highload.fun"
description: "How I reached the top of every working Highload leaderboard in three days."
show_description: false
image: /assets/highload/social-preview.png
image_width: 1730
image_height: 909
image_alt: "Top scores on highload.fun in Zig, C/C++, C#, Go, and Rust"
date: 2026-09-28
---

[Highload.fun](https://highload.fun) is a popular competitive programming platform for performance optimisation. In recent months it has of course become [dominated by AI](https://josusanmartin.com/blog/2026/01/18/the-game-has-changed-vibecoded-highload.html). If you enjoy reading Intel documentation this makes it less interesting. If you enjoy doing stuff with AI this makes it far more interesting, and you may like to hear how I reached the top of every working Highload leaderboard in three days.

![Top scores across five languages](/assets/highload/top-scores.jpg)

![Highload.fun compute challenges leaderboard](/assets/highload/leaderboard.jpg)

*What Highload looks like now*

1. **Use the right model, obviously.** I started this brief adventure by trying out Opus 5.5 on the *Parse Integers* challenge, where GPT 5.5 Sol had got me to third place. Astra had failed to make progress on it and Fable [refused](https://x.com/dj_d_sol/status/2080726431772839956), so when Opus 5.5 Medium topped the leaderboard in an hour or so, I could see it was very special. It then cost only about half a week’s usage on a Claude Max 20x subscription to win all the other challenges. However, Opus 5.5 is no secret and Highload has been active without anyone beating my records yet, so we must consider what else is needed beyond spamming AI.

2. **Automate submissions.** This should also be obvious, even if Highload was not exactly built with automation in mind. Copy-pasting and checking the scoreboard yourself takes far too long. AI can automate this quickly, just make sure it’s not doing some silly computer use thing.

3. **Rent a near-identical server.** This is not obviously necessary to an outsider, but the top submissions are very tuned to the particular Haswell box that they run on. There is no good substitute for having a close replica of the deployment host: it makes your local benchmarks much more accurate and allows you to use perf counters to figure out what the bottlenecks are. I was able to get one from Circle City Servers for $65 per month. You might be able to go even cheaper if you can find somewhere with daily billing. Also, don’t use llvm-mca or uiCA to try and simulate this stuff. Claude often wanted to use these but they were always a waste of time.

4. **Do the challenges in the right order.** *Count uint8* is a good place to start because it’s about reading bytes as fast as possible, and almost all challenges benefit from that. You don’t even need to figure out the order after that. This was my go-to prompt that usually one-shotted first place:

   > What’s a good next highload challenge that builds on what we’ve achieved so far? Pick one and go work on it to get us in first place. Commit and push as you go along. You don’t need to ask me before submitting

5. **Understand how you are scored.** Every submission is run nine times, and your score is based on the fifth-best run. So some challenges are best approached with a solution that is usually very fast but occasionally horrendous.

6. **Be aware of the best optimisations.** Without going into detail, there were a handful of tricks that Claude needed to be reminded of, even if it was the one who discovered them in the first place.

7. **Port the solutions to the other languages (Zig, Go etc).** This is easy, just make sure your clanker is not trying to be idiomatic or express its artistic soul with this work.

8. **(Optional) Get a time machine to win the unbeatable MD5 challenge.** This challenge is currently broken because recent submissions always run a bit slower than they used to, and unlike the other challenges it’s already at its theoretical floor modulo machine noise. I thought it would be undignified to complain about this since I already hammered the server to win the 24 other challenges.

9. **(Optional) Get a time machine to top the home-page leaderboard.** There is a Reputation Points leaderboard on the home page of highload.fun. Being first in every challenge only took me to third place, because it rewards beating existing records by huge margins, which is something that the top two guys did a lot of and which is much harder to do now. So the top two might stay there forever

Notwithstanding the MD5 issue above, I think there is still plenty of juice left to squeeze out of these challenges. I, however, will retire from highload.fun and leave that for others to enjoy. I hope to see myself dethroned soon!
