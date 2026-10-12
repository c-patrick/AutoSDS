# Features

An overview of what SDS Helper does and the logic behind it. For instructions on using it, see the [User Guide](user-guide.md).

**Contents**

- [General](#general)
- [Data validation](#data-validation)
- [Chemical safety](#chemical-safety)
- [Summary of automatic assignments](#summary-of-automatic-assignments)

---

## General

- **A single interface** to input most of the information required for an SDS.
- **Editable output:** When the user clicks **Generate SDS**, an editable Word document is created with the entered information populated.
- **Built-in review comments:** The generated document contains comments that guide the user to the parts that need checking.
- **"No data" for blank fields:** Any box left unfilled returns *"No data"* in the generated SDS.

![The SDS Helper interface](images/interface.png)

## Data validation

### Minimum information

A minimum amount of information is required before an SDS can be generated. The status bar at the bottom of the form shows what is still missing. Currently the requirement is:

- Product Identifier
- Product Use
- Physical State
- Colour
- Physical Form
- A valid CAS number (if one has been entered)

The **Generate SDS** button stays disabled until these are complete.

### CAS number check

If a CAS number is entered, a quick check confirms it is valid. CAS numbers are assigned systematically (the last digit is a check digit calculated from the others), so validity is easy to test. If the number fails the check, the user is prompted that something is wrong.

> *How CAS check digits work, using 7732-18-5 (water) as an example: working from the right, multiply each digit before the check digit by its position (1, 2, 3, …) and add them: 8×1 + 1×2 + 2×3 + 3×4 + 7×5 + 7×6 = 105. The last digit of 105 is 5, which matches the check digit.*

If the CAS number isn't known, leave the field blank and *"No data"* will be added to the generated SDS.

### Physical state check

A warning appears when a selected H phrase doesn't match the physical state. For example, if **Physical State** is *Solid* and **H226: Flammable liquid and vapour** is selected, a pop-up asks the user to confirm whether this is correct. The user can override the warning or cancel and change their selection.

## Chemical safety

### Phrase library

Hazard and precautionary phrases are read from an Excel spreadsheet before the lists on the form are populated. This makes maintenance easy if phrasing or guidance changes: update the spreadsheet and the form picks up the change. See [Installation](installation.md#4-set-up-the-phrase-library).

### Automatic assignments from H phrases

When H phrases are selected, the tool automatically fills in other properties. The logic comes from ECHA's *Guidance on labelling and packaging in accordance with Regulation (EC) No 1272/2008* (available from the [ECHA guidance page](https://echa.europa.eu/support/guidance)). The tool:

- assigns the **P phrases** associated with the selected H phrases;
- assigns the **signal word**, using the highest severity among the selected H phrases; and
- assigns the appropriate **GHS pictograms**.

### Manual override

Any of the default assignments can be overridden before the SDS is generated. **Manual Override** unlocks all fields in the interface so that automatically populated values can be edited.

### Reduced labelling

When **Reduced Labelling** is toggled on, a new section is created in the SDS containing reduced H and P phrases and pictograms. If it isn't selected, no reduced labelling section is created. The logic is also taken from ECHA guidance.

The button only becomes active when reduced labelling is possible.

### Research materials

For materials that haven't been fully assessed, the user can toggle **Research Material**. This prevents H and P phrases, a signal word and pictograms from being added. The resulting SDS shows the yellow exclamation mark together with the text *"Caution - material not fully tested!"*.

## Summary of automatic assignments

| Item | How it is set | Can it be overridden? |
| --- | --- | --- |
| P phrases | Associated with the selected H phrases | Yes, with **Manual Override** |
| Signal word | Highest severity among the selected H phrases | Yes, with **Manual Override** |
| Pictograms | Appropriate to the selected H phrases | Yes, with **Manual Override** |
| Reduced labelling section | Only created if **Reduced Labelling** is toggled on (and available) | n/a |
| Research material wording | Applied when **Research Material** is toggled on; H and P phrases, signal word and pictograms are blocked | n/a |
| Blank fields | Return *"No data"* in the generated SDS | Fill in the field |
