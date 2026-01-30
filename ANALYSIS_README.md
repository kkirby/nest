# NestJS Codebase Analysis

This directory contains a comprehensive analysis of the NestJS codebase, quantifying how much of the code is related to:

- **DI/Container/Module-scanning** (Category A)
- **Transport/Controllers/Routing/Adapters** (Category B)  
- **Shared/Other** (Category C)

## Analysis Results

See [`CODEBASE_ANALYSIS.md`](./CODEBASE_ANALYSIS.md) for the complete analysis report with:

- Executive summary with LOC and percentages
- Detailed methodology
- Package-by-package breakdown
- Top 30 DI-heavy and Transport-heavy files
- Sanity checks and limitations

## Quick Summary

Based on analysis of **30,916 lines** of TypeScript source code across 596 files:

| Category | LOC | Percentage |
|----------|-----|------------|
| **DI/Container/Module** | 3,637 | **11.8%** |
| **Transport/Controllers/Routing** | 4,484 | **14.5%** |
| **Shared/Other** | 22,794 | **73.7%** |

**Confidence Score:** 0.98 / 1.0

## Running the Analysis

The analysis script is fully self-contained and reproducible:

```bash
# Run with default repository path
python3 analyze_codebase.py

# Or specify a custom path
python3 analyze_codebase.py /path/to/nest/repo
```

The script will:
1. Discover all packages in the monorepo
2. Analyze TypeScript source files (excluding tests and generated files)
3. Classify each file using multiple signals:
   - Package path patterns (40% weight)
   - Keyword frequency analysis (40% weight)
   - Import graph analysis (20% weight)
4. Generate a comprehensive Markdown report

## Methodology

The analysis uses a multi-signal classification approach:

1. **Package Priors**: Files in certain directories (e.g., `packages/core/injector/`) get DI priors
2. **Keyword Scoring**: Counts occurrences of category-specific keywords (34 DI keywords, 38 Transport keywords)
3. **Import Analysis**: Examines what modules each file imports from

Files with a dominant category (≥60% score) are fully allocated to that category. Files without a clear dominant category have their LOC split proportionally.

## Key Findings

- **Core package** contains the most DI code (25% of its LOC) and Transport code (17%)
- **Common package** is 94% shared utilities and decorators
- **Microservices package** is primarily shared infrastructure (87%)
- Only **11 files** (4% of LOC) have high ambiguity (no category >45%)

See the full report for detailed breakdowns and top files in each category.
