This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.


# Jumpstart Data Quality Platform — Claude Code Build Prompt

## ROLE & MISSION

You are a senior full-stack engineer, data quality specialist, and UX architect. Your task is to build **Jumpstart** — a production-grade, AI-powered Data Quality & Comparison Platform that runs fully locally. This is not a prototype. Every component must be production-ready, type-safe, performant, and maintainable.

Study this entire prompt before writing a single line of code. Plan the architecture first, then build bottom-up: types → utilities → store → components → pages.

---

## TECH STACK (STRICT)

| Layer | Technology |
|---|---|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript 5 (strict mode) |
| Styling | Tailwind CSS + shadcn/ui |
| Table | TanStack Table v8 |
| Charts | Recharts |
| Animations | Framer Motion |
| State | Zustand |
| File parsing | PapaParse (CSV) + XLSX (Excel) |
| File upload | React Dropzone |
| Icons | Lucide React |
| AI | Anthropic SDK (`@anthropic-ai/sdk`) |
| Utilities | lodash, fuse.js, date-fns |
| Dev | ESLint, Prettier, TypeScript strict |

---

## PROJECT FOLDER STRUCTURE

```
jumpstart/
├── app/
│   ├── layout.tsx                    # Root layout, ThemeProvider, fonts
│   ├── page.tsx                      # Redirects to /workspace
│   └── workspace/
│       └── page.tsx                  # Main single-page workspace shell
│
├── components/
│   ├── layout/
│   │   ├── Sidebar.tsx               # Collapsible nav sidebar
│   │   ├── TopBar.tsx                # Breadcrumb, actions, theme toggle
│   │   └── WorkspaceShell.tsx        # Main layout wrapper
│   │
│   ├── upload/
│   │   ├── DropZone.tsx              # React Dropzone with drag-and-drop
│   │   ├── FileCard.tsx              # Loaded file summary card
│   │   ├── SheetSelector.tsx         # Excel multi-sheet tab selector
│   │   └── DataPreviewTable.tsx      # Quick preview of uploaded data
│   │
│   ├── quality/
│   │   ├── QualityScoreCard.tsx      # Animated score ring + breakdown
│   │   ├── IssueCard.tsx             # Expandable issue with affected rows
│   │   ├── IssueFilters.tsx          # Filter bar (type, severity, column)
│   │   ├── AutoCleanToolbar.tsx      # One-click fix action buttons
│   │   ├── CleanActionLog.tsx        # Timestamped action history
│   │   ├── CompletenessBar.tsx       # Per-column completeness bar
│   │   └── MergeGroupCard.tsx        # Duplicate group with merge UI
│   │
│   ├── compare/
│   │   ├── SheetSelector.tsx         # A/B sheet pickers
│   │   ├── ColumnMatchConfig.tsx     # Match column selector + toggles
│   │   ├── ThresholdSlider.tsx       # Fuzzy match threshold control
│   │   ├── CompareResultsSummary.tsx # KPI cards for match results
│   │   ├── MatchedRecordsTable.tsx   # Exact + fuzzy match list
│   │   ├── UnmatchedTable.tsx        # Only-A / Only-B tables
│   │   └── SideBySideView.tsx        # Color-coded side-by-side diff
│   │
│   ├── table/
│   │   ├── DataTable.tsx             # TanStack Table with full features
│   │   ├── ColumnHeader.tsx          # Sort, filter, type icon header
│   │   ├── CellRenderer.tsx          # Type-aware cell rendering
│   │   ├── IssueIndicator.tsx        # Inline issue dot/tooltip
│   │   ├── TableToolbar.tsx          # Search, filter, export, column toggle
│   │   └── BulkActionBar.tsx         # Bulk delete/clean/export actions
│   │
│   ├── dashboard/
│   │   ├── KPIGrid.tsx               # Animated KPI cards grid
│   │   ├── QualityBySheetChart.tsx   # Bar chart per sheet
│   │   ├── IssueTypePieChart.tsx     # Pie breakdown by type
│   │   ├── CompletenessHeatmap.tsx   # Column x Sheet heatmap table
│   │   ├── TrendAreaChart.tsx        # Issue trend over cleaning sessions
│   │   └── InsightPanel.tsx          # AI-generated text insights
│   │
│   ├── assistant/
│   │   ├── AssistantPanel.tsx        # Main chat container
│   │   ├── MessageBubble.tsx         # User/AI message rendering
│   │   ├── SuggestedPrompts.tsx      # Quick-start prompt chips
│   │   └── ContextBadge.tsx          # Shows data context loaded
│   │
│   ├── normalize/
│   │   ├── NormalizationRules.tsx    # Rule builder UI
│   │   ├── RuleCard.tsx              # Single normalization rule
│   │   └── NormalizationPreview.tsx  # Before/after preview
│   │
│   └── shared/
│       ├── Tag.tsx                   # Colored badge/tag
│       ├── EmptyState.tsx            # Illustrated empty states
│       ├── ConfirmDialog.tsx         # Confirmation modal
│       ├── ExportMenu.tsx            # CSV/Excel/JSON export dropdown
│       └── ThemeToggle.tsx           # Sun/Moon toggle button
│
├── lib/
│   ├── types/
│   │   ├── dataset.ts                # Dataset, Column, Row, Sheet types
│   │   ├── quality.ts                # Issue, Severity, IssueType types
│   │   ├── comparison.ts             # CompareResult, MatchPair types
│   │   ├── normalization.ts          # Rule, RuleType, RuleAction types
│   │   └── ai.ts                     # Message, AssistantContext types
│   │
│   ├── engine/
│   │   ├── typeInference.ts          # Column type detection
│   │   ├── qualityAnalyzer.ts        # Full quality analysis engine
│   │   ├── comparisonEngine.ts       # Exact + fuzzy sheet comparison
│   │   ├── normalizationEngine.ts    # Apply normalization rules
│   │   ├── cleaningEngine.ts         # Auto-clean actions
│   │   ├── fuzzyMatcher.ts           # Levenshtein + Fuse.js matching
│   │   └── scoringEngine.ts          # Quality score calculation
│   │
│   ├── parsers/
│   │   ├── csvParser.ts              # PapaParse wrapper
│   │   ├── excelParser.ts            # XLSX multi-sheet parser
│   │   ├── jsonParser.ts             # JSON array/object parser
│   │   └── schemaDetector.ts         # Auto-detect schema from data
│   │
│   ├── exporters/
│   │   ├── csvExporter.ts            # Export to CSV
│   │   ├── excelExporter.ts          # Export to XLSX with formatting
│   │   └── jsonExporter.ts           # Export to JSON
│   │
│   ├── ai/
│   │   ├── client.ts                 # Anthropic SDK client setup
│   │   ├── contextBuilder.ts         # Build data context for AI
│   │   └── prompts.ts                # System prompt templates
│   │
│   └── utils/
│       ├── formatting.ts             # formatPhone, formatCurrency, etc.
│       ├── validators.ts             # isEmail, isPhone, isDate, etc.
│       ├── strings.ts                # levenshtein, similarity, properCase
│       └── statistics.ts             # mean, stdDev, outlierDetection
│
├── store/
│   ├── datasetStore.ts               # Loaded sheets, active sheet
│   ├── qualityStore.ts               # Issues, resolved, clean log
│   ├── compareStore.ts               # Compare config + results
│   ├── uiStore.ts                    # View, theme, sidebar, modals
│   └── assistantStore.ts             # Chat messages, loading state
│
├── hooks/
│   ├── useDataset.ts                 # Dataset CRUD operations
│   ├── useQualityAnalysis.ts         # Run + memoize quality analysis
│   ├── useComparison.ts              # Run + memoize sheet comparison
│   ├── useAutoClean.ts               # Apply cleaning + track changes
│   ├── useExport.ts                  # Multi-format export logic
│   └── useAssistant.ts               # AI chat with streaming
│
├── config/
│   ├── navigation.ts                 # Nav items, icons, routes
│   ├── qualityRules.ts               # Default quality check configs
│   └── theme.ts                      # Color tokens, theme definition
│
└── public/
    └── (static assets)
```

