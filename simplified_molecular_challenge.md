# 3D Molecular Visualization Challenge - Simplified Edition

## Overview

Create a web-based 3D molecular visualization system that can parse, validate, and display molecular structures with basic interactive features. This challenge focuses on clean architecture, accurate data representation, and engaging visualization rather than complex physics simulation.

**Maximum Score: 100 points**  
**Estimated Time: 1-2 weeks**  
**Target: Browser-based implementation**

## Required Components

### 1. MoleculeParser.js (15 points)
Parse simplified molecular data formats (JSON/CSV) into internal representation.

**Required Methods:**
```javascript
class MoleculeParser {
  // Parse molecule from JSON format
  static parseMoleculeJSON(jsonData)
  
  // Parse molecule from simple CSV format  
  static parseMoleculeCSV(csvData)
  
  // Validate molecule data structure
  static validateMolecule(moleculeData)
  
  // Export molecule to JSON
  static exportToJSON(molecule)
}
```

**Sample Input Format (JSON):**
```json
{
  "name": "Water",
  "atoms": [
    {"id": 1, "element": "O", "x": 0.0, "y": 0.0, "z": 0.0},
    {"id": 2, "element": "H", "x": 0.96, "y": 0.0, "z": 0.0},
    {"id": 3, "element": "H", "x": -0.24, "y": 0.93, "z": 0.0}
  ],
  "bonds": [
    {"atom1": 1, "atom2": 2, "order": 1},
    {"atom1": 1, "atom2": 3, "order": 1}
  ]
}
```

### 2. AtomNode.js (10 points)
Represent individual atoms with properties and 3D coordinates.

**Required Methods:**
```javascript
class AtomNode {
  constructor(id, element, x, y, z)
  
  // Get standard properties for element
  getAtomicNumber()
  getAtomicMass()
  getColor()        // Standard CPK colors
  getRadius()       // Van der Waals radius
  
  // Coordinate manipulation
  getPosition()
  setPosition(x, y, z)
  distanceTo(otherAtom)
}
```

### 3. BondEdge.js (10 points)
Represent chemical bonds between atoms.

**Required Methods:**
```javascript
class BondEdge {
  constructor(atom1, atom2, bondOrder = 1)
  
  getLength()
  getAtoms()
  getBondOrder()
  
  // Get expected bond length from lookup table
  getExpectedLength()
}
```

### 4. MolecularStructure.js (15 points)
Main data structure managing atoms and bonds.

**Required Methods:**
```javascript
class MolecularStructure {
  constructor(name = "Unknown")
  
  // Basic operations
  addAtom(atomNode)
  addBond(bondEdge)
  removeAtom(atomId)
  removeBond(bondId)
  
  // Queries
  getAtoms()
  getBonds()
  findAtomById(id)
  getBondsForAtom(atomId)
  
  // Calculations
  calculateBondAngle(atom1Id, atom2Id, atom3Id)
  calculateMolecularWeight()
  getCenterOfMass()
  
  // Validation
  validateGeometry()  // Check bond lengths/angles against expected values
}
```

### 5. Visualizer3D.js (25 points)
3D visualization using Three.js with interactive controls.

**Required Features:**
```javascript
class Visualizer3D {
  constructor(containerId, width = 800, height = 600)
  
  // Rendering modes
  setRenderMode(mode)  // 'ball-stick', 'space-fill', 'wireframe'
  
  // Display molecule
  loadMolecule(molecularStructure)
  render()
  
  // Interactions
  enableRotation(enabled = true)
  enableZoom(enabled = true)
  
  // Highlighting
  highlightAtom(atomId, color = 0xff0000)
  highlightBond(bondId, color = 0xff0000)
  
  // Animation
  animateRotation(speed = 1.0)
  
  // Export
  takeScreenshot()
}
```

**Visualization Requirements:**
- Ball-and-stick model with proper CPK coloring
- Smooth rotation and zoom controls
- Atom/bond highlighting on hover
- Responsive design for different screen sizes

### 6. AccuracyValidator.js (15 points)
Validate molecular geometry against reference data.

