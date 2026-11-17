# IS373 Group Content System — Review 1

Draft for team review. The scope below is proposed. Architecture, source permission, and story assignments are pending. No runtime checks have been run.

## Reader and problem

Proposed topic: educational-content publishing. An IS373 student needs to find the current instructions for a review and verify them against official material. Can a shared drafting and review workflow help students find accurate instructions and help reviewers catch unsupported or outdated claims? We need evidence for the assumption that students struggle when instructions are spread across multiple pages.

## Permitted source and workflow

Source trace pending. Record the original source's title, URL, version or access date, and what reuse is permitted. Keep restricted excerpts out of this public repository.

Proposed workflow: select a permitted source → extract a claim and retain its source location → save a cited guide as a draft → have another teammate check the claim against the original → approve the guide for student access or return it with a reason.

## Architecture alternatives

- Vector retrieval with RAG finds passages by meaning and can help draft cited guides. Check whether similar assignments or older instructions crowd out the correct source.
- Graph retrieval can link courses, assignments, source versions, and guides explicitly. Check whether the team can maintain those links and whether students can find guides using everyday wording.

Decision pending. Compare both on the same source trace, citing original technical material. Consider evidence quality, version handling, and maintenance effort.

## Checkable stories

All checks are planned. Name one owner and a different reviewer per story.

1. A reviewer opens the exact passage supporting a guide claim. A missing or unsupported citation fails. Owner and reviewer pending.
2. A reviewer returns an inaccurate draft with a reason the author can act on. The returned draft stays out of the student view. Owner and reviewer pending.
3. A student finds the approved guide for the intended assignment and can identify its current source. Draft, stale, or wrong-assignment results fail. Owner and reviewer pending.

## Peer review and contributions

Peer feedback pending. Ask a peer to follow the source trace and challenge an assumption or tradeoff. Record the feedback, team decision, and any resulting documentation change. Each member adds a contribution note with links to their own work.

- **Changed:** Drafted the proposed scope, alternatives, and three stories with AI assistance.
- **Checked:** No project checks run.
- **Next:** Confirm the topic, complete the source trace and comparison, and collect peer feedback. See [teammate research task](../../issues/1).

[Review 1 assignment](https://njit.instructure.com/courses/70733/assignments/769189)