---

## CORE FEATURES — DETAILED SPECIFICATIONS

### 1. FILE UPLOAD & PARSING

**Supported formats:** CSV, Excel (XLSX, XLS), JSON

**DropZone behavior:**
- Full-page drop target on Upload view
- Accepts multiple files simultaneously
- Shows upload progress per file
- Parses in a Web Worker to avoid UI blocking
- For Excel: auto-detects all sheets, shows sheet tab selector
- For CSV: auto-detects delimiter (comma, tab, semicolon, pipe)
- Displays parse errors inline without crashing
- Stores all loaded sheets in Zustand with unique IDs

**Post-parse actions:**
- Auto-run schema detection on every loaded sheet
- Auto-run quality analysis (debounced, memoized)
- Show parsed row/column counts with column type badges
- Allow renaming sheets inline

**SheetSelector component:**
- Horizontal tab bar for Excel files with multiple sheets
- Each tab shows: sheet name, row count, quality score badge
- Click to preview, double-click to rename

---

### 2. SCHEMA DETECTION ENGINE (`lib/engine/typeInference.ts`)

Infer column types from both **column name patterns** and **value content analysis**.

**Supported types:**
```typescript
type ColumnType =
  | 'id'          // Matches: ^id$, _id, uuid — unique, short, alphanumeric
  | 'email'       // Matches: /email/ in name OR valid email regex in values
  | 'phone'       // Matches: /phone|tel|mobile/ in name OR phone patterns
  | 'date'        // Matches: /date|time|_at$/ in name OR parseable dates
  | 'currency'    // Matches: /amount|price|cost|revenue/ in name OR $-prefixed
  | 'number'      // All values parseable as float
  | 'percentage'  // Values 0-100 with % or /pct|percent/ in name
  | 'url'         // Matches: /url|link|website/ OR http(s):// values
  | 'boolean'     // Values: true/false, yes/no, 1/0
  | 'category'    // Low-cardinality string (uniqueCount <= 10% of rows)
  | 'firstName'   // Matches: /first.?name/
  | 'lastName'    // Matches: /last.?name/
  | 'fullName'    // Matches: /^name$|full.?name/
  | 'organization'// Matches: /org|company|business|account/
  | 'address'     // Matches: /address|street|addr/
  | 'city'        // Matches: /^city$/
  | 'state'       // Matches: /^state$|province/
  | 'country'     // Matches: /country|nation/
  | 'zip'         // Matches: /zip|postal/
  | 'text'        // Default fallback
```