**Required Methods:**
```javascript
class AccuracyValidator {
  constructor(molecularStructure)
  
  // Validation methods
  validateBondLengths()    // Returns {passed: bool, errors: []}
  validateBondAngles()     // Returns {passed: bool, errors: []}
  validateMolecularFormula()
  
  // Generate report
  generateValidationReport()
  
  // Reference data
  static getReferenceData(moleculeName)
}
```

**Reference Data:**
- Pre-defined expected values for common molecules (H2O, CH4, C6H6, etc.)
- Bond length tolerances: ±0.1 Å
- Bond angle tolerances: ±5°

### 7. WebInterface.js (10 points)
Browser interface coordinating all components.

**Required Features:**
```javascript
class WebInterface {
  constructor()
  
  // File handling
  loadMoleculeFile(file)
  
  // UI controls
  setupControls()      // Render mode, rotation, etc.
  updateDisplay()
  
  // Results display
  showValidationResults(report)
  displayMolecularProperties(properties)
}
```

## Test Molecules

Your system will be tested with these molecules (increasing complexity):

1. **Hydrogen (H2)** - Simple diatomic
2. **Water (H2O)** - Angular geometry
3. **Ammonia (NH3)** - Pyramidal geometry  
4. **Methane (CH4)** - Tetrahedral geometry
5. **Benzene (C6H6)** - Planar ring structure

## Scoring Breakdown

### Code Architecture (25 points)
- **File Organization** (5 pts): Clean separation of concerns
- **Class Design** (10 pts): Proper encapsulation and interfaces
- **Error Handling** (5 pts): Graceful failure handling
- **Code Quality** (5 pts): Readable, documented code

### Data Accuracy (30 points)
- **Bond Lengths** (15 pts): Within ±0.1 Å of reference
- **Bond Angles** (10 pts): Within ±5° of reference  
- **Molecular Properties** (5 pts): Correct molecular weight, formula

### Visualization Quality (25 points)
- **3D Rendering** (15 pts): Correct geometry, smooth performance
- **User Interface** (10 pts): Intuitive controls, responsive design

### Functionality (20 points)
- **File Parsing** (8 pts): Handles JSON/CSV input correctly
- **Validation System** (7 pts): Accurate error detection and reporting
- **Interactive Features** (5 pts): Rotation, zoom, highlighting work properly

## Implementation Requirements

### Technology Stack
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **3D Graphics**: Three.js
- **No backend required** - pure client-side implementation

### Browser Compatibility
- Chrome/Firefox/Safari (latest versions)
- Mobile responsive design
- WebGL support required

### File Structure
```
molecular-visualizer/
├── index.html
├── css/
│   └── styles.css
├── js/
│   ├── MoleculeParser.js
│   ├── AtomNode.js
│   ├── BondEdge.js
│   ├── MolecularStructure.js
│   ├── Visualizer3D.js
│   ├── AccuracyValidator.js
│   └── WebInterface.js
├── data/
│   ├── molecules/
│   │   ├── water.json
│   │   ├── methane.json
│   │   └── benzene.json
│   └── reference/
│       └── expected_values.json
└── README.md
```

## Deliverables

1. **Working web application** accessible via browser
2. **Self-assessment report** generated by your validation system
3. **README.md** with setup instructions and feature overview
4. **Demo video** (2-3 minutes) showing key features

## Evaluation Criteria

### Automated Testing
- Load each test molecule
- Validate geometry against reference data
- Test all visualization modes
- Verify interactive controls

### Manual Review
- Code quality and architecture
- User interface design
- Error handling robustness
- Documentation completeness

## Success Metrics

- **80+ points**: Professional-quality implementation
- **60-79 points**: Good implementation with minor issues
- **40-59 points**: Basic functionality working
- **<40 points**: Significant issues or missing components

## Sample Workflow

1. User uploads/selects molecule file
2. Parser validates and loads molecular data
3. Structure validates geometry against reference
4. Visualizer renders 3D model in browser
5. User interacts with controls (rotate, zoom, highlight)
6. Validation report displays accuracy metrics
7. User can export results or screenshots

This simplified version maintains the multi-component architecture and scoring system while being achievable in 1-2 weeks and fully browser-based!