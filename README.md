# SWE-Agent Cloud Service - User Guide

[English](README.md) | [简体中文](README.zh-CN.md)

## Introduction

SWE-Agent Cloud Service is an **AI-powered GitHub automation platform** that provides cloud-based SWE-Agent workstations. Simply comment `/code` in any Issue or PR to trigger cloud execution.

### Core Features

- **Multi-Model Execution**: Supports Claude Sonnet 4.5 and GPT-5 Codex
- **End-to-End Workflow**: Requirement understanding → Auto coding → Isolated testing → PR delivery
- **Transparent Audit**: Real-time cost breakdown and full execution logs

## Key Capabilities

### 🤖 AI Auto-Coding

Connects Claude Sonnet 4.5 and GPT-5 Codex to generate merge-ready code patches with repository context.

- Intelligently understands Issue requirements and PR context
- Automatically selects the most suitable AI model
- Generates code that follows project conventions

### ✅ Full Testing Pipeline

Executes tests in isolated containers with regression analysis and self-healing before submission.

- Docker container isolation
- Automatic test suite execution
- Auto-retry and fix on test failures

### 🚀 Automated PR Workflow

Generates structured PR descriptions with logs and cost reports for transparent and reversible delivery.

- Automatically creates or updates Pull Requests
- Includes complete change descriptions and test results
- Transparent cost and execution time for each task

## Pricing

SWE-Agent Cloud Service uses a **pay-as-you-go** model—you only pay for actual consumption.

### Billing Rules

- **Model Calls**: Charged by actual token consumption
  - Claude Sonnet 4.5: Input $3/M tokens, Output $15/M tokens
  - GPT-5 Codex: OpenAI official pricing
- **Test Tasks**: Container execution time charged per second
- **Cost Transparency**: Each Issue generates independent cost reports and execution logs

### Beta Pricing

**Current Beta Phase Offer**:

| Item | Price |
|------|-------|
| **Minimum Top-up** | $10 USD (~¥13 CNY) |
| **Exchange Rate** | 1 USD = 1.3 CNY (fixed) |
| **Validity** | No expiration during beta |

> 💡 CNY payments are converted to USD balance at a fixed rate of 1.3. All charges are settled in USD.

### Typical Task Cost Estimates

| Task Type | Context | Output | Estimated Cost |
|-----------|---------|--------|----------------|
| Small Bug Fix | 50k tokens | 2k tokens | ~$0.18 |
| Medium Feature | 100k tokens | 5k tokens | ~$0.45 |
| Large Refactor | 200k tokens | 10k tokens | ~$0.90 |

## How to Use

### Step 1: Apply for Whitelist Access

Join the testing program to unlock swe-agent automation.

