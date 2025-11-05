---
description: Update waypoint plan before context compaction in Claude Code
argument-hint: Optional - specific context or tasks to focus on (leave empty for comprehensive update)
---

We're approaching context limits. Please update the waypoint plan documentation to ensure seamless continuation after context reset.

## 🔄 New Workflow: Task-First Updates

**This command now enforces integrated task tracking**:

1. ✅ **FIRST**: Update `[task-slug]-tasks.md` (mark completed tasks, calculate progress)
2. ✅ **THEN**: Update `[task-slug]-context.md` SESSION PROGRESS (using task status from step 1)
3. ✅ **VERIFY**: Ensure both files are synchronized and consistent

**Why this matters**: Tasks.md is the source of truth. Context.md SESSION PROGRESS reflects task status. This prevents:
- Forgetting to update task checklists
- Progress mismatches between files
- Losing track of what's actually done
- Resuming with stale or incorrect task status

## Priority: Update Tasks First, Then SESSION PROGRESS

**Critical workflow order**: Update `tasks.md` → then use task status to inform `context.md` SESSION PROGRESS.

This ensures consistency between task checklists and progress tracking.

### For each active task in `plans/active/*/`:

#### Step 1: Review and Update Tasks File

**File**: `[task-slug]-tasks.md`

1. **Read the entire tasks file** and identify completed tasks based on work done this session
2. **Mark completed tasks** with `[x]`
3. **Add IN PROGRESS marker** to current task: `- [ ] Task description **(IN PROGRESS)**`
4. **Calculate progress**: Count completed vs total tasks (e.g., "8/15 tasks = 53%")
5. **Verify acceptance criteria**: Ensure marked tasks meet their completion criteria
6. **Add newly discovered tasks** if requirements expanded
7. **Update task order** if priorities changed

**Example before:**
```markdown
### Phase 1: Foundation
- [x] Set up project structure
- [ ] Implement authentication
- [ ] Create database schema
```

**Example after:**
```markdown
### Phase 1: Foundation (2/3 tasks = 67%)
- [x] Set up project structure
- [x] Implement authentication **(COMPLETED THIS SESSION)**
- [ ] Create database schema **(IN PROGRESS)**
```

#### Step 2: Update Context File SESSION PROGRESS

**File**: `[task-slug]-context.md`

Now update the `## SESSION PROGRESS` section **using task status from Step 1**:

```markdown
## SESSION PROGRESS (YYYY-MM-DD HH:MM)

**Progress**: [X/Y tasks completed = Z%] ← FROM TASKS.MD STEP 1

### ✅ COMPLETED THIS SESSION
[Copy completed tasks from tasks.md - be specific with file names]
- Task 1 [x] from tasks.md
- Task 2 [x] from tasks.md

### 🟡 IN PROGRESS
[Copy current task marked with **(IN PROGRESS)** from tasks.md]
- Current task details
- File: [exact file path]
- Function/Component: [exact name]

### ⏳ PENDING
[Copy upcoming unchecked tasks from tasks.md in priority order]
- Next task from tasks.md
- Following task from tasks.md

### 🚫 BLOCKED (if any)
[Specific blockers with what's needed to unblock]
- Cross-reference with any blocked tasks in tasks.md

### 🎯 NEXT ACTION
[VERY SPECIFIC next step aligned with current **(IN PROGRESS)** task in tasks.md]
Example: "Implement refreshToken() function in lib/supabase/auth.ts to handle expired tokens (Task 3 from tasks.md)"
```

**Consistency check**: Verify that:
- ✅ COMPLETED section matches `[x]` tasks in tasks.md
- 🟡 IN PROGRESS matches the `**(IN PROGRESS)**` task in tasks.md
- ⏳ PENDING matches remaining `[ ]` tasks in tasks.md
- Progress percentage is accurate (count tasks in tasks.md)

## Required Updates

### 1. Update Active Task Context Files

For each `[task-slug]-context.md`:

**Key Decisions Section**:
```markdown
## KEY DECISIONS

### Decision: [Title] (YYYY-MM-DD)
**Chose**: [What was decided]
**Rationale**: [Why this approach]
**Alternatives**: [What else was considered]
**Impact**: [Files affected, breaking changes]
```

**Important Discoveries Section**:
```markdown
## IMPORTANT DISCOVERIES

### [Discovery Title]
[Technical findings, gotchas, important patterns discovered]
```

**Files Modified Section**:
```markdown
## FILES MODIFIED

### Created
- `path/to/file.ts` - [Purpose]

### Modified
- `path/to/file.ts` - [What changed and why]
```

**Quick Resume Section**:
```markdown
## QUICK RESUME

To continue this work:
1. Read this file (context.md) for current state
2. Check tasks.md for checklist
3. Refer to plan.md for overall strategy
4. Current file: [exact file path]
5. Current function/component: [exact name]
6. Next step: [specific action to take]
7. After that: [following step]
8. Expected time: [estimate for next step]
```

### 2. Verify Task-Context Synchronization

**After updating both files, verify consistency**:

For each waypoint (`[task-slug]-tasks.md` and `[task-slug]-context.md`):

**Cross-reference check**:
- [ ] Count of completed tasks matches between files
- [ ] Current task **(IN PROGRESS)** appears in both files
- [ ] Progress percentage in context.md matches tasks.md count
- [ ] NEXT ACTION in context.md aligns with current task in tasks.md
- [ ] Blocked tasks (if any) are noted in both files

