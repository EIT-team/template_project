This is a template for tidying up the existent software in the EIT system.
Each component should have its own repository, e.g. ScouseTom, RatCGAL, HumanCGAL, ForwardSolver, etc. 
You will have to move files around to an appropriate folder structure following the one this template project has:

```
├── LICENSE.txt
├── build
├── config
│   ├── arduino
│   ├── cxx
│   └── matlab
├── doc
├── lib
├── resources
│   └── data
├── src
│   ├── arduino
│   ├── cxx
│   ├── matlab
│   └── schematics
└── test
    ├── arduino
    ├── cxx
    └── matlab
```

Files should be renamed accordingly, big files (>100MB) should go in the Research Data space, files that can be created with the uploaded code should not be uploaded to GitHub, etc. 

For each component, we should follow the instructions [here](GitConfiguration.md) to have it set up. 
