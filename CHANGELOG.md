# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-11-14

### Added
- 7 agents: Orchestrator, Researcher, Domain Expert, Critical Thinking, Fact-Checker, Debater, Final Decision
- 9 skills: web-research, academic-search, evidence-extraction, source-credibility, argument-graph, bias-and-framing, counterfactual-analysis, deliberation-protocol, consensus-and-report
- 4 rules: no-unverified-claims, citation-discipline, conflict-resolution, independent-first
- 1 command: run-task
- MIT LICENSE (Copyright 2026 Vkyrie)
- 3 pipeline examples: Great Wall visibility, small shop online decision, Python vs JavaScript for beginners
- Independent-first debate with Best-Point Scoring 0-8, Anti-Sycophancy Guard, Devil's Advocate, 2-round cap
- consensus-and-report skill
- Mirror structure: .claude/agents/, .claude/skills/, .claude/commands/, .claude/rules/ mirrored from top-level folders
- .claude-plugin/plugin.json with Vkyrie repository
- README.md with pipeline documentation and examples index
- CLAUDE.md for project context
- docs/pipeline.md with execution rules and contracts
- .gitignore with standard patterns

### Fixed
- plugin.json repository URL and LICENSE copyright to Vkyrie
- deliberation-protocol and run-task mirrors to match source files
- Examples: NASA 404 link removed from Example 1; Example 3 confidence corrected to MODERATE
- Agent/skill/rule counts corrected in docs (3 rules → 4 rules)
- Stage 1 scope updated from "structure only" to "complete — agents and skills defined"