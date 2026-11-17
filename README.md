# IS373 Group Content System — Review 1

Review 1 plan for educational-content publishing. Application behavior and runtime checks are planned. [Review 1 assignment](https://njit.instructure.com/courses/70733/assignments/769189)

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
| Review and publish | A second teammate reopens the original section at approval time and compares the current passage with the draft claim. If the passage changed and no longer supports the claim, the reviewer returns the draft with a reason and requires fresh review before publication. The access date records when the source was read. Students see the guide only after approval. |

### Architecture comparison

| Approach | How it would handle the same question | Tradeoff |
| --- | --- | --- |
| Vector retrieval with RAG | Use PostgreSQL with pgvector to rank team-written source summaries by cosine distance after filtering by course, topic, and current source status. Pass the retrieved summary and its citation to the draft generator. [pgvector documentation](https://github.com/pgvector/pgvector#querying) · [Original RAG paper](https://arxiv.org/abs/2005.11401) | Everyday phrases like “go live” can match ideas like “publication,” but a similar summary could rank first. The reviewer checks the original source before approving. |
| Graph retrieval | Use Cypher to match the path from course to project topic to source version to claim, then return the claim and its citation. [Neo4j Cypher Manual](https://neo4j.com/docs/cypher-manual/current/patterns/) | Explicit relationships make the source version and citation path easy to inspect. The team would need to maintain those relationships and map everyday questions to the right topic or claim. |

**Review 1 architecture choice.** Use PostgreSQL with pgvector for vector retrieval and keep source metadata, citations, and guide review status in PostgreSQL. The first workflow needs to handle student wording and link each draft claim back to a known source. A graph would become more useful if the team later needs to trace which guides are affected when one source supersedes another. [IS373 database/RAG handout](https://kaw393939.github.io/is373-studio/handouts/database-rag-research.html#_2-compare-the-retrieval-approaches)

### Checkable stories

All checks below are planned.

1. **Citation check.** As a reviewer, I can open the passage behind a claim and decide whether it supports the draft. Test a correctly cited draft, then try a missing link, a working link to an unrelated section, a source record marked superseded, and a working URL whose edited passage no longer supports the draft. Pass if the correct draft can proceed to human approval and each bad draft stays unpublished with a recorded reason. Fail if a bad draft can publish or the reviewer cannot locate and verify the supporting passage. **Owner:** Jiyeon Choi. **Reviewer:** Sebastian (BombayV).
2. **Return a draft.** As a reviewer, I can return an inaccurate draft with a reason the author can act on. Pass if the author can see the reason and the returned draft stays out of the student view. **Owner:** Sebastian (BombayV). **Reviewer:** Jiyeon Choi.
3. **Find the approved guide.** As a student, I can find the approved guide for the intended assignment and open its source link. Pass if the approved version and its source link are accessible from the student view. Fail if the guide is missing, the link is broken, or students see a draft, outdated guide, or guide for another assignment. **Owner:** Sebastian (BombayV). **Reviewer:** Jiyeon Choi.

### Peer review and contributions

| Record | Status |
| --- | --- |
| Peer feedback | The team’s draft records Sebastian’s feedback that the explanation was clear and raises a publication concern. Jiyeon also asked how the team would catch an edit if the source URL stayed the same. |
| Decision and documentation edit | Story 3 checks that students can open the approved guide and its source. Story 1 now includes a same-URL edit, and the workflow requires the reviewer to reopen the original passage before approval. These application checks are planned. |
| Jiyeon Choi | AI-assisted draft of the source trace, retrieval comparison, and citation check. [Contribution section](#jiyeon-choi--source-trace-and-citation-check) · [Issue #1](https://github.com/BombayV/is373-group-project/issues/1) |
| Sebastian | Drafted the initial scope, alternatives, and three stories with AI assistance and opened the source-trace task. [Issue #1](https://github.com/BombayV/is373-group-project/issues/1) |

- **Changed:** Drafted the source trace, retrieval comparison, and citation check for the existing plan.
- **Checked:** The public course brief opens and its “Choose a bounded problem” section supports the paraphrased claim about human approval. No runtime checks have been run.
- **Next:** Build the draft, review, and publication workflow and run the three story checks.
