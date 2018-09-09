# Dynamic Releases

**How are the releases managed and structured?** 
The project will have snaphot releases pulled from the 'development' branch. 
Individual contributors will have to create their own branches which will be merged against the development branch. The main branch will be used for main releases only.
All previous successful major releases will have own branches.

## Versioning 
The dynamicreports project seeks to adhere to semantic versioning and the artefacts are labelled in the following manner : "Major.Minor.Patch" 

**Major** We have made incompatible API changes
**Minor** We have added functionality in a backwards-compatible manner
**Patch** We have made backwards-compatible bug fixes

## Arguments For

 - Seems practical
 - We will always have access to source code of the previous releases 

## Arguments Against
 - Wait and see...

## TBD
 - We are yet to decide how far back we can inexpensively maintain compatibility for java versions 
