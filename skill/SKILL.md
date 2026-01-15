# MEDDPIC Deal Analyzer

Analyze sales call transcripts using the MEDDPIC qualification methodology. Generates comprehensive deal analysis with stakeholder mapping, gap identification, and recommended actions.

## Invocation

Use this skill when:
- User says "analyze this deal", "MEDDPIC analysis", "qualify this opportunity"
- User wants to analyze a sales call transcript
- User asks for deal qualification or stakeholder analysis

## Modes

### Quick Mode
Generates: Scorecard + Stakeholder Matrix only
Use when: User says "quick", "scorecard only", "summary"

### Full Mode (Default)
Generates: Complete analysis with all sections
- Executive summary
- MEDDPIC scorecard with maturity assessment
- Stakeholder matrix (7 columns)
- Detailed gap analysis for each MEDDPIC element
- Individual participant deep-dives
- Prioritized action recommendations

## Workflow

### Step 1: Configuration (First Use Only)

On first use, ask:
```
Where would you like to store MEDDPIC analysis files?
Default: /Users/olivier/projects/meddpic analyzer/output/
```

Save the preference for future sessions.

### Step 2: Transcript Source

Ask the user:
```
How would you like to provide the transcript?

1. Fetch from Fireflies.ai
2. Fetch from Fathom.video
3. Upload/paste a transcript directly
```

**If Fireflies or Fathom:**
Ask for:
- Company name or keyword to search
- Time frame (e.g., "this week", "last 7 days", "2026-01-01 to 2026-01-15")

Then use the Fathom Transcripts Extractor app:
- Location: `~/Documents/fathom transcripts extractor`
- Fireflies: `node cli.js extract-fireflies --start DATE --end DATE --keywords "KEYWORD"`
- Fathom: `node cli.js extract-fathom --start DATE --end DATE --keywords "KEYWORD"`

**If Upload:**
User provides transcript text or file path directly.

### Step 3: Participant Detection

After reading the transcript:

1. **Auto-detect participants** from:
   - Email addresses in participant list
   - Speaker names in transcript
   - References to people in conversation

2. **Present to user for confirmation:**
```
I detected the following participants:

INTERNAL (your team):
- [Name] - [email]
- [Name] - [email]

EXTERNAL (prospect):
- [Name] - [email]
- [Name] - [email]

Please confirm:
1. Are the internal/external classifications correct?
2. Is anyone missing from this list?
3. Any speaker attribution errors to correct?
```

3. **Watch for common transcript errors:**
   - Multiple speakers labeled as one person
   - Missing participants mentioned in conversation
   - Role/title information mentioned but not captured

### Step 4: Analysis

Apply MEDDPIC framework (see `meddpic-framework.md` for definitions):

**For each participant, identify:**
- Pain points (2 key ones)
- Level of urgency (LOW / LOW-MEDIUM / MEDIUM-HIGH / HIGH)
- Value interest (what they want to explore)
- Clear value interest? (Yes / No / Partial)
- Primary blocker

**Score each MEDDPIC element (1-10):**
- M - Metrics
- E - Economic Buyer
- D - Decision Criteria
- D - Decision Process
- P - Paper Process
- I - Identify Pain
- C - Champion
- C - Competition

**Scoring guidance:**
- 1-4: Critical gap, blocks deal progression (RED)
- 5-6: Partial information, needs work (YELLOW)
- 7-8: Good understanding, minor gaps (GREEN)
- 9-10: Fully qualified, strong position

### Step 5: Output Generation

**Create output folder:**
```
{output_base_path}/{CompanyName}/
```

**Generate two files:**

1. **Full HTML** (`{CompanyName}_Deal_Analysis.html`)
   - Self-contained, no external dependencies
   - All sections included
   - Printable

2. **2-Page PDF** (`{CompanyName}_Deal_Analysis_2page.pdf`)
   - Executive summary format
   - Page 1: Summary, Scorecard, Stakeholder Matrix, Gap Analysis
   - Page 2: Actions, Detailed Participant Analysis, Key Insight
   - Use Chrome headless: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --print-to-pdf-no-header --print-to-pdf="OUTPUT.pdf" "INPUT.html"`

### Step 6: Present Results

Show user:
1. Overall score and deal health assessment
2. Top 3 critical gaps
3. Immediate next actions
4. File locations

## Output Structure

### Stakeholder Matrix Columns
1. Participant (name)
2. Role
3. Urgency (with color coding)
4. Key Pain Points (2 bullet points)
5. Value Interest
6. Clear Value Interest? (✓ Yes / ✗ No / ⚠ Partial)
7. Primary Blocker

### MEDDPIC Detail Sections
For each element:
- **What We Know**: Bullet points of confirmed information
- **Gap**: What's missing or unclear
- **Action**: Specific question or next step to address the gap

### Action Recommendations
Organized by:
- Overall/Group actions
- Per-participant actions
- Priority levels (HIGH / MEDIUM)

## File Templates

Use templates in this skill folder:
- `template-full.html` - Full analysis template
- `template-2page.html` - Condensed 2-page template
- `meddpic-framework.md` - Framework definitions and scoring guide

## Error Handling

**No transcripts found:**
- Suggest broader date range
- Try different keywords
- Offer to list all available transcripts in range

**Speaker attribution issues:**
- Flag when one speaker has disproportionate talk time
- Check for name mentions that don't match speaker labels
- Ask user to confirm corrections

**Incomplete transcript:**
- Note sections that may be missing
- Adjust confidence in scoring
- Flag in maturity assessment
