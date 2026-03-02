# Lenny Stress Test Plugin

Test your PRD assumptions against real insights from [Lenny Rachitsky's podcast](https://www.lennyspodcast.com/) guests. This Claude Code plugin helps product managers validate their thinking by surfacing relevant experiences from 500+ podcast episodes.

## What It Does

The `stress-test` skill analyzes specific sections of your PRD and:
1. Extracts implicit assumptions you're making
2. Queries the Lenny Lens corpus for relevant guest experiences
3. Validates or challenges those assumptions with real-world evidence
4. Surfaces the hardest question you need to answer before your next stakeholder review

## Prerequisites

- **Claude Code** (CLI) or **Claude Desktop** (app)
- No API key needed - uses a shared public key for Lenny Lens API

## Installation

### For Claude Code (CLI)

```bash
claude plugins install https://github.com/rachitha15/lenny-stress-test
```

### For Claude Desktop (App)

Add to your Claude Desktop configuration file:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`

```json
{
  "plugins": [
    {
      "source": "github:rachitha15/lenny-stress-test"
    }
  ]
}
```

After adding, restart Claude Desktop.

## Quick Start

Once installed, use the `/stress-test` skill in your conversation:

```
/stress-test GTM section

# Or more naturally:
"Test assumptions in my GTM strategy"
"What would Lenny's guests say about my pricing approach?"
"Challenge my thinking on MVP scope"
```

## Supported PRD Sections

The skill can analyze these sections:
- **GTM** (Go-to-Market strategy)
- **Metrics** (Success criteria, North Star metrics)
- **Pricing** (Pricing strategy, tier structure)
- **MVP Scope** (What to build first)
- **Problem Statement** (Problem definition)
- **Activation** (User onboarding, aha moments)
- **Retention** (Engagement, churn prevention)
- **Stakeholder Alignment** (Internal buy-in strategy)

## Example Workflow

1. **Share your PRD**: Paste a section, attach a document, or reference content from earlier in the conversation
2. **Invoke the skill**: `/stress-test [section name]`
3. **Review findings**: Get 3 assumption stress tests with guest insights
4. **Act on it**: Address the "hardest question" before your next review

### Sample Input

```
I'm working on a PLG motion for our payment analytics product. Here's my GTM section:

[Your GTM strategy...]

/stress-test GTM
```

### Sample Output

```
Assumption stress test: GTM

Assumption 1: Bottom-up adoption will happen organically if we nail the product experience
What Lenny's guests experienced: Elena Verna (Amplitude) found that PLG requires
dedicated growth engineering—virality loops don't happen by accident. Episode: "How
to build a PLG motion that works"
Verdict: Challenges

Assumption 2: Finance will approve tool spend if individual contributors love it
What Lenny's guests experienced: [...]
Verdict: Validates

[...]

The hardest question this surfaces:
Who owns the budget line for analytics tools at your target companies, and have you
validated that individual users can expense $99/month without procurement?
```

## How It Works

The plugin uses:
- **Lenny Lens API** - Semantic search across 500+ podcast episodes
- **Claude's reasoning** - To extract assumptions and synthesize insights
- **MCP (Model Context Protocol)** - To integrate the API with Claude

The skill extracts implicit assumptions from your PRD, formulates precise retrieval queries, and surfaces relevant guest experiences with confidence scores.

## API Key

The plugin uses a shared public API key (`engage2025`) for the Lenny Lens API. This is pre-configured in the plugin—no setup needed.

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/rachitha15/lenny-stress-test/issues) on GitHub.

## License

To be determined.

## About

Created by [Rachitha Suresh](https://github.com/rachitha15) to help PMs stress test their assumptions with real-world insights.

---

**Note:** The Lenny Lens corpus is primarily US/SaaS/B2C focused. Context translation may be needed for India-specific or B2B use cases.
