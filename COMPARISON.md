# Journey Planner Code Comparison: Original vs. Improved

## Side-by-Side Comparison

| Aspect | ❌ Original Code | ✅ Improved Code |
|--------|-----------------|-----------------|
| **Layout Engine** | `layout=neato` (no positioning) | `layout=neato` with manual `pos` coordinates |
| **Node Positioning** | Automatic (unpredictable) | Explicit `pos="x,y!"` for every node |
| **Node Size** | `width=0.30` (too large) | `width=0.12` (tube station sized) |
| **Label Position** | Inside nodes (`label=`) | Outside nodes (`xlabel=`) |
| **Timeline Header** | ❌ None | ✅ Week 1-6 markers |
| **Interchange Stations** | ❌ Not distinguished | ✅ Larger nodes, thicker borders |
| **Edge Routing** | `splines=true` (curved) | `splines=polyline` (straighter) |
| **Background** | Plain white | Light grey (`#F9FAFB`) |
| **Spacing** | Default | Optimized with `sep=0.8, pad=0.5` |
| **Line Thickness** | `penwidth=2.4` | `penwidth=3.0` (more visible) |

## Visual Representation of Changes

### Original Code Node Definition
```dot
node [
    shape=circle,
    fixedsize=true,
    width=0.30,           // ❌ Too large
    style=filled,
    fillcolor="white",
    fontname="Helvetica",
    fontsize=9
];

initial_contact [label="Initial Contact"];  // ❌ No position, label inside
```

**Result:** Random positioning, large circles, text inside circles

---

### Improved Code Node Definition
```dot
node [
    shape=circle,
    fixedsize=true,
    width=0.12,           // ✅ Smaller, tube-like
    height=0.12,
    style=filled,
    fillcolor="white",
    fontname="Arial",
    fontsize=7,
    penwidth=1.8,
    color="black"
];

initial_contact [
    pos="0,5!",                    // ✅ Explicit position
    xlabel="Initial\nContact"      // ✅ Label outside node
];
```

**Result:** Controlled positioning, small station circles, external labels

---

## Key Code Changes Explained

### 1. Adding Manual Positioning

**Before:**
```dot
initial_contact          [label="Initial Contact"];
planning_meeting         [label="Planning Meeting"];
```

**After:**
```dot
initial_contact [pos="0,5!", xlabel="Initial\nContact"];
planning_meeting [pos="1.5,5!", xlabel="Planning\nMeeting"];
```

**What changed:**
- Added `pos="x,y!"` - The `!` forces the position (no auto-adjustment)
- Changed `label` to `xlabel` - Places text outside the circle
- Added `\n` line breaks - Makes labels more compact

---

### 2. Timeline Headers

**Before:** ❌ None

**After:**
```dot
// Add timeline headers
node [shape=plaintext, fontsize=9, fontname="Arial Bold"];
week1 [label="Week 1", pos="1,7!"];
week2 [label="Week 2", pos="3,7!"];
week3 [label="Week 3", pos="5,7!"];
week4 [label="Week 4", pos="7,7!"];
week5 [label="Week 5", pos="9,7!"];
week6 [label="Week 6", pos="11,7!"];

// Invisible edges to maintain spacing
edge [style=invis];
week1 -- week2 -- week3 -- week4 -- week5 -- week6;

// Reset node style for stations
node [shape=circle, fontsize=7, fontname="Arial"];
```

**What this does:**
- Creates text labels (not circles) at the top
- Positions them above the station tracks (y=7)
- Connects them with invisible edges to enforce spacing

---

### 3. Interchange Stations

**Before:**
```dot
submission [label="Submission"];
final_approvals [label="Final Approvals"];
```

**After:**
```dot
submission [
    pos="12.5,5!",
    xlabel="SUBMISSION",
    width=0.25,              // ✅ Larger than regular stations
    penwidth=3.5,            // ✅ Thicker border
    fillcolor="#FEE2E2"      // ✅ Light red background
];

final_approvals [
    pos="11,5!",
    xlabel="Final\nApprovals",
    width=0.18,              // ✅ Slightly larger
    penwidth=2.5             // ✅ Thicker border
];
```

**Visual effect:**
- Interchanges stand out with larger circles
- Thicker borders indicate importance
- Optional background color highlights critical milestones

---

### 4. Edge Routing Improvements

**Before:**
```dot
graph [
    bgcolor="white",
    overlap=false,
    splines=true          // ❌ Generic curved splines
];
```

**After:**
```dot
graph [
    bgcolor="#F9FAFB",    // ✅ Subtle grey background
    layout=neato,
    overlap=false,
    splines=polyline,     // ✅ Straight line segments
    sep=0.8,              // ✅ Node separation
    pad=0.5               // ✅ Canvas padding
];
```

**Benefits:**
- `polyline` creates straighter edges (more tube-like)
- `sep=0.8` prevents node overlap
- `pad=0.5` adds breathing room around the graph

---

## Coordinate System Explanation

### Positioning Grid

```
y-axis (Tracks)
    ↑
  7 | WEEK 1    WEEK 2    WEEK 3    WEEK 4    WEEK 5    WEEK 6
  6 |
  5 | ●─────●─────●─────●─────●─────●─────●─────●─────●→ Central Line
  4 |       ●─────●─────●─────●───────────→ Ethics Track
3.5 |             ●─────●───────────→ Proposal Development
  3 |                   ●─────●─────●→ Tech Support
2.5 | ●─────●─────●─────●─────●→ Finance Track
  2 |
  1 | ●─────●─────●─────●─────●─────●→ Partnerships Track
  0 |
    └─────────────────────────────────────────────→ x-axis (Time)
    0     2     4     6     8    10    12
```

