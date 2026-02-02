# POST_EXECUTION Hook

This hook executes after all blueprint phases complete successfully, before execution summary generation and plan archival.

## Validation Gates

Before marking the blueprint as complete, verify:

### 1. Code Quality Checks

- Run project linting checks if configured (e.g. `npm run lint`, `npm run eslint`, or equivalent)
- All linting rules must pass without errors
- If no linter is configured, skip this step

### 2. Test Suite Validation

- Run project test suite if configured (e.g. `npm test`, `npm run test:integration`, or equivalent)
- All tests must pass successfully
- If no test suite is configured, skip this step

### 3. Task Completion Verification

- Verify all tasks in the plan have `status: "completed"` in their frontmatter
- Check that no tasks remain with `status: "pending"` or `status: "in-progress"`
- Confirm all phase checkmarks (✅) are present in the blueprint section

## Reporting

Provide a comprehensive execution summary:

- **Phases Completed**: List all phases executed
- **Tasks Accomplished**: Count of total tasks completed
- **Features Delivered**: High-level summary of what was built
- **Test Coverage**: Report on test execution results (if applicable)
- **Code Quality**: Report on linting results (if applicable)

## Failure Behavior

If any validation gate fails:

- **Halt execution immediately** - do not proceed to summary generation or archival
- **Leave plan in `plans/` directory** for debugging and correction
- **Document the failure** in the plan file with details about which gate failed
- **Provide actionable next steps** for resolving the failure
