# RAD Journey Planner - TfL Tube Map Style

## Overview
This is a Transport for London (TfL) tube map-style visualization of the LSBU Pre-Award research funding process. The journey planner maps the complex approval workflow as an intuitive, color-coded subway system.

## Files
- `journey-planner.html` - Main visualization file (standalone HTML with embedded SVG)

## Design Features

### Six Journey Lines
1. **Central Line (Red)** - Core Approvals Journey
   - Main pathway through the approval process
   - From Initial Contact to SUBMISSION

2. **Northern Line (Black)** - Ethics & Governance
   - Ethics approval pathway
   - Tech requirements and ethics approval stations

3. **Piccadilly Line (Navy Blue)** - Proposal Development
   - Proposal drafting and development
   - Draft proposal and related stages

4. **District Line (Green)** - Partnerships & Due Diligence
   - Partnership management and due diligence
   - Bottom pathway for partner-related stages

5. **Circle Line (Yellow)** - Costings
   - Financial planning and costing stages
   - Draft and finalized cost calculations

6. **Victoria Line (Light Blue)** - Systems
   - PURE setup and systems integration
   - Technical infrastructure pathway

### Key Stations (Interchange Points)
- **Partner Details** - Multiple lines converge
- **PURE Setup** - System integration point
- **Draft Costs** - Financial planning junction
- **Finalise Costs** - Budget approval junction
- **Tech Requirements/Tech Support** - Technical review point
- **Head of College/ADRI Approval** - Final approval stage
- **SUBMISSION** - Final destination

## Usage
Simply open `journey-planner.html` in any modern web browser. The visualization is:
- Fully responsive
- SVG-based for crisp rendering at any size
- Standalone (no external dependencies)
- Print-friendly

## Authentic TfL Design Elements
- Official TfL color scheme for all lines
- Johnston font family (TfL's typeface)
- Classic roundel logo adapted for "RAD Journey Planner"
- Interchange circles for key decision points
- Legend box with all line descriptions
- Clean, minimalist station design

## Technical Implementation
- Pure HTML5 and SVG
- No JavaScript required
- CSS3 for styling and hover effects
- Responsive design adapts to different screen sizes
- Accessible markup with proper semantic structure

## Browser Compatibility
Works in all modern browsers:
- Chrome/Edge (recommended)
- Firefox
- Safari
- Opera

## Customization
To modify the map:
1. Edit station positions by changing `cx` and `cy` coordinates
2. Adjust line paths using the SVG `path` elements
3. Change colors by modifying the stroke colors in the CSS
4. Add new stations by duplicating existing station markup

## Credits
Design inspired by the iconic London Underground tube map, originally designed by Harry Beck in 1931.
Adapted for LSBU Research Awards & Development (RAD) pre-award processes.
