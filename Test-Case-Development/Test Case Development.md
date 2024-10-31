# Test Plan Documentation
Refer to RTM for the ID numbers.
### Environment Data
- *Browser*: Microsoft Edge
- *Operating System*: Windows 11
- *Application Version*: Planetarium 1.0
- *Access Point*: http://localhost:8080/

## Test Data (ID = 1) 
### Use case: Users should be able to open a User account with the Planetarium

#### 1. Requirement: Usernames and passwords should not be longer than 30 characters
| 0 character Username | 30 characters Username         | 31 characters Usernames         |
|----------------------|--------------------------------|---------------------------------|
|                      | KingofthePiratesoftheGrandLine | AKingofthePiratesoftheGrandLine |

| 0 character Password | 30 characters Password         |31 characters Password|
|----------------------|--------------------------------|-|
|                      | WholeCakeIslandWasAHorribleArc |WholeCakeIslandWasAHorribleArc!|

#### 2. Requirement: Users should have unique usernames
| Unique Username | Non-Unique Username |
|-----------------|---------------------|
| Luffy           | Zoro                |
For the non-unique username, we will have to ensure there is a created User with "Zoro" as their username

#### 3. Requirement: Passwords should never be visible in plaintext
- Password that should be obfuscated: "WholeCakeIslandWasAHorribleArc"
    - use for both Exploratory Testing and Error Guess Testing

#### Acceptance Testing Data
Use positive and negative test data found for the first two requirements 

### Test Scenario
#### Decision Table for Username and Password Length Requirement Testing
| Username                                            | Password                                           | Account Create Result | Redirect                      |
|-----------------------------------------------------|----------------------------------------------------|-----------------------|-------------------------------| 
| (0 characters)                                      | (0 characters)                                     | no user created       | remain in create account page |
| (0 characters)                                      | WholeCakeIslandWasAHorribleArc<br/>(30 characters) | no user created       | remain in create account page |
| KingofthePiratesoftheGrandLine<br/>(30 characters)  | WholeCakeIslandWasAHorribleArc<br/>(30 characters) | user created          | redirect to login page        |
| AKingofthePiratesoftheGrandLine<br/>(31 characters) | WholeCakeIslandWasAHorribleArc<br/>(30 characters) | no user created       | remain in create account page |
| AKingofthePiratesoftheGrandLine<br/>(31 characters) | WholeCakeIslandWasAHorribleArc!<br/>(31 characters)     | no user created       | remain in create account page |

#### Decision Table for Unique Username Requirement Testing
| Username | Password     | Account Create Result | Redirect                      |
|---------|--------------|-----------------------|-------------------------------| 
| Luffy   | MonkeyDLuffy | User created          | redirect to login page |
| Zoro    | RoronoaZoro  | No user created       | remain in create account page |

#### Parameterized Test Scenario
| Step                                                                                     | Actor    | Data           | Result                                                    |
|------------------------------------------------------------------------------------------|----------|----------------|-----------------------------------------------------------| 
| Given the user is on the login page                                                      | new user | http://localhost:8080/ |                                                           |
| when the user clicks on the "Create Account" button                                      | ^^       |                | they should be redirected to the "Create Account" page    |
| When the user provides valid {*username*} and {*password*} and press the "Create" button | ^^       | {username}, {password} |                                                           |
| then the user should receive an alert with the {account result}                          | ^^       | {account result} | alert pops up                                             |
| and the user is redirected back to the login page                                        | ^^       |  | redirect to the login page if successful account creation |

## ID = 2
### Use case: Users should be able to securely access their account

#### 1. Requirement: Passwords should never be visible in plaintext
- Password that should be obfuscated: "WholeCakeIslandWasAHorribleArc"
    - use for both Exploratory Testing and Error Guess Testing

#### 2. Requirement: Only logged-in Users should be able to access the Planetarium home page
- Use Error Guess Testing to check if a user can access the http://localhost:8080/planetarium without having logged in

### Test Scenario
#### Positive Parameterized Test Scenario
| Step                                                                                     | Actor         | Data                   | Result                                                 |
|------------------------------------------------------------------------------------------|---------------|------------------------|--------------------------------------------------------| 
| Given the user is on the login page                                                      | existing user | http://localhost:8080/ |                                                        |
| When the user provides valid {*username*} and {*password*} and preses the "Login" button | ^^            | {username}, {password} | they should be redirected to the "Create Account" page |
| then the user should be redirected and see their planetarium                             | ^^            |                        | redirect to Home Page                                  |

#### Negative Test Scenario
| Step                                                                               | Actor         | Data                              | Result                       |
|------------------------------------------------------------------------------------|---------------|-----------------------------------|------------------------------| 
| Given the user is on the login page                                                | existing user | http://localhost:8080/            |                              |
| when the user tries to access the planetarium without logging in through the {url} | ^^            | http://localhost:8080/planetarium |                              |
| then the user should not see the planetarium                                       | ^^            |                                   | no access to the planetarium |


## ID = 3
### Use case: Users should be able to see planets and moons added to the Planetarium

