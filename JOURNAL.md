## Week 7 - Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/97

**Issue title:** Review progress indicator doesn't update in real time during long-running reviews

**Tier:** [ ] Tier 1  [ ] Tier 2  [x] Tier 3

**Problem summary:**

During a long-running review, the user currently sees a fixed loading spinner instead of progress that changes as the review runs. This can make the application appear stuck even when the review is still processing normally. The backend already provides review status information, but the frontend is not currently reflecting those updates in real time. A successful fix would restore meaningful progress feedback on the review page, primarily around `ReviewPage.tsx` and `useReviewStatus.ts`.

**Branch name:** `fix/97-review-progress-indicator`

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

### Issue selection notes

I chose this issue because the problem is clearly defined and has a visible impact on the user experience. The issue identifies `frontend/src/pages/ReviewPage.tsx` and `frontend/src/hooks/useReviewStatus.ts` as clear starting points, and I have read the relevant code to understand how the current polling and loading behavior works.

The expected before-and-after behavior is also concrete. Today, a long-running review only shows a static spinner, which makes it difficult to tell whether processing is still active. After the fix, the review page should reflect changing progress or status information while the existing polling flow continues to run.

I am comfortable taking on this Tier 3 issue because I can trace the React hook, API polling flow, TypeScript types, and the surrounding review-page logic well enough to form a rough implementation plan. I also investigated the existing frontend tests and confirmed that there are currently no tests specifically for `ReviewPage.tsx` or `useReviewStatus.ts`, so I know new coverage will likely need to be added.

The scope appears realistic for Weeks 8–9, and the issue does not list any unresolved blocker or dependency. The main risk is that further investigation may reveal that frontend types, backend progress fields, or additional tests also need changes, so I will verify the API contract before deciding the final implementation scope.

I also checked the issue comments and know that multiple students have already expressed interest in Issue #97. Since CodePath treats claims as non-exclusive, I am comfortable proceeding with the issue.

## Week 8 - Reproduction & solution planning

**Reproduction commit link:** [to be added after reproduction commit]

**Reproduction summary:**
I reproduced the issue locally by logging into the PathReview app, starting a new portfolio review, and following the review flow to the results page. During processing, the review experience did not show any meaningful progress information, and the status response ultimately returned `progress_pct: 0`, confirming that the current flow does not provide real progress updates to the user.

**PLAN.md link:** [to be added after PLAN.md is committed]

**Walkthrough video (recommended):** Not recorded

**Blockers or open questions:**
The remaining design decisions are how to represent coarse progress milestones and how strictly to type the status response. I’ll resolve those in `PLAN.md` while keeping the existing polling architecture.