**If inconsistencies found**:
1. **Tasks.md is source of truth** for task status
2. Update context.md SESSION PROGRESS to match tasks.md
3. Ensure file modifications support completed task claims
4. Document any gaps in acceptance criteria

### 3. Capture Session-Specific Context

Include in relevant context.md files:

**Complex Problems Solved**:
- What was the problem?
- What approach worked?
- Why did other approaches fail?
- Code examples if relevant

**Tricky Bugs Fixed**:
- Bug description
- Root cause
- Fix applied
- How to prevent similar bugs

**Architectural Decisions**:
- What changed in architecture
- Rationale for the change
- Impact on other components
- Migration path if breaking

**Integration Discoveries**:
- How components/services interact
- API contracts discovered
- Data flow patterns
- Edge cases found

### 4. Update Memory Files (if applicable)

If significant preferences or patterns emerged, update:

**`.claude/memory/project/knowledge.json`**:
```json
{
  "tech_stack": { /* current stack info */ },
  "structure": { /* project organization */ },
  "last_verified": "YYYY-MM-DD"
}
```

**`.claude/memory/project/decisions.json`**:
```json
{
  "decisions": [
    {
      "id": "unique-id-YYYY-MM-DD",
      "date": "YYYY-MM-DD",
      "decision": "What was decided",
      "rationale": "Why",
      "alternatives_considered": ["Alt 1", "Alt 2"],
      "impact": "How it affects project",
      "files_affected": ["list", "of", "files"]
    }
  ]
}
```

### 5. Document Unfinished Work

**Critical for resume**:

```markdown
## UNFINISHED WORK

### What I Was Doing
[Exact task being worked on when context limit approached]

### Exact State
- File: [exact file path]
- Function/Component: [exact name]
- Line number: [if relevant]
- What was being implemented: [specific detail]

### Why It's Unfinished
[Blocker, context limit, or just in progress]

### To Complete It
1. [Specific step 1]
2. [Specific step 2]
3. [Specific step 3]

### Test Commands
```bash
# Commands to verify the work when resumed
npm run test
npm run build
```
```

### 6. Update All Timestamps

Ensure all files have current timestamps:
```markdown
**Last Updated**: YYYY-MM-DD HH:MM
```

## Additional Context: $ARGUMENTS

## Verification Checklist

Before finishing, verify **in this order**:

### Phase 1: Tasks File (Source of Truth)
- [ ] **Read** `[task-slug]-tasks.md` completely
- [ ] **Identified** all completed tasks from this session
- [ ] **Marked** completed tasks with `[x]`
- [ ] **Added** `**(IN PROGRESS)**` marker to current task
- [ ] **Calculated** progress percentage (X/Y tasks = Z%)
- [ ] **Verified** acceptance criteria met for completed tasks
- [ ] **Added** any newly discovered tasks
- [ ] **Updated** task priorities if needed

### Phase 2: Context File (Derived from Tasks)
- [ ] **Copied** task status from tasks.md to SESSION PROGRESS
- [ ] **Updated** SESSION PROGRESS with current timestamp
- [ ] **Matched** progress percentage from tasks.md
- [ ] **Aligned** NEXT ACTION with current **(IN PROGRESS)** task
- [ ] **Listed** completed tasks from tasks.md in ✅ COMPLETED section
- [ ] **Listed** pending tasks from tasks.md in ⏳ PENDING section

### Phase 3: Consistency Validation
- [ ] **Verified** completed task count matches between both files
- [ ] **Verified** current task matches between both files
- [ ] **Verified** progress percentage is accurate
- [ ] **Verified** file modifications support completed tasks

### Phase 4: Additional Documentation
- [ ] Key decisions documented with rationale
- [ ] Files modified section is complete
- [ ] Quick resume instructions are current
- [ ] All timestamps updated
- [ ] Any blockers clearly described with unblock requirements

## After Updating

**Report to user**:

1. **Files updated**: List both tasks.md and context.md files
2. **Progress summary**: "Completed X/Y tasks (Z%)" from tasks.md
3. **Current task**: Show what's marked **(IN PROGRESS)** in tasks.md
4. **Next action**: Specific step from context.md NEXT ACTION
5. **Consistency status**: "✅ Tasks and context are synchronized"
6. **Resume confidence**: "Ready to continue after context reset (< 60 second resume)"

**Example report**:
```
Updated waypoint files:
- plans/active/auth-implementation/auth-implementation-tasks.md
- plans/active/auth-implementation/auth-implementation-context.md

Progress: 8/15 tasks completed (53%)
Current task: Implement token refresh in auth.ts **(IN PROGRESS)**
Next action: Add refreshToken() function to handle expired tokens

✅ Tasks and context are synchronized
✅ Ready for seamless continuation after context reset
```

**Priority**: Focus on capturing information that would be hard to rediscover or reconstruct from code alone. The goal is < 60 second resume time after context reset.

## See Also

- `.claude/skills/context-persistence/SKILL.md` - Full waypoint plan patterns
- `.claude/skills/memory-management/SKILL.md` - Memory storage patterns
- `/create-plan` - Create new waypoint plan structure
- `/resume` - Resume work from existing context