**Application Methods**:
- Email: `support@stellarlink.co`
- GitHub Issues: [Submit Application](https://github.com/swe-agent-bot/swe-agent/issues)

**Required Information**:
Please provide the following to expedite review:
- GitHub username
- Repository name (if determined)
- Use case description
- Expected concurrent tasks

### Step 2: Install GitHub App

Install the swe-agent GitHub App in your target repository to grant access.

1. Visit [swe-agent GitHub App](https://github.com/apps/swe-agent-bot)
2. Click "Install"
3. Select your organization or personal account
4. Choose repositories to authorize:
   - **All repositories**: Authorize all repos (recommended)
   - **Only select repositories**: Choose specific repos
5. Click "Install & Authorize"

### Step 3: Top Up Balance

Log in to the [Dashboard](https://swe-agent.ai/dashboard) and make your first deposit.

1. Visit the dashboard and log in with your GitHub account
2. Click "Balance" or "Top Up"
3. Enter amount (minimum $10 USD)
4. Scan QR code to pay with WeChat/Alipay in CNY
5. Balance updates automatically after payment

### Step 4: Start Using

Comment `/code` in any Issue or PR with your task description.

**Command Format**:

```bash
/code <task description>
/code --plan <task description>  # Enable plan mode
```

**Parameters**:
- **Default Mode**: Directly execute task, generate code and submit PR
- **`--plan` Mode**: Generate detailed implementation plan first, wait for your confirmation before execution
  - Suitable for complex tasks or when implementation approach is unclear
  - AI will analyze requirements, list implementation steps, assess risks
  - You can suggest modifications to the plan before execution

**Examples**:

1. **Fix Bug** (direct execution):
   ```bash
   /code Fix login button styling issue, ensure proper display on mobile
   ```

2. **Add Feature** (plan mode):
   ```bash
   /code --plan Add email verification for user table, including email sending and validation logic
   ```
   > Use `--plan` for complex features—AI will present implementation approach for your review

3. **Code Refactoring** (plan mode):
   ```bash
   /code --plan Extract authentication logic from UserService into a separate AuthService
   ```
   > Refactoring tasks should use plan mode to avoid breaking existing functionality

4. **Update Documentation** (direct execution):
   ```bash
   /code Update README with new API endpoint documentation
   ```

### Execution Flow

After submitting a `/code` command, SWE-Agent automatically executes:

1. **Task Receipt**: Verify permissions and create task
2. **Context Collection**: Read Issue/PR content, codebase structure, related files
3. **AI Code Generation**: Call AI models to generate code changes
4. **Test Validation**: Run tests in isolated container
5. **Submit PR**: Create or update Pull Request
6. **Result Notification**: Comment task results and cost on original Issue/PR

The entire process typically takes 2-10 minutes, depending on task complexity.

### Check Task Progress

Monitor task execution through:

1. **GitHub Comments**: SWE-Agent continuously updates progress in the original Issue/PR
2. **Dashboard**: Log in to view real-time status of all tasks
3. **Email Notifications**: Receive email when task completes (optional)

## FAQ

### Balance

**Q: How do I check my balance?**
A: Log in to the dashboard to see your current balance at the top.

**Q: What happens if balance is insufficient?**
A: New tasks cannot execute when balance is below $10. Top up first.

**Q: How long until top-up is credited?**
A: Real-time crediting after payment, usually within 10 seconds.

**Q: Are failed tasks charged?**
A: Failed tasks deduct consumed API costs (if any), but refund pre-authorized frozen amounts.

### Permissions

**Q: Why is there no response to my /code command?**
A: Possible reasons:
1. Your GitHub account is not whitelisted
2. You lack collaborator permissions on the repository
3. GitHub App not properly installed on the repository

**Q: How to add team members to whitelist?**
A: Contact admin via support@stellarlink.co to request addition.

### Usage

**Q: Can multiple tasks execute simultaneously?**
A: Yes, supports concurrent Issue processing. Ensure sufficient balance (each task pre-authorizes $2).

**Q: How to cancel a running task?**
A: Cancellation mid-execution is not currently supported, but task status can be viewed in dashboard. Contact support for forced stop.

**Q: How is AI-generated code quality ensured?**
A:
- All code undergoes test validation
- PR creation requires manual code review
- Supports iterative optimization via `/code`

**Q: Which programming languages are supported?**
A: Supports all mainstream languages including:
- JavaScript/TypeScript
- Python
- Go
- Java
- Rust
- PHP
- Ruby

### Troubleshooting

**Q: Task stuck in "Running" status?**
A: Task timeout is 30 minutes; it will auto-fail after timeout. Contact support with task ID if issues persist.

**Q: PR creation failed?**
A: Check:
- GitHub App has sufficient permissions
- Target branch exists
- No conflicting PRs

## Best Practices

### 1. Clear and Specific Task Descriptions

❌ **Bad Example**:
```
/code Optimize code
```

✅ **Good Example**:
```
/code Optimize UserController query performance by using indexes to reduce database query time
```

### 2. Split Large Tasks

For complex features, split into smaller tasks and complete incrementally.

❌ **Bad Example**:
```
/code Refactor entire auth system including login, registration, password reset, OAuth integration
```

✅ **Good Example**:
```
/code Extract authentication logic from UserController into separate AuthService
```
Then submit subsequent tasks.

### 3. Provide Context Information

If task involves specific design patterns or libraries, mention in description.

✅ **Good Example**:
```
/code Add bcrypt password hashing for users, replacing current plaintext storage
```

### 4. Leverage PR Context

Use `/code` in existing PR comments—AI will automatically update that PR, avoiding duplicate branches.

### 5. Use Plan Mode Wisely

**When to use `--plan`**:
- ✅ Complex feature development (involves multiple files or modules)
- ✅ Code refactoring (need to assess impact scope)
- ✅ Unclear implementation approach (want to review plan first)
- ✅ Critical system changes (requires careful review)

**When to execute directly**:
- ✅ Simple bug fixes
- ✅ Documentation updates
- ✅ Configuration file adjustments
- ✅ Minor styling changes

**Example Comparison**:

```bash
# Simple task - direct execution
/code Fix button click unresponsive issue

# Complex task - use plan mode
/code --plan Refactor user authentication flow to support multi-factor authentication (MFA)
```

## Support & Feedback

### Contact

- **Email**: support@stellarlink.co
- **GitHub Issues**: [Submit Issue](https://github.com/swe-agent-bot/swe-agent/issues)
- **Documentation**: [Online Docs](https://github.com/swe-agent-bot/swe-agent/blob/main/README.md)

### Feedback Channels

We welcome your feedback and suggestions:
- Feature Requests: Create Feature Request on GitHub Issues
- Bug Reports: Create Bug Report on GitHub Issues
- Usage Questions: Email support@stellarlink.co

---

<div align="center">

**Start using SWE-Agent Cloud Service—let AI become your coding assistant!**

[Visit Dashboard](https://swe-agent.ai/dashboard) | [View Demo](https://github.com/cexll/myclaude/issues/17)

</div>