#### 1. Requirement: Only logged in Users should be able to access the Planetarium home page
- Use Error Guess Testing to check if a user can access the http://localhost:8080/planetarium without having logged in

#### Acceptance Testing 
Confirm upon login that there is data loaded in the User's planetarium

### Test Scenario
Refer to *ID = 2: Positive Parameterized Test Scenario*

## ID = 4
### Use case: Users should be able to add new planets to the Planetarium

#### 1. Requirement: Planet names should not have more than 30 characters
| 0 character Planet | 30 characters Planet           | 31 characters Planet            |
|--------------------|--------------------------------|---------------------------------|
|                    | OdasWorldofOnePiecePirateStory | OdasWorldofOnePieceAPirateStory |

#### 2. Requirement: Planets should have unique names
| Unique Planet | Non-Unique Planet |
|---------------|-------------------|
| Raftel        | East Blue         |
For the non-unique planet name, we will have to ensure there is a created Planet with "East Blue" inside of a User's planetarium

#### 3. Requirement: Planets should be "owned" by the user that added it to the Planetarium
| Username | Password   |
|----------|------------|
| Luffy    | pirateking |
| Zoro     | firstmate  |

Their associated planets:

| User | Planet    |
|----------|-----------|
| Luffy    | Raftel    |
| Zoro     | East Blue |

Use acceptance testing to confirm if you can see Raftel in Zoro's planetarium and East Blue in Luffy's planetarium

#### 4. Requirement: Planets should allow adding an associated image, but an image should not be required for the data to be added to the database
| Planet       | Image          |
|--------------|----------------|
| Loguetown    | pirateking.png |
| Syrup Island | (no image)     |


#### Acceptance Testing Data
Use positive and negative test data found for the first two and the fourth requirements 

### Test Scenario
#### Decision Table for Planet names should not have more than 30 characters requirement testing
| Planet                                              | Planet Creation   | Result          |
|-----------------------------------------------------|-------------------|-----------------| 
| (0 characters)                                      | no planet created | alert pops up   |
| OdasWorldofOnePiecePirateStory<br/>(30 characters)  | planet created    | table refreshes |
| OdasWorldofOnePieceAPirateStory<br/>(31 characters) | no planet created | alert pops up   |

#### Decision Table for Unique Planet Name Requirement Testing
| Planet    | Planet Creation   | Result          |
|-----------|-------------------|-----------------| 
| Raftel    | planet created    | table refreshes |
| East Blue | no planet created | alert pops up   |

#### Decision Table for Planets should allow adding an associated image, but an image is not mandatory requirement testing
| Planet         | Image          | Result          |
|----------------|----------------|-----------------| 
| (0 characters) | (no image)     | alert pops up   |
| Loguetown      | pirateking.png | table refreshes |
| Syrup Island   | (no image)     | table refreshes |

#### Parameterized Test Scenario for Ownership
**_It is important to note that data must already be added to another user's account_

| Step                                                                                            | Actor        | Data                              | Result                                |
|-------------------------------------------------------------------------------------------------|--------------|-----------------------------------|---------------------------------------| 
| Given user X has added planets to their planetarium and the current user is on the login screen | current user | http://localhost:8080/            |                                       |
| when the user provides valid {*username*} and {*password*} and press the "Login" button         | ^^           | {username}, {password}            | alert pops up                         |
| then the current user should be in their planetarium                                            | ^^           | http://localhost:8080/planetarium | redirect to the planetarium home page |
| and they should not see user X's planets                                                        | ^^           |                                   |                                       |

## ID = 5
### Use case: Users should be able to remove planets from the Planetarium

#### 1. Requirement: Users should only be able to interact with resources they have added to the Planetarium
- Use exploratory testing by going through existing users and checking if other user's data are affected when removing planets

### Test Scenario

#### Test Scenario for Positive Planet Removal
**_It is important to note that data must already be added to a user's account_

| Step                                                                                                | Actor  | Data                              | Result                              |
|-----------------------------------------------------------------------------------------------------|--------|-----------------------------------|-------------------------------------| 
| Given user X has existing planets in their planetarium                                              | user X | http://localhost:8080/planetarium |                                     |
| when the user clicks on the dropdown and selects planet                                             | ^^     |                                   | dropdown changes to planet          |
| and provides a valid {*planet name*} that exists in their planetarium and presses the delete button | ^^     | {planet name}                     |                                     |
| then the table refreshes                                                                            | ^^     |                                   | {planet name} is removed from table |

#### Test Scenario for Negative Planet Removal
**_It is important to note that data must already be added to a user's account

*For an invalid planet name, refer to *ID = 4*

| Step                                                                   | Actor  | Data                              | Result                     |
|------------------------------------------------------------------------|--------|-----------------------------------|----------------------------| 
| Given user X has existing planets in their planetarium                 | user X | http://localhost:8080/planetarium |                            |
| when the user clicks on the dropdown and selects planet                | ^^     |                                   | dropdown changes to planet |
| and provides an *invalid {*planet name*} and presses the delete button | ^^     | {planet name}                     | an alert pops up           |
| then no change is detected in the table                                | ^^     |                                   | no change in data          |

