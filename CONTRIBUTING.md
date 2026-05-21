# Contributing to Agentic Collections

Add skills to the Red Hat Agentic Collections marketplace.

## How to Contribute

The fastest way to contribute is using `/agentic-contribution-skill` in Claude Code. It guides you through everything: discovery, definition, generation, validation, and git workflow.

### Two paths

**Have an idea for a new skill?**

```
/agentic-contribution-skill
# Choose "Create" → answer discovery questions → skill is generated and validated
```

**Already have a SKILL.md?**

```
/agentic-contribution-skill
# Choose "Import" → point to your file → skill is analyzed, adapted, and validated
```

### Quick start

1. Fork and clone the repository
2. Open the project in Claude Code
3. Run `/agentic-contribution-skill` and follow the prompts

The skill handles pack selection, CLAUDE.md routing, validation (Tier 1 + Tier 2), and git workflow automatically.

## Pack Selection

Each pack targets a specific persona. Choose the one that matches your skill:

| Pack | Persona | Use when |
|------|---------|----------|
| `rh-sre` | Site Reliability Engineers | CVE remediation, system compliance, RHEL automation |
| `rh-developer` | Application Developers | App deployment, S2I builds, Helm charts |
| `rh-virt` | Virtualization Admins | VM lifecycle, snapshots, migrations |
| `ocp-admin` | OpenShift Administrators | Cluster management, health reports, monitoring |
| `rh-ai-engineer` | AI/ML Engineers | Model serving, vLLM, KServe, NVIDIA NIM |
| `rh-automation` | Automation Leads | Ansible AAP governance, safety checks |
| `rh-basic` | General Red Hat Users | CVE diagnostics, lifecycle, patching |
| `rh-support-engineer` | Support Engineers | Technical support, troubleshooting |

Not sure which pack? The skill will suggest one based on your skill's content.

## Manual Contribution

If you prefer to create skills manually:

1. Read the standards: [SKILL_DESIGN_PRINCIPLES.md](SKILL_DESIGN_PRINCIPLES.md)
2. Create `<pack>/skills/<skill-name>/SKILL.md` following the template
3. Update `<pack>/CLAUDE.md` intent routing table
4. Validate Tier 1: `./scripts/run-skill-linter.sh <pack>/skills/<skill-name>/`
5. Validate Tier 2: `make validate-skill-design-changed`

Both tiers must pass before submitting a PR.

## Before You Submit

4. **Open the repository in Claude Code**
   - The `/agentic-contribution-skill` will be automatically available
   - Claude Code loads skills from `.claude/skills/` directory on startup
   - Verify it's available by typing `/agentic-contribution-skill` in the prompt

### Knowledge Requirements

- **Basic understanding** of AI skills and agents
- **Familiarity** with YAML frontmatter syntax
- **Knowledge** of the technology/platform your skill targets
- **Understanding** of Git workflow (fork, branch, commit, PR)

## Contribution Workflow

### Using agentic-contribution-skill (Recommended)

The agentic-contribution-skill guides you through 5 phases:

#### Phase 1: Discovery
Answer questions about your skill:
- What does it do?
- Who uses it?
- Which pack should it belong to?
- What MCP tools does it need?

#### Phase 2: Definition
Provide detailed specifications:
- Skill name (unique, kebab-case)
- Use case examples (concrete user phrases)
- Workflow steps with MCP tools
- Common issues users might face

#### Phase 3: Generation
agentic-contribution-skill creates:
- Complete `SKILL.md` with all mandatory sections
- Updated `CLAUDE.md` intent routing
- MCP configuration (if needed)
- New pack structure (if creating new pack)

#### Phase 4: Validation
Automated quality checks:
- **Tier 1**: agentskills.io specification compliance
- **Tier 2**: Repository design principles (DP1-11)
- Detailed feedback on any issues

#### Phase 5: Git Workflow
With your confirmation at each step:
- Create branch (`feat/skill-name`)
- Stage files
- Create commit with co-authorship
- Push to your fork
- Guide PR creation

### Manual Contribution (Advanced)

If you prefer manual creation:

