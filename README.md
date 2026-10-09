# IEA 15 MW OpenFAST 5.0 monopile case

Run from `IEA-15-240-RWT-Monopile`:

```sh
./openfast IEA-15-240-RWT-Monopile.fst
```

The current case uses ElastoDyn with BeamDyn blades (`CompElast=2`), ROSCO control, and 18 m/s IEC ETM seed-2 turbulent wind. Linearization and VTK output are disabled. SeaState, HydroDyn and SubDyn remain disabled in the primary input, as configured in this case.

BeamDyn convergence required adaptive tight coupling (`ModCoupling=3`) with a 0.005 s integration timestep. Tabular output remains sampled every 0.05 s; the production duration remains 660 s. BeamDyn geometry, sectional properties and stiffness-proportional damping were preserved.

The wind file `IEA15MW_IEC_ETM_U18_seed2_OF5.bts` was regenerated from the accompanying TurbSim input using its existing seed and turbulence parameters. Its 290 m grid spans 5–295 m, covering the tower base, and its 720 s duration covers the production run. It is a new realization rather than a byte-identical copy of the previously mismatched wind file.

The controller can emit notch-filter default warnings because the legacy DISCON input declares zero notch filters. The tight-coupling controller-interface warning describes reusing DLL values until simulation time advances. Neither warning is the BeamDyn convergence error.

Validation: OpenFAST v5.0.0 completed a 10 s simulation normally with these settings. All 201 output samples across 1,538 columns were finite. At 10 s, rotor speed was 7.113 rpm, blade-1 pitch was 13.792 degrees, and electrical power was 14,113 kW. Startup aerodynamic warnings included Mach number above 0.3 and temporary unsteady-aero deactivation; the check establishes startup convergence, not accuracy of the full 660 s simulation. The full production duration has not been validated.
