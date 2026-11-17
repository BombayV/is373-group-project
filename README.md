# IS373 Group Content System — Review 1

Draft for team review. The scope and architecture below are proposed. The citation check has not been run. [Review 1 assignment](https://njit.instructure.com/courses/70733/assignments/769189)

## Reader and problem

An IS373 student needs to find current instructions for a project review and verify them against official material. Can a shared drafting and review workflow help students find accurate instructions and help reviewers catch unsupported or outdated claims?

**Observation.** The public group-project brief explains the publishing workflow, and the Canvas assignment contains the Review 1 submission instructions. **Assumption.** Students have trouble finding the right information across course pages. We have yet to verify that assumption with a student.

## Jiyeon Choi — source trace and citation check

### Permitted source and workflow

**Source record.** Keith Williams, *Deliverable 3 - Group content system + problem research*, “Choose a bounded problem,” accessed November 17, 2026. For this public plan, use the link and a short team-written paraphrase. The proposed import uses that paraphrase and source metadata. Broader copying or indexing of course pages needs permission. [Original course brief and passage](https://kaw393939.github.io/is373-studio/projects/group.html#choose-a-bounded-problem)

**Verified claim.** The instructor’s brief says the educational-content workflow can automate preparation while keeping human approval before publication. Accordingly, our proposed guide will stay in draft until a teammate approves it.

| Step | Proposed behavior |
| --- | --- |
| Extract | A teammate opens “Choose a bounded problem,” identifies the sentence about human approval, and records a paraphrase and the section link. |
| Store | Save the paraphrase, source title, section link, access date, and topic in a source record. Store the guide separately as a draft linked to that record. |
| Retrieve | For “Can an automatically prepared study guide go live right away?”, search the approved educational-content records and retrieve the record about human approval. |
| Draft | Show “A teammate must approve our automatically prepared study guide before it goes live.” Link the draft sentence to the [original passage](https://kaw393939.github.io/is373-studio/projects/group.html#choose-a-bounded-problem). |
| Review and publish | A second teammate opens the link, confirms that the passage supports the claim, and records approval or returns the draft with a reason. Students see the guide only after approval. |

### Architecture comparison

| Approach | How it would handle the same question | Tradeoff |
| --- | --- | --- |
| Vector retrieval with RAG | Use PostgreSQL with pgvector to rank team-written source summaries by cosine distance after filtering by course, topic, and current source status. Pass the retrieved summary and its citation to the draft generator. [pgvector documentation](https://github.com/pgvector/pgvector#querying) · [Original RAG paper](https://arxiv.org/abs/2005.11401) | Everyday phrases like “go live” can match ideas like “publication,” but a similar summary could rank first. The reviewer checks the original source before approving. |
| Graph retrieval | Use Cypher to match the path from course to project topic to source version to claim, then return the claim and its citation. [Neo4j Cypher Manual](https://neo4j.com/docs/cypher-manual/current/patterns/) | Explicit relationships make the source version and citation path easy to inspect. The team would need to maintain those relationships and map everyday questions to the right topic or claim. |

**Recommendation for team review.** Start with vector retrieval and source metadata in PostgreSQL. The first workflow needs to handle student wording and link each draft claim back to a known source. A graph would become more useful if the team later needs to trace which guides are affected when one source supersedes another. The team’s architecture decision is pending. [IS373 database/RAG handout](https://kaw393939.github.io/is373-studio/handouts/database-rag-research.html#_2-compare-the-retrieval-approaches)

### Checkable stories

All checks below are planned.

1. **Citation check.** As a reviewer, I can open the passage behind a claim and decide whether it supports the draft. Test a correctly cited draft, then try a missing link, a working link to an unrelated section, and a source record marked superseded. Pass if the correct draft can proceed to human approval and each bad draft stays unpublished with a recorded reason. Fail if a bad draft can publish or the reviewer cannot locate and verify the supporting passage. **Proposed owner:** Jiyeon Choi. **Proposed reviewer:** Sebastian (BombayV).
2. **Return a draft.** As a reviewer, I can return an inaccurate draft with a reason the author can act on. Pass if the author can see the reason and the returned draft stays out of the student view. Owner and reviewer pending.
3. **Find the approved guide.** As a student, I can find the approved guide for the intended assignment and open its source link. Pass if the approved version and its source link are accessible from the student view. Fail if the guide is missing, the link is broken, or students see a draft, outdated guide, or guide for another assignment. Owner and reviewer pending.

### Peer review and contributions

| Peer feedback | Sebastian said the explanation was clear and raised the concern that the guide might not be published correctly. |
| Team decision and documentation edit | Proposed: Update Story 3 to check that students can open the approved guide and its source link after publication. Team confirmation is pending. |

| Record | Status |
| --- | --- |
| Peer feedback | Pending real peer response. |
| Team decision and documentation edit | Pending feedback. Add the decision, what changed, and the edit or commit link here. |
| Jiyeon Choi | AI-assisted draft of the source trace, retrieval comparison, and citation check. [Contribution section](#jiyeon-choi--source-trace-and-citation-check) · [Issue #1](https://github.com/BombayV/is373-group-project/issues/1) |
| Sebastian | Drafted the initial scope, alternatives, and three stories with AI assistance and opened the source-trace task. [Issue #1](https://github.com/BombayV/is373-group-project/issues/1) |

- **Changed:** Drafted the source trace, retrieval comparison, and citation check for the existing plan.
- **Checked:** The public course brief opens and its “Choose a bounded problem” section supports the paraphrased claim about human approval. No runtime checks have been run.
- **Next:** Collect peer feedback, record the team’s decision and edit, and confirm the remaining story assignments.
