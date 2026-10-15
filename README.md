[README.md](https://github.com/user-attachments/files/33502838/README.md)
# Frac Treating Simulator

A training tool for CalGEM staff who witness hydraulic fracturing (well stimulation) jobs. Enter well, rock and pump schedule inputs, run the job, and watch the treating chart, a wellbore and fracture animation, and live gauges replay together. Diagnostic tabs show the shut-in analysis a witness would work up.

**This is a training model, not a job design tool.** Values open on an illustrative 8,000 ft vertical well.

---

## Quick start

1. Open the simulator link.
2. Review or change the inputs in the left panel.
3. Press **Run job**. The job replays automatically.
4. Use **Play/Pause**, the **speed** selector (simulated minutes per real second) and the **time slider** to move through the job. You can also click or drag on the treating chart to jump to a time.
5. Pick a **scenario** at the top right to see what a problem job looks like.

## Scenarios

| Scenario | What happens | What to look for |
|---|---|---|
| Normal job | Breakdown, pad, proppant ramp, flush, step-down, shut-in | Steady propagation; STP drifts down as heavier slurry fills the hole |
| Screenout | Proppant bridges at the perforations once 3 ppa reaches them | STP climbs fast at constant rate until the pumps kick out |
| Height growth | Barrier stress contrast drops to 0.04 psi/ft | Net pressure flattens; fracture grows into the shale |
| Casing leak | Casing communicates with the surface casing annulus during the 2–3 ppa stage | Annulus jumps; 1785(b)(1) alarm; treatment terminated |

## Inputs

| Group | Inputs |
|---|---|
| Well | Perf TVD, measured depth, casing ID, casing burst, 1784.1 test level (sets the 90% or 80% burst limit), pump kickout |
| Rock and stress | σh gradient in the pay, barrier contrast, σH/σh, pore pressure gradient, tensile strength, Young's modulus, Poisson's ratio, pay height, fluid efficiency |
| Fluid and proppant | Fluid type (sets default viscosity and friction reduction), viscosity, pipe friction reduction %, base fluid density, proppant SG |
| Perforations | Number open, diameter, discharge coefficient (new and eroded), near-wellbore friction at design rate |
| Pumping | Design rate, breakdown rate, step-down test on/off, shut-in monitoring time |
| Annulus | Starting surface casing annulus pressure, ballooning/thermal response |

Edit stages in the **Pump schedule** tab: volume, start and end ppa, and rate. **Set flush to wellbore volume** fills in the flush.

## Screens

- **Animation:** the full wellbore column colored by proppant concentration (plug flow); a zoomed view of the pay and shale barriers with the fracture growing (pad near the tip, proppant behind it); a breakdown flash; closure onto proppant after shut-in; and a plan-view compass showing the fracture along σH.
- **Gauges:** STP, BHTP, hydrostatic, net pressure, perforation, near-wellbore and pipe friction, rate, surface and bottomhole ppa, proppant placed, annulus pressure, and fracture gradient after shut-in. Alarms show here.
- **Treating chart:** STP, BHTP, hydrostatic, annulus and rate, with the burst limit, kickout and closure stress drawn as reference lines. A lower panel shows surface and bottomhole ppa.
- **Pressure budget:** σh + net pressure + perforation friction + near-wellbore friction = BHTP; BHTP − hydrostatic + pipe friction = STP. Updates with the cursor.
- **Shut-in diagnostics:** G-function plot (BH pressure and G·dP/dG) with closure picked; ISIP (surface and bottomhole), fracture gradient, net pressure, closure gradient, efficiency check, and OK/flag witness checks.
- **Step-down test:** friction at each step, split into perforation (∝ q²) and near-wellbore (∝ √q), with the implied number of open perforations.
- **Net pressure:** Nolte–Smith log-log plot with 1/4, 0 and 1 slope guides and the barrier contrast line.
- **Event log:** time-stamped breakdown, stage changes, alarms, shut-in and closure. Events after the cursor are greyed out.

## Model basis

| Item | Method |
|---|---|
| Hydrostatic | 0.052 × density × TVD, summed over the column. Slurry density = (ρf + ppa) ÷ (1 + ppa × absolute volume factor) |
| Pipe friction | Fanning friction with Blasius factor for water, reduced by the friction-reducer % |
| Perforation friction | 0.2369 q² ρ ÷ (n² d⁴ Cd²). Cd rises from the new value to the eroded value as proppant passes |
| Near-wellbore friction | Scales with √q; part of it erodes away with proppant |
| Breakdown | Hubbert–Willis/Kirsch, non-penetrating: 3σh − σH − Pp + T |
| Fracture geometry | PKN length–width relation (Economides & Nolte form), constant fluid efficiency, material balance. Net pressure = E′w ÷ 2h |
| Height growth | Height grows when net pressure exceeds the barrier stress contrast |
| Shut-in decline | Nolte G-function for Carter leakoff. Closure at Gc where η = Gc ÷ (2 + Gc) |
| Water hammer | Damped oscillation with period 4 × MD ÷ 4,700 ft/s |

## Limits

- Vertical well, single fracture, Newtonian fluid, confined-height PKN geometry.
- Cased and perforated wells often break down at a different pressure than the Kirsch estimate.
- Leak, screenout, water hammer and annulus behavior are illustrative.
- Use real job data, charts and the approved permit in the field. Regulatory limits referenced: 14 CCR 1784.1 and 1785.

## Technical

A single self-contained HTML page with no external libraries; fonts load from Google Fonts and fall back to system fonts. It works in light or dark theme and at phone width. It does not save inputs between sessions.