1. **Read the standards**
   - [SKILL_DESIGN_PRINCIPLES.md](SKILL_DESIGN_PRINCIPLES.md) - Complete requirements
   - [agentskills.io specification](https://agentskills.io/specification) - Base standard

2. **Create skill structure**
   ```bash
   mkdir -p <pack>/skills/<skill-name>/
   # Create SKILL.md following SKILL_DESIGN_PRINCIPLES.md template
   ```

3. **Update pack CLAUDE.md**
   - Add entry to intent routing table

4. **Validate locally**
   ```bash
   # Tier 1 validation (agentskills.io)
   ./scripts/run-skill-linter.sh <pack>/skills/<skill-name>/
   
   # Tier 2 validation (design principles)
   make validate-skill-design-changed

   # Skill docs link validation (must use skill-local docs/... paths)
   uv run python scripts/validate_skill_doc_links.py <pack>/skills/<skill-name>/SKILL.md

   # Skill docs tree validation (skills docs markdown links)
   uv run python scripts/validate_docs_tree_links.py <pack>/skills/<skill-name>/SKILL.md
   
   # Both must pass before committing
   ```

5. **Create pull request**
   ```bash
   git checkout -b feat/<skill-name>
   git add <pack>/skills/<skill-name>/ <pack>/CLAUDE.md
   git commit -m "feat: add <skill-name> skill to <pack>"
   git push origin feat/<skill-name>
   # Create PR on GitHub from your fork to upstream
   ```

## Quality Standards

All skills must comply with **two tiers** of standards:

### Tier 1: agentskills.io Specification (Automated)

Base standard for skill structure and format:
- Valid YAML frontmatter with required fields
- Proper naming conventions (kebab-case)
- Section structure and ordering
- Parameter documentation

**Validation**: `./scripts/run-skill-linter.sh`

### Tier 2: Repository Design Principles (Automated)

Enhanced requirements specific to this repository:

| Principle | Requirement | Validated By |
|-----------|-------------|--------------|
| **DP1** | Document Consultation Transparency | Script checks for Read tool + declaration |
| **DP2** | Precise Parameter Specification | Validates parameter examples exist |
| **DP3** | Description Conciseness | Counts tokens, must be <500 |
| **DP4** | Dependencies Declaration | Checks Dependencies section presence |
| **DP5** | Human-in-the-Loop Requirements | Validates confirmation steps for critical ops |
| **DP6** | Mandatory Sections | Verifies all required sections present in order |
| **DP7** | MCP Server Verification | Checks for credential exposure |
| **DP11** | Pack-Level CLAUDE.md | Validates intent routing updated |

**Validation**: `make validate-skill-design-changed`

See [SKILL_DESIGN_PRINCIPLES.md](SKILL_DESIGN_PRINCIPLES.md) for complete details and rationale.

## What Makes a Good Skill?

### Clear Purpose
- **Do one thing well** - Single responsibility
- **Specific use case** - Not too broad
- **Real user need** - Solves actual problem

### Quality Documentation
- **Concrete examples** - Real user phrases, not generic descriptions
- **Precise parameters** - Exact formats with examples
- **Common issues** - At least 3 documented with solutions
- **Complete workflow** - All steps with error handling

### Production Ready
- **Error handling** - Covers failure scenarios
- **Security** - No credential exposure
- **Human-in-the-loop** - Confirmations for critical operations
- **Validated** - Passes Tier 1 + Tier 2 checks

## Pack Selection Guide

Choose the right pack for your skill:

| Pack | Persona | When to Use |
|------|---------|-------------|
| **rh-sre** | Site Reliability Engineers | CVE remediation, system compliance, RHEL automation |
| **rh-developer** | Application Developers | App deployment, S2I builds, Helm charts |
| **openshift-virtualization** | Virtualization Admins | VM lifecycle, snapshots, migrations |
| **ocp-admin** | OpenShift Administrators | Cluster management, health reports, monitoring |
| **rh-ai-engineer** | AI/ML Engineers | Model serving, vLLM, KServe, NVIDIA NIM |
| **rh-automation** | Automation Leads | Ansible AAP governance, safety checks |
| **rh-support-engineer** | Support Engineers | Technical support, troubleshooting |

**Creating a new pack?** Use agentic-contribution-skill - it will create the complete pack structure for you.

## Testing Your Skill Locally

Before submitting a PR, test your skill locally:

1. **Invoke the skill** in Claude Code:
   ```
   /your-skill-name
   ```

2. **Try different scenarios**:
   - Normal use case (happy path)
   - Edge cases
   - Error conditions

3. **Verify the output**:
   - Check that MCP tools are called correctly
   - Ensure error messages are helpful
   - Confirm human-in-the-loop prompts appear for critical operations

4. **Test with real data** (if applicable):
   - Use actual VMs, clusters, or systems (in a safe environment)
   - Don't test destructive operations on production systems

## Pull Request Process

### Before Submitting

- [ ] Skill created with agentic-contribution-skill or manually validated
- [ ] Tier 1 validation passed: `./scripts/run-skill-linter.sh`
- [ ] Tier 2 validation passed: `make validate-skill-design-changed`
- [ ] Skill docs links validation passed: `uv run python scripts/validate_skill_doc_links.py <pack>/skills/<skill-name>/SKILL.md`
- [ ] Skill docs tree links validation passed: `uv run python scripts/validate_docs_tree_links.py <pack>/skills/<skill-name>/SKILL.md`
- [ ] Tested skill locally by invoking it in Claude Code
- [ ] No credentials hardcoded (use `${ENV_VAR}` format)
- [ ] Human-in-the-loop confirmation for destructive operations

## Resources

- [SKILL_DESIGN_PRINCIPLES.md](SKILL_DESIGN_PRINCIPLES.md) -- Design principles and templates
- [Federation Review Guide](docs/FEDERATION_REVIEW_GUIDE.md) -- How external packs are evaluated for federation
- [agentskills.io specification](https://agentskills.io/specification) -- Base skill standard
- [Documentation site](https://rhecosystemappeng.github.io/agentic-collections) -- Browse all collections
- [GitHub Issues](https://github.com/RHEcosystemAppEng/agentic-collections/issues) -- Report bugs or ask questions

## License

By contributing, you agree your contributions are licensed under [Apache License 2.0](LICENSE).
