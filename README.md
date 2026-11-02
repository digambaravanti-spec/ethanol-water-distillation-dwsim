# ethanol-water-distillation-dwsim
Thermodynamic model comparison and reflux sensitivity study of an ethanol-water column in DWSIM
# Ethanol-Water Distillation: Thermodynamic Model Selection and Sensitivity Analysis (DWSIM)

## Objective
Ethanol-water forms an azeotrope at about 89 mol% ethanol (1 atm), so the choice of thermodynamic model and the operating conditions decide how accurately the separation is predicted and how much energy it costs.

## Methods
- **Software:** DWSIM v9
- **Property packages compared:** NRTL, UNIQUAC, Peng-Robinson, Raoult's law
- **Validation:** Txy diagrams at 1.01325 bar compared with experimental VLE data from [Kamihama et al., 2012]
- **Column:** 20 stages, feed stage 10, total condenser, 100 kmol/h feed (50/50 mol%), distillate 50 kmol/h
- **Sensitivity study:** reflux ratio varied from 2 to 11 (manual parametric sweep); 

## Results
- NRTL reproduced the azeotrope (0.88-0.90) mol% ethanol, [78.5] °C); Raoult's law predicted none; Peng-Robinson gave unphysical results at low ethanol fraction.
- Raising the reflux ratio from 2 to 5 doubled the reboiler duty (1635 to 3266 kW) but increased distillate purity only from 0.819 to 0.846.
- Specific energy rose from about 144 to about 550 MJ per kmol ethanol between R = 2 and R = 11.
- Purity is capped near the azeotrope (about 0.894), so more reflux gives diminishing returns.

## Key insights
1. **Model choice matters.** Raoult's law cannot represent the azeotrope at all, and Peng-Robinson fails for this polar, hydrogen-bonding system. An activity-coefficient model (NRTL/UNIQUAC) is needed.
2. **Reboiler duty is linear in reflux ratio** at about 544 kW per unit of R. This follows from the vapor rate V = D(R + 1): 544 kW over 50 kmol/h is about 39 kJ/mol, close to the latent heat of ethanol-water vapor, which is a useful sanity check on the simulation.
3. **Purity shows strongly diminishing returns.** From R = 2 to 11, distillate ethanol rose only from 0.819 to 0.856. R = 3 captures about 41% of that total gain and R = 5 about 74%. Beyond R = 5 each +0.5 in R costs a further 272 kW for under 0.002 of purity.
4. **Specific energy rises about 3.8 times** (144 to 550 MJ/kmol) across the sweep, while purity improves by less than 4 percentage points. Pushing reflux high is energetically wasteful.
5. **Stages and reflux affect different costs.** At fixed reflux, adding stages barely changes reboiler duty (under 0.5%) but improves purity: it is a capital cost, whereas reflux is an operating (energy) cost. The purity gain per added stage shrinks as stages increase (about +0.0032 per stage from 10 to 15 and +0.0012 from 20 to 30).
6. **Purity plateaus below the azeotrope.** Even at R = 11 the distillate reaches 0.856, below the azeotropic limit of about 0.894. With a 50/50 split a large share of ethanol is forced into the bottoms, so the split and number of stages, not only the azeotrope, set this plateau.
7. **Practical operating region (judgment criterion):** R of about 3 to 5. Below it purity falls quickly, and beyond it each extra 272 kW adds almost no separation. Reaching purity above the azeotrope would need a different process, such as extractive or pressure-swing distillation.

## Limitations
- DWSIM's built-in sensitivity tool did not re-converge reliably, so the sweep was done manually.
- Column runs above [30] stages exceeded the solver time limit.
- Only reboiler energy was considered; capital cost and condenser cooling were not.

## Repository contents
| Folder | Contents |
|---|---|
| `simulation/` | DWSIM flowsheet (`.dwxmz`) |
| `data/` | Sensitivity results and experimental VLE data |
| `plots/` | Txy comparison and sensitivity plots 
## Tools
DWSIM, Excel, Python (pandas, matplotlib)