**Detection algorithm:**
1. Check name pattern first (highest confidence)
2. Sample up to 50 non-null values, run regex checks
3. Score each possible type, return highest confidence match
4. Return `{ type, confidence: 0-1, isNullable: boolean, uniqueRatio: number }`

**Primary key detection:**
- Mark a column as `isPrimaryKey` if: uniqueRatio === 1.0 AND (type === 'id' OR name matches /^id$/i OR name is the first column with all unique values)

---

### 3. DATA QUALITY ENGINE (`lib/engine/qualityAnalyzer.ts`)

Run a full analysis pass on every loaded sheet. Return a structured `QualityReport`.

```typescript
interface QualityReport {
  sheetId: string;
  score: number;          // 0-100, weighted by severity
  completeness: number;   // 0-1, avg across all columns
  issues: QualityIssue[];
  columnStats: ColumnStats[];
  rowCount: number;
  columnCount: number;
  analysisTimestamp: Date;
}

interface QualityIssue {
  id: string;
  type: IssueType;
  severity: 'critical' | 'high' | 'medium' | 'low' | 'info';
  column: string;
  title: string;
  description: string;
  affectedRowIndices: number[];
  count: number;
  confidence: number;      // 0-1
  suggestedFix?: string;
  autoFixAvailable: boolean;
  groups?: DuplicateGroup[];  // For duplicate issues
}

type IssueType =
  | 'missing_values'
  | 'invalid_email'
  | 'invalid_phone'
  | 'inconsistent_phone_format'
  | 'extra_whitespace'
  | 'improper_casing'
  | 'exact_duplicate'
  | 'fuzzy_duplicate'
  | 'numeric_outlier'
  | 'invalid_date'
  | 'mixed_types'
  | 'invalid_url'
  | 'suspicious_value'
  | 'encoding_issue'
```

**Checks to implement (in order):**

1. **Missing values** — per column, calc completeness, severity by % missing
2. **Invalid emails** — EMAIL_REGEX test, flag malformed entries
3. **Inconsistent phone formats** — detect >1 format pattern, flag all rows
4. **Invalid phone numbers** — normPhone().length not in [7,10,11]
5. **Extra whitespace** — leading/trailing spaces OR double spaces
6. **Improper casing** — all-lowercase or all-uppercase proper names/orgs
7. **Exact duplicates** — group by normalized email OR primary key, find groups > 1
8. **Fuzzy duplicates** — Levenshtein similarity >= 0.82 on name columns
9. **Numeric outliers** — values > 2.5σ from mean in numeric columns
10. **Invalid dates** — values that fail Date.parse() in date columns
11. **Mixed types** — column has both numeric and string values
12. **Invalid URLs** — URL columns with values not matching URL pattern
13. **Encoding issues** — values containing replacement chars (â€, Ã, etc.)

**Quality score formula:**
```
base = 100
deduct per issue:
  critical: -15 per affected row (capped at -40)
  high:     -8  per affected row (capped at -25)
  medium:   -3  per affected row (capped at -15)
  low:      -1  per affected row (capped at -5)
score = max(0, min(100, base - totalDeductions / totalCells * 100))
```

