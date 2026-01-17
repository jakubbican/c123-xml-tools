# Penalties Quality Analyzer

Analyzes ex-post penalty corrections in canoe slalom race results to identify problematic gates.

**Live tool:** https://opencanoetiming.github.io/c123-xml-tools/penalties-quality-analyzer/penalties-quality-analyzer.html

## What It Does

The tool detects when penalties were entered or modified **after** a competitor's run was completed. This happens when:

1. **Time is outside the run interval** - penalty was entered more than 5 seconds before start or more than 30 seconds after finish
2. **Time differs significantly from other penalties** - entry time deviates by more than 10 minutes from the median

High correction counts on specific gates may indicate:
- Poor judge visibility
- Difficult penalty assessment
- Technical issues with electronic entry
- Need for judge repositioning or gate adjustments

## How To Use

1. Export XML file from Canoe123
2. Open the tool and drag & drop the XML file
3. View the results table showing correction counts per gate and race
4. Copy to clipboard for Excel analysis

## Output

The table shows:
- Rows: Individual races (sorted by schedule time)
- Columns: Gate numbers (1, 2, 3, ...)
- Values: Number of detected ex-post corrections
- Colors: Higher intensity = more corrections (orange/red scale)

## Technical Notes

- Works entirely in your browser (no server)
- Analyzes `GateTimes` timestamps vs `dtStart`/`dtFinish` times
- XML format details: see [c123-protocol-docs](https://github.com/OpenCanoeTiming/c123-protocol-docs)