## ID = 6
### Use case: Users should be able to add Moons to the Planetarium associated with a planet

* A Planet must exist in the planetarium in order to test these features below
  * Use any existing planet's id to test this usecase

#### 1. Requirement: Moon names should not have more than 30 characters
| 0 character Moon | 30 characters Moon             | 31 characters Moon              |
|------------------|--------------------------------|---------------------------------|
|                  | CaesarClownsArtificialFruits!! | ToMePunkHazardIsntThtBadofAnArc |

#### 2. Requirement: Moons should have unique names
| Unique Planet | Non-Unique Planet |
|---------------|-------------------|
| Whiskey Peak  | Alubarna          |
For the non-unique moon name, we will have to ensure there is a created Moon with "Alubarna" inside a User's planetarium

#### 3. Requirement: Moons should be "owned" by the user that added it to the Planetarium
| Username | Password   |
|----------|------------|
| Luffy    | pirateking |
| Zoro     | firstmate  |

Their associated planets:

| User | Moon           |
|----------|----------------|
| Luffy    | The New World  |
| Zoro     | The Grand Line |

Use acceptance testing and exploratory testing to confirm if you can see "The New World" in Zoro's planetarium and "The Grand Line" in Luffy's planetarium

#### 4. Requirement: Moons should allow adding an associated image, but an image should not be required for the data to be added to the database
| Moon        | Image         |
|-------------|---------------|
| WholeCake   | wholecake.png |
| Arlong Park | (no image)    |


#### Acceptance Testing Data
Use positive and negative test data found for the first two and the fourth requirements

### Test Scenario
#### Decision Table for Moon names should not have more than 30 characters requirement testing
| Moon                                                  | Planet ID     | Moon Creation   | Result          |
|-------------------------------------------------------|---------------|-----------------|-----------------| 
| (0 characters)                                        | (no id)       | no moon created | alert pops up   |
| CaesarClownsArtificialFruits!!<br/>(30 characters)    | (no id)       | no moon created | alert pops up   |
| ToMePunkHazardIsntThtBadofAnArc<br/>(31 characters)   | (no id)       | no moon created | alert pops up   |
| CaesarClownsArtificialFruits!!<br/>(30 characters)    | (existing id) | moon created    | table refreshes |


#### Decision Table for Unique Moon Name Requirement Testing
| Moon         | Moon Creation   | Result          |
|--------------|-----------------|-----------------| 
| Whiskey Peak | moon created    | table refreshes |
| Alubarna     | no moon created | alert pops up   |

#### Decision Table for Moon should allow adding an associated image, but an image is not mandatory requirement testing
| Moon           | Image         | Result          |
|----------------|---------------|-----------------| 
| (0 characters) | (no image)    | alert pops up   |
| WholeCake      | wholecake.png | table refreshes |
| Arlong Park    | (no image)    | table refreshes |

#### Parameterized Test Scenario for Ownership
**_It is important to note that data must already be added to another user's account_

| Step                                                                                          | Actor        | Data                              | Result                                |
|-----------------------------------------------------------------------------------------------|--------------|-----------------------------------|---------------------------------------| 
| Given user X has added moons to their planetarium and the current user is on the login screen | current user | http://localhost:8080/            |                                       |
| when the user provides valid {*username*} and {*password*} and press the "Login" button       | ^^           | {username}, {password}            | alert pops up                         |
| then the current user should be in their planetarium                                          | ^^           | http://localhost:8080/planetarium | redirect to the planetarium home page |
| and they should not see user X's moons                                                        | ^^           |                                   |                                       |

## ID = 7
### Use case: Users should be able to remove moons from the Planetarium

#### 1. Requirement: Users should only be able to interact with resources they have added to the Planetarium
- Use exploratory testing by going through existing users and checking if other user's data are affected when removing planets

### Test Scenario

#### Test Scenario for Positive Moon Removal
**_It is important to note that data must already be added to a user's account_

| Step                                                                                                        | Actor  | Data                              | Result                              |
|-------------------------------------------------------------------------------------------------------------|--------|-----------------------------------|-------------------------------------| 
| Given user X has existing Moons in their planetarium                                                        | user X | http://localhost:8080/planetarium |                                     |
| when the user provides a valid {*moon name*} that exists in their planetarium and presses the delete button | ^^     | {moon name}                       |                                     |
| then the table refreshes                                                                                    | ^^     |                                   | {planet name} is removed from table |

#### Test Scenario for Negative Moon Removal
**_It is important to note that data must already be added to a user's account

*For an invalid planet name, refer to *ID = 6*

| Step                                                                          | Actor  | Data                              | Result            |
|-------------------------------------------------------------------------------|--------|-----------------------------------|-------------------| 
| Given user X has existing moons in their planetarium                          | user X | http://localhost:8080/planetarium |                   |
| when the user provides an invalid {*moon name*} and presses the delete button | ^^     | {moon name}                       | alert pops up     |
| then no change is detected in the table                                       | ^^     |                                   | no change in data |