---

### 4. AUTO-CLEAN ENGINE (`lib/engine/cleaningEngine.ts`)

All clean operations are **non-destructive** — original data is preserved in Zustand, cleaned versions replace it in a new snapshot.

```typescript
interface CleanOperation {
  id: string;
  type: CleanOperationType;
  timestamp: Date;
  cellsAffected: number;
  rowsAffected: number;
  columnsAffected: string[];
  undoSnapshot: Row[];  // Previous state for undo
}

type CleanOperationType =
  | 'trim_whitespace'       // String.trim() + collapse inner double-spaces
  | 'standardize_phones'    // Normalize to (XXX) XXX-XXXX
  | 'fix_casing'            // properCase() on name/org columns
  | 'clean_emails'          // trim + lowercase emails
  | 'remove_duplicates'     // Keep first, remove subsequent in group
  | 'fill_missing'          // Fill with mode/median/custom value
  | 'standardize_dates'     // Parse + reformat to ISO YYYY-MM-DD
  | 'strip_special_chars'   // Remove non-printable/encoding-broken chars
  | 'normalize_booleans'    // Convert yes/no/1/0 to true/false
```

**Undo/Redo support:**
- Maintain a `cleanHistory: CleanOperation[]` stack in `qualityStore`
- Each operation stores a snapshot of the rows it modified
- Provide `undoLastClean()` and `undoAll()` in store
- Show operations in a timestamped `CleanActionLog` with undo buttons

---

### 5. NORMALIZATION ENGINE (`lib/engine/normalizationEngine.ts`)

Users can define and save **normalization rules** — reusable, ordered transformations.

```typescript
interface NormalizationRule {
  id: string;
  name: string;
  description: string;
  isActive: boolean;
  column: string | '__all__';  // Target specific column or all text
  type: NormalizationRuleType;
  config: Record<string, unknown>;
  order: number;
}

type NormalizationRuleType =
  | 'find_replace'       // Config: { find: string, replace: string, regex: boolean }
  | 'prefix_strip'       // Config: { prefix: string }
  | 'suffix_strip'       // Config: { suffix: string }
  | 'format_phone'       // Config: { targetFormat: string }
  | 'format_date'        // Config: { inputFormat: string, outputFormat: string }
  | 'uppercase'
  | 'lowercase'
  | 'proper_case'
  | 'truncate'           // Config: { maxLength: number }
  | 'pad_left'           // Config: { length: number, char: string }
  | 'map_values'         // Config: { mapping: Record<string, string> }
  | 'extract_regex'      // Config: { pattern: string, group: number }
  | 'custom_js'          // Config: { expression: string } — sandboxed eval
```

**Rule builder UI (`normalize/NormalizationRules.tsx`):**
- Drag-and-drop rule ordering (Framer Motion)
- Live preview: shows before/after for first 5 affected rows
- Save named rule sets as presets
- Import/export rules as JSON
- "Apply to Sheet" and "Apply to All Sheets" buttons

---

### 6. COMPARISON ENGINE (`lib/engine/comparisonEngine.ts`)

Compare two sheets and categorize every record.

```typescript
interface CompareConfig {
  sheetAId: string;
  sheetBId: string;
  matchColumns: string[];
  fuzzyThreshold: number;      // 0.5–1.0, default 0.82
  matchMode: 'any' | 'all';    // Match on ANY vs ALL selected columns
  ignoreCase: boolean;
  ignoreWhitespace: boolean;
  normalizePhones: boolean;    // Strip non-digits before comparing
}

interface CompareResult {
  config: CompareConfig;
  exactMatches: MatchPair[];
  fuzzyMatches: FuzzyMatchPair[];
  onlyInA: number[];           // Row indices in Sheet A
  onlyInB: number[];           // Row indices in Sheet B
  duplicatesInB: DuplicateGroup[];
  duplicatesInA: DuplicateGroup[];
  stats: CompareStats;
  executionMs: number;
}

interface FuzzyMatchPair {
  indexA: number;
  indexB: number;
  similarity: number;          // 0-1 overall
  columnSimilarities: Record<string, number>;  // Per-column breakdown
  matchReason: string;         // Human-readable explanation
}
```

**Algorithm:**
1. Build normalized key map for Sheet A
2. Pass 1 — exact matching: normalize all match columns, find identical keys
3. Pass 2 — fuzzy matching on unmatched rows: compute per-column Levenshtein similarity, take weighted average, apply threshold
4. Categorize remaining unmatched rows as onlyA / onlyB
5. Run within-sheet duplicate detection on both sheets independently