### Example Coordinates

| Station | Position | Track | Week |
|---------|----------|-------|------|
| Initial Contact | `(0, 5)` | Central | Week 1 |
| Budget Scope | `(0.5, 2.5)` | Finance | Week 1 |
| HAPLO Setup | `(3.5, 5)` | Central | Week 2 |
| Draft Costs | `(5, 2.5)` | Finance | Week 3 |
| Submission | `(12.5, 5)` | Central | Week 6+ |

---

## Rendering Comparison

### Command to Test Both Versions

```bash
# Original version (will look messy)
neato -Tsvg journey_planner.dot -o original.svg

# Improved version (should look more organized)
neato -Tsvg journey_planner_improved.dot -o improved.svg

# Open both to compare
open original.svg improved.svg
```

### Expected Visual Differences

| Element | Original | Improved |
|---------|----------|----------|
| Layout | Random, chaotic | Organized, linear |
| Station Circles | Large, dominant | Small, subtle |
| Labels | Inside circles (crowded) | Outside circles (clear) |
| Timeline | Missing | Visible at top |
| Interchanges | Not visible | Clearly marked |
| Overall feel | Abstract graph | Tube map aesthetic |

---

## Common Issues and Fixes

### Issue 1: Nodes Still Overlap

**Cause:** Not all nodes have `pos` attributes

**Fix:**
```dot
// Ensure EVERY node has pos="x,y!" with the ! suffix
bad_node [label="Bad"];           // ❌ Will be auto-positioned
good_node [pos="5,3!", xlabel="Good"];  // ✅ Fixed position
```

### Issue 2: Labels Cut Off

**Cause:** Graph canvas too small

**Fix:**
```dot
graph [
    pad=1.0,        // Increase padding
    margin=0.5      // Add margin
];
```

Or render with explicit size:
```bash
neato -Tsvg -Gsize=20,10! journey_planner_improved.dot -o output.svg
```

### Issue 3: Lines Look Messy

**Cause:** Wrong spline setting

**Fix:** Try different settings:
```dot
splines=polyline  // ✅ Best for tube maps
splines=ortho     // ✅ Right-angle bends
splines=line      // ✅ Completely straight
splines=curved    // ❌ Too organic
splines=true      // ❌ Generic curves
```

---

## Further Enhancements (Beyond GraphViz)

### SVG Post-Processing
After generating SVG, you can:
1. Add parallel line segments manually
2. Rotate labels to 45° angles
3. Insert background zones (Thames area)
4. Add legend and branding
5. Create interactive hover effects

### Web Implementation (D3.js)
For production-quality interactive version:

```javascript
// Pseudo-code for D3.js implementation
const stations = [
    { id: "initial_contact", x: 0, y: 5, label: "Initial Contact", line: "central" },
    { id: "planning_meeting", x: 1.5, y: 5, label: "Planning Meeting", line: "central" },
    // ... more stations
];

const lines = [
    { id: "central", color: "#E32017", path: ["initial_contact", "planning_meeting", ...] },
    // ... more lines
];

// D3 rendering code
svg.selectAll("circle.station")
    .data(stations)
    .enter()
    .append("circle")
    .attr("cx", d => xScale(d.x))
    .attr("cy", d => yScale(d.y))
    .attr("r", 6)
    .style("fill", "white")
    .style("stroke", "black");
```

---

## Performance Notes

| Metric | Original | Improved |
|--------|----------|----------|
| Render Time | ~1-2 sec | ~1-2 sec |
| File Size (SVG) | ~50KB | ~60KB |
| Code Readability | Medium | High (with comments) |
| Maintainability | Low (random layout) | High (explicit positions) |

---

## Testing Checklist

- [ ] All nodes have `pos="x,y!"` attributes
- [ ] Node sizes are appropriate (`width=0.12`)
- [ ] Labels are external (`xlabel`)
- [ ] Timeline headers render at top
- [ ] Interchange stations are visually distinct
- [ ] Line colors match TfL standards
- [ ] No node overlaps
- [ ] Labels are readable (not cut off)
- [ ] Graph fits on page/screen
- [ ] SVG renders correctly in browser

---

## Conclusion

**Improvement Summary:**
- **Positioning:** Random → Controlled
- **Aesthetics:** Generic graph → Tube map style
- **Readability:** Cluttered → Clear
- **Maintainability:** Difficult → Easy
- **Usability:** Abstract → Intuitive

**Remaining Challenges:**
1. Cannot create true parallel lines (GraphViz limitation)
2. Limited label rotation options
3. Background zones require manual editing
4. Interchange symbols need SVG enhancement

**Recommended Next Step:**
Use the improved GraphViz code as a **foundation**, then enhance with:
- **For print:** SVG post-processing in Inkscape
- **For web:** D3.js interactive version
- **For documentation:** Current improved code is sufficient

---

**Files to Use:**
- ✅ `journey_planner_improved.dot` - Use this version
- ❌ `journey_planner.dot` - Reference only (shows original problems)
- 📖 `JOURNEY_PLANNER_ANALYSIS.md` - Detailed technical explanation
- 🚀 `README_JOURNEY_PLANNER.md` - Usage guide and quick start
