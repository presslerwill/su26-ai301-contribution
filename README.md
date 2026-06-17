# Contribution [1]: [test(agent): cover honeypot_post_session pure-parser helpers]

**Contribution Number:** [1]  
**Student:** [Will Pressler]  
**Issue:** [[GitHub issue link](https://github.com/InnerWarden/innerwarden/issues/819)]  
**Status:** [Phase I] [Complete]

---

## Why I Chose This Issue

I chose this issue because of the opportunity it presents for growth. I am interested in learning more about cybersecurity as a software engineer and this project is perfect to start learning. Innerwarden is a security AI agent that autonomously fights against real security threats, so while working on the issue I will get to learn more about cybersecurity and how AI agents interact with security. I have some prior educational experience with cybersecurity, but this will be the first opportunity for me to build skills of a cybersecurity software engineer, not just a regular engineer. 
Furthermore, I wanted to tackle an issue with a tech stack that is new to me. I want to expand beyond the tech stack I work with on a day to day basis, and this project uses Rust, which is completely new to me. So while working on the issue I hope to learn Rust and be able to contribute more to Rust projects in the future.

---

## Understanding the Issue

### Problem Description

[In your own words, what's broken or missing?]

### Expected Behavior

[What should happen?]

### Current Behavior

[What actually happens?]

### Affected Components

[Which parts of the codebase are involved?]

---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]
Remember to install RUST! I didn't have Rust installed prior to this...
I also used a WSL and Kali Linux to run the project as I am on a Windows machine, should be a disclaimer that it is easier to run on Mac or Linux systems.

### Steps to Reproduce

1. From a WSL2 Kali terminal, install build prerequisites: sudo apt update && sudo apt install -y build-essential pkg-config git
2. Install Rust via rustup, not Kali's apt package — Kali/Ubuntu ship rustc 1.75, but this repo's Cargo.lock uses lockfile format v4, which requires roughly Rust 1.83+. Running cargo with the apt version fails immediately
   with lock file version 4 requires -Znext-lockfile-bump. Use: curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y then source "$HOME/.cargo/env".
3. Clone your fork and check out the branch: git clone https://github.com/presslerwill/innerwarden.git && cd innerwarden && git checkout fix-issue-honeypot-coverage
4. Install the coverage tooling the issue itself uses to measure the gap: rustup component add llvm-tools-preview && cargo install cargo-llvm-cov
5. Run the command cited in the issue: cargo llvm-cov -p innerwarden-agent --no-fail-fast --json --summary-only, and inspect crates/agent/src/honeypot_post_session.rs.
Observed result: The file honeypot_post_session.rs is at 61% line coverage (231/378 lines).

### Reproduction Evidence

- **Commit showing reproduction:** [[Link to commit in your fork]](https://github.com/presslerwill/innerwarden/tree/fix-issue-honeypot-coverage)
- **Screenshots/logs:** [If applicable]
- **My findings:** The file honeypot_post_session.rs is at 61% line coverage (231/378 lines). This needs to be increased to at least 80%, the higher the better.

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** 
After a honeypot is set to detect malicious actors, the honeypot_post_session.rs file runs after the session. It currently is under 80% line coverage so the fucntions in the file need more tests added to 
the unit test suite to reach sufficient coverage.

**Match:** [What similar patterns/solutions exist in the codebase?] 
There are other files, such as narrative_autofp.rs, that follow a similar format with unit tests. They can be referenced for how to structure the test 
suite and what kind of tests should be added.

**Plan:** [Step-by-step implementation plan]
1. Within the honeypot_post_sessions.rs file, under the #[cfg(test)] heading, add robust tests that test the edge cases and paths without coverage.
2. Run the existing test suite to see where the tests are covering the source code.
3. Add unit tests that specifically test uncovered lines in the source code.

**Implement:** [Link to your branch/commits as you work] 
[Working branch](https://github.com/presslerwill/innerwarden/tree/fix-issue-honeypot-coverage)

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]


**Evaluate:** [How will you verify it works?]
I will run the test coverage to ensure that the line and branch coverage has increased above the desired threshold. Also, I will use the debugger to step through each test I added and ensure that each test is robust and 
tests a real requirement or edge case. 
The issue also lists these criteria to evaluate my changes: At least 6 new tests under crates/agent/src/honeypot_post_session.rs's #[cfg(test)] mod tests block. cargo test -p innerwarden-agent --bins honeypot_post_session 
passes. No production code changes — these three functions are already pub(crate) and pure.

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