**Comparison views:**
- **Summary**: bar chart of all 5 categories + match rate percentage
- **Matches**: side-by-side table, exact vs fuzzy badge, column similarity breakdown on expand
- **Only in A / Only in B**: filterable table with export button
- **Side-by-side diff**: color-coded rows — green=exact, purple=fuzzy, amber=onlyA, cyan=onlyB, rose=duplicate
- **Conflict view**: when fuzzy matches differ significantly in specific fields, highlight those cell-level differences in amber

---

### 7. DATA TABLE (`components/table/DataTable.tsx`)

Built on **TanStack Table v8** with virtualization for large datasets.

**Features:**
- Column sorting (click header, multi-sort with Shift+click)
- Column-level search filters (popover per column)
- Global search across all visible columns
- Column show/hide toggle (popover menu)
- Column reordering (drag handles)
- Row selection (checkbox column, select all)
- Pagination OR virtual scroll (auto-switch at 500 rows)
- Sticky header + sticky first column
- Row height options: compact / default / comfortable
- Cell-level issue highlighting:
  - `critical`: red left border + red background tint
  - `high`: orange left border + orange tint
  - `medium`: amber left border + amber tint
  - `low`: subtle blue tint, no border
- Per-cell tooltip on hover showing issue details
- Inline cell editing (double-click to edit, Escape to cancel, Enter to save)
- Type-aware cell renderers:
  - `email`: clickable mailto link + validity icon
  - `phone`: formatted display + validity icon
  - `date`: formatted with date-fns
  - `currency`: right-aligned with $ formatting
  - `boolean`: toggle chip
  - `category`: colored Tag component
  - `url`: clickable external link with truncation
  - empty: styled "— empty —" placeholder in muted red
- **Issues-only mode**: toggle to show only rows with at least one issue
- **Bulk actions bar** (appears when rows selected):
  - Delete selected rows
  - Export selected rows (CSV/Excel/JSON)
  - Apply clean to selected rows only
  - Mark as reviewed

---

### 8. ANALYTICS DASHBOARD (`components/dashboard/`)

Auto-generated from loaded sheets. Updates reactively as data changes.

**KPI Grid (top row):**
- Total Records (across all sheets)
- Average Quality Score (animated ring, color by score)
- Total Issues (open vs resolved counts)
- Duplicate Groups
- Data Completeness %
- Sheets Loaded

**Charts:**
- **Quality by Sheet** — horizontal bar chart, bars colored by score (green/amber/red), sortable
- **Issues by Type** — donut chart with legend, click to filter issue panel
- **Completeness Heatmap** — table grid: columns × sheets, color-coded cells (green=100%, amber=80-99%, red=<80%)
- **Severity Distribution** — stacked bar: critical/high/medium/low per sheet
- **Top Problem Columns** — ranked list of columns with most issues
- **Cleaning Progress** (if clean history exists) — area chart showing issue count over cleaning sessions

**Insight Panel (`components/dashboard/InsightPanel.tsx`):**
- 3–5 AI-generated text observations about the loaded data
- Refreshes when data changes
- Loading skeleton during generation
- Each insight has a "→ Go fix" button that deep-links to the relevant view

---

### 9. AI ASSISTANT (`components/assistant/`)

Full-featured chat panel with streaming responses and data-awareness.

**Context sent to AI per message:**
```typescript
interface AssistantContext {
  sheets: {
    name: string;
    rowCount: number;
    columns: { name: string; type: string; completeness: number }[];
    qualityScore: number;
    topIssues: { title: string; severity: string; count: number }[];
    sampleRows: Row[];  // First 8 rows
  }[];
  activeView: string;
  lastCompareResult?: CompareResultSummary;
  recentCleanActions?: string[];
}
```

**System prompt includes:**
- Role as "Jumpstart AI Data Quality Analyst"
- Full context of all loaded sheets
- Instruction to be specific, actionable, and brief
- Instruction to reference actual column names and values

**Suggested prompts:**
- "What are the most critical issues I should fix first?"
- "Explain the fuzzy duplicate groups found"
- "Recommend a normalization strategy for the phone numbers"
- "Which columns have the most data quality problems?"
- "Summarize what's different between Sheet A and Sheet B"
- "Write a data cleaning checklist for this dataset"
- "What's the overall data health status?"
- "Suggest validation rules I should apply before importing"

**AI Actions (buttons AI can suggest the user click):**
- When AI says "you should trim whitespace" → render a "→ Apply Trim" button
- When AI says "remove duplicates" → render a "→ Go to Duplicates" button
- Parse AI response for action keywords and render inline CTAs

