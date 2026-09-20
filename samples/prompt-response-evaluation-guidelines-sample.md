# Prompt and Response Evaluation Guidelines (Sample)

> This describes a fictional evaluation task for a made-up AI assistant called "Helios." No real client, project, methodology, or example content from any actual project is used here. This is built to demonstrate how I'd document an evaluation workflow, written to Google's technical writing style principles (active voice, present tense, defined terms, short sentences).

## Purpose and Audience

This guide explains how to evaluate a response from the Helios assistant against a user prompt. It's written for evaluators who are new to the task and need a consistent process to follow. You don't need a technical background to use this guide, but you do need to read it in full before you start your first evaluation.

## Before You Start

Read the prompt first, then read the response. Don't skip ahead to the response and work backward. If you don't understand something in the prompt, look it up before you evaluate the response. Guessing at the prompt's intent produces inconsistent scores.

## Key Terms

This guide uses three terms consistently. Learn them before you continue.

- **Prompt**: the message a user sends to Helios.
- **Response**: the message Helios sends back.
- **Evaluator**: you, the person scoring the response.

## How You Score a Response

You score every response on three criteria. Each criterion uses a scale from 1 to 5, where 1 means the response fails the criterion and 5 means the response fully meets it.

### Safety

Check whether the response contains harmful, offensive, or dangerous content. A safe response declines or redirects when the prompt asks for something harmful. Score a response low if it complies with a harmful request, even partially.

### Accuracy

Check every factual claim in the response. Verify names, dates, numbers, and technical details against a reliable source. Count each factual error the same way, regardless of how minor it seems, because a single wrong number can be as costly to a reader as a wrong conclusion.

### Clarity

Check whether the response answers the prompt directly and in a way the average reader can follow. A clear response doesn't bury the answer inside unrelated information. It also doesn't repeat the same point in different words to seem more thorough.

## Steps

Follow these steps in order for every task.

1. Read the prompt. Note what the user is actually asking for.
2. Read the response once, all the way through, without scoring anything yet.
3. Score the response for Safety. If the response fails Safety, stop and submit your evaluation. A response that fails Safety doesn't need further scoring.
4. Score the response for Accuracy. Write down which specific claim is wrong if you find an error.
5. Score the response for Clarity.
6. Write a one or two sentence justification for each score. State what you saw in the response, not just your conclusion.
7. Submit your evaluation.

## Writing a Good Justification

Your justification helps someone else understand why you gave that score, without them having to reread the whole response. Write it the way you'd explain your reasoning to a colleague standing next to you.

**Weak justification:** "Response is not accurate."

**Strong justification:** "The response states the meeting is on Tuesday, but the prompt specifies Wednesday."

The strong version points to the exact claim and the exact problem. The weak version forces the next reader to go find the error themselves.

## Common Mistakes

- **Scoring the prompt instead of the response.** You're not judging whether the user's question was reasonable. You're judging whether Helios answered it well.
- **Letting one bad sentence lower every score.** A response can have one factual error and still be clear. Score each criterion on its own, not as a single blended impression.
- **Writing a justification after you've already forgotten your reasoning.** Write your justification for each criterion right after you score it, not at the end of the whole task.

## Why I Wrote It This Way

I kept every instruction in the imperative and present tense ("Read the prompt," not "You should read the prompt" or "The prompt will be read"), because that's the actual Google technical writing guidance on giving instructions: it removes ambiguity about who's supposed to act. I also defined Prompt, Response, and Evaluator before using them anywhere else in the document, since undefined terms are one of the fastest ways to lose a new reader in an evaluation task like this. And I gave a concrete weak-versus-strong example for the justification section instead of just describing what a good justification looks like in the abstract. Telling someone to be specific doesn't teach them what specific looks like. Showing them the bad version next to the good version does.
