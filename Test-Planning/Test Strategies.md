# Test Strategies
This document is for laying out the types of testing for each use case. Refer to the RTM for the ID number.

## ID = 1 - Users should be able to open a User account with the Planetarium

### Test Strategy List
- *Boundary Value Analysis* : for the boundaries for the input fields when creating an account
- *Equivalence Partitioning* : for testing uniqueness of the username
- *Error Guess Testing* : for password fields being visible or not

## ID = 2 - Users should be able to securely access their account

### Test Strategy List
- *Error Guess Testing* : for password fields being visible or not and for checking if the user can
access the planetarium without being logged in

## ID = 3 - Users should be able to see planets and moons added to the Planetarium

### Test Strategy List
- *Acceptance Testing* : checking the home page to ensure it is indeed their account
  - This may require some user data already being uploaded to the account
- *Error Guess Testing* : for checking if the user can access the planetarium without being logged in

## ID = 4 - Users should be able to add new planets to the Planetarium

### Test Strategy List
- *Boundary Value Analysis* : for the boundaries for the input field when adding a planet
- *Equivalence Partitioning* : for testing the uniqueness of the planet name
- *Acceptance Testing* : for checking that a planet was added and reflected in the planetarium
- *Exploratory Testing* : for checking if the planet belongs to only the specified User
- *Error Guess Testing* : for checking if the user can add a planet without an associated image

## ID = 5 - Users should be able to remove planets from the Planetarium

### Test Strategy List
- *Acceptance Testing* : for checking if the user can remove a planet with valid / invalid planet names
  - planet data must be added before running this test
- *Exploratory Testing* : for checking if the removal of a planet in one account has an effect on another account

## ID = 6 - Users should be able to add Moons to the Planetarium associated with a planet

### Test Strategy List
- *Boundary Value Analysis* : for the boundaries for the input field when adding a moon
  - Associated planet id must also have tests written for them
- *Equivalence Partitioning* : for testing the uniqueness of the moon name
- *Acceptance Testing* : for checking that a moon was added and reflected in the planetarium
- *Exploratory Testing* : for checking if the moon belongs to only the specified User
- *Error Guess Testing* : for checking if the user can add a moon without an associated image

## ID = 7 - Users should be able to remove moons from the Planetarium

### Test Strategy List
- *Acceptance Testing* : for checking if the user can remove a moon with valid / invalid moon names
  - moon data must be added before running this test
- *Exploratory Testing* : for checking if the removal of a moon in one account has an effect on another account