---

### 10. VALIDATION WORKFLOW ENGINE

Beyond detecting issues, allow users to define **validation rules** that flag rows as invalid.

```typescript
interface ValidationRule {
  id: string;
  name: string;
  column: string;
  condition: ValidationCondition;
  severity: 'critical' | 'high' | 'medium' | 'low';
  message: string;       // Error message shown on failure
  isActive: boolean;
}

type ValidationCondition =
  | { type: 'required' }
  | { type: 'regex'; pattern: string }
  | { type: 'min_length'; value: number }
  | { type: 'max_length'; value: number }
  | { type: 'numeric_range'; min?: number; max?: number }
  | { type: 'in_list'; values: string[] }
  | { type: 'not_in_list'; values: string[] }
  | { type: 'unique' }
  | { type: 'email_format' }
  | { type: 'phone_format' }
  | { type: 'date_range'; after?: string; before?: string }
  | { type: 'cross_column'; otherColumn: string; operator: 'equals'|'greater'|'less' }
  | { type: 'custom_js'; expression: string }
```

**Validation Rule Builder UI:**
- Visual form builder (no code required for standard rules)
- Live preview showing matching/failing rows
- Rule templates: "Email must be valid", "Required field", "ID must be unique", etc.
- Export/import rule sets as JSON presets
- "Validate All" button runs all active rules and adds results to the issues panel

---

### 11. DATA PROFILING PANEL

Per-column statistical summary, accessible by clicking any column header → "Profile Column".

**Numeric columns:**
- Min, Max, Mean, Median, Standard Deviation
- 25th / 75th percentile
- Histogram (Recharts BarChart, 10 bins)
- Outlier count (values > 2σ)
- Null count and percentage

**String/Category columns:**
- Unique value count + uniqueness ratio
- Top 10 most frequent values (bar chart)
- Average/min/max string length
- Null count
- Empty string count (vs null)
- Sample values

**Date columns:**
- Earliest / Latest date
- Range in days
- Distribution by month (bar chart)
- Invalid/unparseable count

---

### 12. IMPORT/EXPORT MANAGEMENT

**Export options (available everywhere via `ExportMenu` component):**
- CSV (PapaParse unparse)
- Excel XLSX (XLSX library with column width auto-fit, header styling)
- JSON (pretty-printed array)
- Export scope: full sheet / filtered rows / selected rows / issues report

**Export targets:**
- Full cleaned dataset
- Issues report (sheet with all quality issues)
- Comparison results (matched / unmatched / duplicates as separate tabs in Excel)
- Validation failures report

**Session persistence:**
- Auto-save to `localStorage` (compressed with `lz-string`) every 30s
- On load, offer to restore previous session
- Named workspace save/load (up to 10 saved workspaces)
- Export full workspace as JSON bundle (data + settings + history)

---

## STATE MANAGEMENT (ZUSTAND STORES)

### `datasetStore.ts`
```typescript
interface DatasetStore {
  sheets: Sheet[];
  activeSheetId: string | null;
  addSheets: (sheets: Sheet[]) => void;
  removeSheet: (id: string) => void;
  updateSheetRows: (id: string, rows: Row[]) => void;
  renameSheet: (id: string, name: string) => void;
  clearAll: () => void;
  getActiveSheet: () => Sheet | null;
}
```

### `qualityStore.ts`
```typescript
interface QualityStore {
  reports: Record<string, QualityReport>;  // sheetId → report
  resolvedIssueIds: Set<string>;
  cleanHistory: CleanOperation[];
  activeFilters: IssueFilters;
  setReport: (sheetId: string, report: QualityReport) => void;
  resolveIssue: (issueId: string) => void;
  pushCleanOperation: (op: CleanOperation) => void;
  undoLastClean: () => void;
  setFilters: (filters: Partial<IssueFilters>) => void;
}
```

### `compareStore.ts`
```typescript
interface CompareStore {
  config: CompareConfig | null;
  result: CompareResult | null;
  isRunning: boolean;
  setConfig: (config: Partial<CompareConfig>) => void;
  runComparison: () => Promise<void>;
  clearResult: () => void;
}
```

### `uiStore.ts`
```typescript
interface UIStore {
  activeView: ViewId;  // 'upload'|'quality'|'compare'|'dashboard'|'table'|'normalize'|'validate'|'assistant'
  theme: 'dark' | 'light' | 'system';
  sidebarCollapsed: boolean;
  activeQualitySheetId: string | null;
  activeTableSheetId: string | null;
  setView: (view: ViewId) => void;
  toggleTheme: () => void;
  toggleSidebar: () => void;
}
```

---

## UI/UX DESIGN SYSTEM

### Color Tokens (Tailwind + CSS variables)
```css
/* Dark mode (default) */
--color-bg:          #0B1120;
--color-bg-2:        #0F172A;
--color-card:        #131C31;
--color-card-hover:  #1A2744;
--color-border:      #1E2D4A;
--color-border-hover:#2A3F66;
--color-sidebar:     #0D1529;
--color-text:        #F1F5F9;
--color-text-muted:  #94A3B8;
--color-text-subtle: #64748B;

/* Accent — teal/cyan */
--color-accent:      #14B8A6;
--color-accent-light:#2DD4BF;
--color-accent-dark: #0D9488;

/* Light mode overrides */
--color-bg:          #EEF3FA;
--color-bg-2:        #F8FAFD;
--color-card:        #FFFFFF;
--color-sidebar:     #FFFFFF;
--color-border:      #D0DCF0;
--color-text:        #1A2744;
--color-text-muted:  #4E6A90;
```

### shadcn/ui Components to use:
- `Button`, `Badge`, `Card`, `Separator`, `Tooltip`, `Popover`
- `Dialog`, `AlertDialog`, `Sheet` (slide-over panel)
- `DropdownMenu`, `Select`, `Checkbox`, `Switch`, `Slider`
- `Tabs`, `ScrollArea`, `Skeleton`, `Progress`
- `Input`, `Textarea`, `Label`
- `Table` (base, override with TanStack)
- `Toast` / `Sonner` for notifications

### Framer Motion usage:
- Page transitions between views (opacity + y slide)
- Issue card expand/collapse (AnimatePresence + height animation)
- KPI numbers count-up on load
- Sidebar collapse animation
- Toast slide-in notifications
- Chart bar/segment entrance animations (staggered)
- Drag-and-drop reorder (normalization rules, column order)

### Typography:
- Font: `Inter` (body) + `JetBrains Mono` (code, numbers, IDs)
- Scale: 12px (xs), 13px (sm), 14px (base), 16px (lg), 20px (xl), 24px (2xl)

---

## PERFORMANCE REQUIREMENTS

- **Parse large files**: Use Web Workers for parsing > 5MB files
- **Quality analysis**: Memoize with `useMemo` keyed on `[sheetId, rowCount, dataHash]`
- **TanStack virtual rows**: Enable `@tanstack/virtual` for tables > 500 rows
- **Fuzzy matching**: Use `fuse.js` for faster fuzzy search on large datasets
- **Chart rendering**: Limit data points to 100 per chart (aggregate if needed)
- **AI context**: Truncate sample rows to 8, issues to 10, to fit API context window
- **Debounce**: All search inputs debounced 200ms, analysis re-runs debounced 500ms

---

## NAVIGATION STRUCTURE

```
Sidebar Navigation (8 items):
├── 📤  Upload           → Load files, preview, manage sheets
├── 🛡️  Quality          → Issues, auto-clean, merge duplicates
├── 🔀  Compare          → Sheet A vs B matching
├── 📊  Dashboard        → KPIs, charts, insights
├── 📋  Data Table       → Full spreadsheet explorer
├── ⚙️  Normalize        → Normalization rules builder
├── ✅  Validate         → Validation rule builder + run
└── 🤖  AI Assistant     → Claude-powered data chat

Bottom of sidebar:
├── ☀️/🌙  Theme toggle
└── ←→   Collapse sidebar
```

---

## ENVIRONMENT SETUP

### `.env.local`
```
ANTHROPIC_API_KEY=your_key_here
NEXT_PUBLIC_APP_NAME=Jumpstart
NEXT_PUBLIC_APP_VERSION=1.0.0
```

### AI API Route (`app/api/assistant/route.ts`)
```typescript
// POST /api/assistant
// Body: { messages: Message[], context: AssistantContext }
// Returns: streaming text/event-stream response
// Uses Anthropic SDK with claude-sonnet-4-5 or claude-opus-4-5
// System prompt built by contextBuilder.ts
```

---

## PACKAGE.JSON DEPENDENCIES

```json
{
  "dependencies": {
    "next": "^14.0.0",
    "react": "^18.0.0",
    "typescript": "^5.0.0",
    "@anthropic-ai/sdk": "latest",
    "@tanstack/react-table": "^8.0.0",
    "@tanstack/react-virtual": "^3.0.0",
    "zustand": "^4.0.0",
    "framer-motion": "^11.0.0",
    "tailwindcss": "^3.0.0",
    "recharts": "^2.0.0",
    "papaparse": "^5.0.0",
    "xlsx": "^0.18.0",
    "react-dropzone": "^14.0.0",
    "fuse.js": "^7.0.0",
    "lodash": "^4.17.0",
    "date-fns": "^3.0.0",
    "lz-string": "^1.5.0",
    "lucide-react": "latest",
    "class-variance-authority": "latest",
    "clsx": "latest",
    "tailwind-merge": "latest",
    "@radix-ui/react-*": "latest"
  },
  "devDependencies": {
    "@types/lodash": "latest",
    "@types/papaparse": "latest",
    "@types/node": "latest",
    "eslint": "latest",
    "prettier": "latest"
  }
}
```

---

## CODE QUALITY STANDARDS

1. **TypeScript strict mode** — no `any`, all functions fully typed
2. **No inline styles** — all styling via Tailwind classes or CSS variables
3. **Component size** — max 200 lines per component; extract sub-components
4. **Custom hooks** — all business logic in `hooks/`, components are pure UI
5. **Engine functions** — pure functions only in `lib/engine/`, no React dependencies
6. **Error boundaries** — wrap each major view in an ErrorBoundary
7. **Loading states** — every async operation shows a skeleton or spinner
8. **Empty states** — every list/table has an illustrated empty state
9. **Accessibility** — all interactive elements have aria-labels, keyboard navigation works
10. **Comments** — JSDoc on all engine functions, complex algorithms explained inline

---

## BUILD ORDER (RECOMMENDED)

Build in this exact sequence to avoid circular dependencies:

```
Phase 1 — Foundation
  1. types/ — all TypeScript interfaces
  2. lib/utils/ — pure utility functions
  3. lib/engine/ — analysis engines (no React)
  4. lib/parsers/ + lib/exporters/
  5. store/ — Zustand stores

Phase 2 — Shared UI
  6. config/theme.ts + Tailwind config
  7. components/shared/ — Tag, EmptyState, etc.
  8. shadcn/ui component installations

Phase 3 — Feature Modules (parallel)
  9. Upload module
  10. Quality module
  11. Table module
  12. Compare module
  13. Dashboard module
  14. Normalize module
  15. Validate module
  16. Assistant module

Phase 4 — Integration
  17. Layout — Sidebar, TopBar, WorkspaceShell
  18. app/workspace/page.tsx — wire all modules
  19. app/api/assistant/route.ts
  20. Session persistence

Phase 5 — Polish
  21. Framer Motion transitions
  22. Responsive breakpoints
  23. Keyboard shortcuts
  24. Performance optimization (virtual scroll, memoization)
  25. Error boundaries + fallbacks
```

---

## KEYBOARD SHORTCUTS

| Shortcut | Action |
|---|---|
| `⌘/Ctrl + K` | Command palette (quick navigation) |
| `⌘/Ctrl + U` | Go to Upload |
| `⌘/Ctrl + Q` | Go to Quality |
| `⌘/Ctrl + T` | Go to Table |
| `⌘/Ctrl + D` | Go to Dashboard |
| `⌘/Ctrl + .` | Toggle sidebar |
| `⌘/Ctrl + Shift + C` | Run auto-clean (all fixes) |
| `⌘/Ctrl + Z` | Undo last clean |
| `⌘/Ctrl + E` | Export active sheet |
| `⌘/Ctrl + F` | Focus search in table |
| `Escape` | Close modal / deselect rows |

---

## FINAL DELIVERABLE CHECKLIST

Before considering the build complete, verify:

- [ ] All 8 nav views render without errors
- [ ] CSV and Excel (multi-sheet) files parse correctly
- [ ] Quality analysis runs on upload and detects all 13 issue types
- [ ] Auto-clean applies and logs changes, undo works
- [ ] Comparison engine runs exact + fuzzy match correctly
- [ ] TanStack table renders with sort, filter, pagination, virtual scroll
- [ ] All charts render with correct data
- [ ] AI assistant sends context and streams responses
- [ ] Dark and light mode switch smoothly
- [ ] Sidebar collapses and expands with animation
- [ ] Export to CSV and XLSX works for all data views
- [ ] Session auto-saves and restores from localStorage
- [ ] TypeScript compiles with zero errors (`tsc --noEmit`)
- [ ] No `console.error` in browser during normal use
- [ ] App runs fully offline (no CDN dependencies at runtime)

---

*Build Jumpstart as if it will be used daily by a data operations team of 20 people. Every interaction should feel fast, clear, and professional.*

